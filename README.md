# Optimized-US-Accidents-Dataset

# 📌 Overview
This project analyzes the US Accidents dataset (2016-2023) containing over 7.7 million accident records using GPU-accelerated data processing with RAPIDS (cuDF, cuPY) for high-performance analytics.

# 🚀 Key Features
  - GPU-accelerated processing using RAPIDS (cudf, cupy)
  - Memory optimization through smart dtype conversions

# 📂 Dataset

## US Accidents (2016-2023)
  -Size: 653MB (compressed), ~3GB uncompressed  
  -Records: 7,728,394 accidents  
  -Features: 46 original columns (reduced to 42 after cleaning)  
  -Source: https://www.google.com/url?sa=t&source=web&rct=j&opi=89978449&url=https://www.kaggle.com/datasets/sobhanmoosavi/us-accidents  


# 🎯 Key Optimizations
|Optimization         | Memory Savings  |	Performance Impact         |
|---------------------|-----------------|----------------------------|
|Float64→Float32	    | ~25% reduction  | 2-3x speedup               |
|Categorical encoding | ~40% reduction	| 5-10x speedup for groupbys |
|uint8 for severity   | ~90% reduction  |	Minimal impact             |

