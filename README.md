# Optimized-US-Accidents-Dataset

# 📌 Overview
This project analyzes the US Accidents dataset (2016-2023) containing over 7.7 million accident records using GPU-accelerated data processing with RAPIDS (cuDF, cuPY) for high-performance analytics.

# 🚀 Key Features
  - GPU-accelerated processing using RAPIDS (cudf, cupy)
  - Memory optimization through smart dtype conversions (from 3.0 GB to 1.8 GB)
  - Detecting outliers with 3 different methods

# 📂 Dataset

## US Accidents (2016-2023)
  -Size: 653MB (compressed), ~3GB uncompressed  
  -Records: 7,728,394 accidents  
  -Features: 46 original columns (reduced to 42 after cleaning)  
  -Source: https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://www.kaggle.com/datasets/sobhanmoosavi/us-accidents  

# 🔍 Outlier Detection Methods
### IQR-based outlier
The IQR (Interquartile Range) rule is a method used to identify outliers in a dataset. It works by defining a range within which most data points are expected to fall, and any data point outside that range is considered an outlier  
![Outlier Visualization](https://www.scribbr.com/wp-content/uploads/2022/11/Interquartile-range-example.webp)
```python
Q1_Lat = df['Start_Lat'].quantile(0.25)  # 1st quartile
Q3_Lat = df['Start_Lat'].quantile(0.75)  # 3rd quartile  
IQR_Lat = Q3_Lat - Q1_Lat  # Interquartile range
```

### Geographic Bounds Method
works by defining min and max latitude and longitude to use as an outlier
```python
us_bounds = {
    'lat_min': 25.0, 'lat_max': 49.0,
    'lng_min': -124.0, 'lng_max': -66.0
}
```
### Grid-Based Density Detection
works by identifying isolated locations by analysing point density in a grid\
  - devides the map into 0.1°×0.1° cells
      - ```python
        df['lat_bin'] = (df['Start_Lat'] * 10).round()
        df['lng_bin'] = (df['Start_Lng'] * 10).round()
  - counts accidents per cell
      - ```python
        grid_counts = df.groupby(['lat_bin', 'lng_bin']).size().rename('count')
  - cells with <=5 points are considered as outliers
      - ```python
        df['outlier'] = df['count'] <= 5

# 🎯 Key Optimizations
|Optimization         | Memory Savings  |	Performance Impact         |
|---------------------|-----------------|----------------------------|
|Float64→Float32	    | ~25% reduction  | 2-3x speedup               |
|Categorical encoding | ~40% reduction	| 5-10x speedup for groupbys |
|uint8 for severity   | ~90% reduction  |	Minimal impact             |

