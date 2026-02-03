# Task 12: Image Segmentation Techniques
# Submitted By: AZAN LATIF - 2023-SE-14

## Task Overview

This task focuses on **image segmentation methods and clustering algorithms** using OpenCV, scikit-learn, and scikit-image. The objective is to learn how to:

- Apply various thresholding techniques (Global, Local, Adaptive)
- Implement K-Means clustering for image segmentation
- Apply Mean Shift segmentation algorithm
- Understand automatic threshold selection methods
- Compare different segmentation approaches
- Visualize segmented regions with colormaps
- Analyze the effect of cluster numbers on segmentation quality

## Lab Task Prompt

**Prompt:**
```
Write a comprehensive Python program that demonstrates various image segmentation 
techniques and clustering algorithms by:

1. **TASK 1: Thresholding Techniques**

   (a) Global Thresholding Using Otsu's Method:
   - Load a colored image and convert to grayscale
   - Apply Otsu's automatic threshold selection algorithm
   - Otsu's method finds the optimal threshold value that minimizes intra-class variance
   - Create binary image by comparing each pixel to the calculated threshold T
   - Formula: BW_global = I > T (where T is Otsu's threshold)
   - Display the resulting binary segmentation

   (b) Local Thresholding:
   - Apply threshold_local() with a specified block/neighborhood size (e.g., 51×51)
   - Calculate local threshold value for each pixel based on neighborhood mean
   - Use offset parameter (e.g., 0.4) to adjust threshold sensitivity
   - Create binary image: BW_local = I > local_threshold
   - Local thresholding adapts to varying illumination across the image
   - Display the resulting segmentation showing better handling of non-uniform lighting

   (c) Adaptive Thresholding:
   - Apply threshold_local() with a block size and zero offset for pure adaptive method
   - Adaptive thresholding adjusts threshold based on local image statistics
   - Similar to local thresholding but with different offset/calculation methods
   - Create binary image: BW_adaptive = I > adaptive_threshold
   - Display the resulting segmentation

2. **TASK 2: K-Means Segmentation**

   For K = 2, 3, and 4 clusters:
   - Convert image to float format (0-1 range)
   - Flatten the grayscale image into a 1D array of pixel values
   - Apply K-Means clustering algorithm from scikit-learn:
     * Initialize K cluster centers randomly
     * Iteratively assign pixels to nearest cluster center
     * Update cluster centers based on mean of assigned pixels
     * Repeat until convergence (center positions stabilize)
   - Perform separate clustering for K=2, K=3, and K=4
   - Use random_state=0 for reproducibility
   - Use n_init=10 for better cluster initialization (modern sklearn parameter)
   - Reshape cluster labels back to original image dimensions
   - Display segmentation result for each K value using colormap
   - Analyze how increasing K creates finer segmentation
   - Observe cluster boundaries and number of distinct regions

3. **TASK 3: Mean Shift Segmentation**

   - Load the colored (RGB) image for better segmentation
   - Reshape image to 2D array where each row is a pixel (R,G,B vector)
   - Normalize pixel values to 0-1 range for proper distance calculation
   - Estimate bandwidth parameter using estimate_bandwidth():
     * bandwidth controls the radius of kernel
     * Use quantile=0.2 to estimate from data distribution
     * Use n_samples=500 to sample data for efficiency
     * quantile parameter: larger value = larger bandwidth = coarser segmentation
   - Apply Mean Shift clustering:
     * Iteratively find mode (peak) of density in feature space
     * Each point follows density gradient to nearest mode
     * Points converging to same mode form one cluster
     * bin_seeding=True speeds up convergence
     * n_jobs=-1 enables parallel processing
   - Get cluster labels for each pixel
   - Reshape labels back to image dimensions
   - Display segmented image with different colors for different clusters
   - Observe natural cluster formation based on color similarity

4. **Image Loading and Preprocessing**:
   - Load test image (image22.jpeg) or create sample image if unavailable
   - Convert BGR to RGB for proper color representation
   - Convert RGB to grayscale where needed
   - Handle file not found errors gracefully

5. **Visualization and Comparison**:
   - Display results for each thresholding method separately
   - Display K-Means results for K=2, K=3, K=4
   - Display Mean Shift segmentation result
   - Use appropriate colormaps (gray for binary, viridis for clusters)
   - Include titles for each segmentation result
   - Allow visual comparison of different techniques

6. **Analysis and Interpretation**:
   - Compare thresholding methods for robustness to lighting variations
   - Analyze K-Means segmentation with different K values
   - Observe Mean Shift's natural cluster discovery
   - Understand tradeoffs between computational complexity and segmentation quality
```

## What This Task Does

### Step-by-Step Process:

1. **Import Required Libraries**
   - scikit-image (skimage) for image I/O and filtering
   - scikit-learn (sklearn) for clustering algorithms
   - NumPy for numerical operations
   - Matplotlib for visualization

2. **TASK 1: Thresholding Techniques**

   **(a) Global Thresholding - Otsu's Method**:
   - **Image Loading**: Reads colored image, converts to grayscale
   - **Otsu's Algorithm**:
     * Computes histogram of grayscale values
     * Tests each possible threshold value T (0-255)
     * For each T, calculates between-class variance:
       - Variance of foreground pixels above T
       - Variance of background pixels below T
     * Selects T that maximizes between-class variance
     * This minimizes within-class variance (more homogeneous segments)
   - **Binarization**: BW_global = I > T (pixels > T become white, ≤ T become black)
   - **Advantage**: Fully automatic, no manual threshold selection
   - **Limitation**: Assumes single optimal threshold for entire image

   **(b) Local Thresholding**:
   - **Sliding Window Approach**:
     * Divides image into overlapping blocks (window size = block_size)
     * Calculates threshold independently for each block
     * Default block_size = 51 × 51 pixels
   - **Threshold Calculation**:
     * Computes mean intensity within neighborhood
     * Applies offset to adjust sensitivity
     * threshold = neighborhood_mean - offset (with offset=0.4)
   - **Binarization**: BW_local = I > local_threshold
   - **Advantage**: Adapts to varying illumination across image
   - **Use Case**: Images with uneven lighting, shadows, or gradients

   **(c) Adaptive Thresholding**:
   - **Similar to Local**: Uses threshold_local() with similar window approach
   - **Key Difference**: offset = 0 for pure adaptive method
   - **Threshold Formula**: threshold = neighborhood_mean - 0
   - **Binarization**: BW_adaptive = I > adaptive_threshold
   - **Advantage**: Simpler adaptive approach without offset
   - **Comparison**: Compare with local to observe offset effect

3. **TASK 2: K-Means Segmentation**

   **Data Preparation**:
   - Converts grayscale image to float (0-1 range)
   - Flattens to 1D array: each pixel value is a data point
   - Reshapes to 2D array for sklearn: shape (n_pixels, 1)

   **K-Means Algorithm**:
   - **Initialization**: Randomly places K cluster centers
   - **Assignment Step**: Assigns each pixel to nearest center using Euclidean distance
   - **Update Step**: Recalculates each center as mean of assigned pixels
   - **Iteration**: Repeats assignment and update until convergence
   - **Convergence**: Centers stabilize or max iterations reached
   - **Parameters**:
     * n_clusters=k: Number of clusters to find
     * random_state=0: Fixed seed for reproducibility
     * n_init=10: Runs algorithm 10 times with different initializations

   **K=2 Segmentation**:
   - Divides image into 2 regions (dark and bright)
   - Creates clear foreground-background separation
   - Labels reshaped to original image dimensions
   - Visualized with colormap

   **K=3 Segmentation**:
   - Adds intermediate cluster for mid-tones
   - Provides 3-level segmentation
   - Shows how increasing K refines segmentation
   - Better capture of image details

   **K=4 Segmentation**:
   - Finest level of clustering with 4 regions
   - Further segmentation of tonal ranges
   - Demonstrates progressive segmentation refinement
   - More distinct region boundaries

   **Visualization**: Uses viridis colormap to distinguish clusters

4. **TASK 3: Mean Shift Segmentation**

   **Color Image Preparation**:
   - Loads colored (RGB) image for better color-based segmentation
   - Reshapes to 2D array: shape (n_pixels, 3) where each row is [R,G,B]
   - Normalizes to 0-1 range for proper distance calculations

   **Bandwidth Estimation**:
   - **estimate_bandwidth() Function**:
     * Samples n_samples=500 pixels from image
     * Calculates distances between samples
     * Estimates bandwidth from quantile of distance distribution
     * quantile=0.2: Uses 20th percentile of distances
   - **Effect of Bandwidth**:
     * Small bandwidth: Many small clusters, fine segmentation
     * Large bandwidth: Few large clusters, coarse segmentation
     * quantile=0.2 typically produces good balance

   **Mean Shift Algorithm**:
   - **Kernel Density Estimation**: Each point has associated kernel (typically Gaussian)
   - **Density Gradient**: Calculates gradient of estimated density
   - **Mode Seeking**: Each point moves in direction of density gradient
   - **Convergence**: Point converges to local mode (peak) of density
   - **Clustering**: Points converging to same mode form one cluster
   - **Parameters**:
     * bandwidth: Kernel radius (estimated automatically)
     * bin_seeding=True: Uses grid-based initial seeds for speed
     * n_jobs=-1: Uses all CPU cores for parallel processing

   **Result Interpretation**:
   - Different colors represent different clusters
   - Natural color grouping emerges from pixel similarity
   - Fewer over-segmentation artifacts than K-Means
   - Discovers variable-sized clusters based on density

5. **Error Handling**
   - Checks if image file exists
   - Creates dummy image if file not found
   - Allows code to run with sample data

6. **Visualization**
   - Each segmentation displayed in separate figure
   - Appropriate colormaps for each task
   - Titles indicate segmentation method
   - Easy comparison of different techniques

## Key Concepts Covered

### 1. **Thresholding Techniques**

   **Global Thresholding**:
   - Single threshold value applied to entire image
   - Otsu's method automatically selects optimal threshold
   - Fast and simple but limited for non-uniform illumination
   - Mathematical basis: Maximize between-class variance

   **Local Thresholding**:
   - Threshold varies across image based on local neighborhood
   - Handles varying illumination and shadows
   - Offset parameter controls sensitivity
   - More robust to lighting variations

   **Adaptive Thresholding**:
   - Similar concept to local thresholding
   - Adjusts threshold based on local statistics
   - Can use different offset values
   - Bridges local and global approaches

### 2. **K-Means Clustering**

   **Algorithm Overview**:
   - Partitions data into K non-overlapping clusters
   - Minimizes within-cluster variance
   - Iterative refinement until convergence

   **Properties**:
   - Fast and simple to implement
   - Requires specifying K in advance
   - Sensitive to initialization
   - Works well for roughly spherical clusters

   **For Image Segmentation**:
   - Each pixel intensity is a data point
   - Segments image into K intensity levels
   - K determines segmentation granularity
   - Results in labeled regions

### 3. **Mean Shift Clustering**

   **Algorithm Overview**:
   - Non-parametric density estimation approach
   - No need to specify number of clusters
   - Automatically discovers variable-sized clusters

   **Properties**:
   - Based on kernel density estimation
   - Robust to outliers
   - Computationally more expensive than K-Means
   - Discovers natural clusters without parameter tuning

   **For Image Segmentation**:
   - Works in color space (RGB vectors)
   - Finds modes of color distribution
   - Produces more natural-looking segments
   - Better for non-uniform cluster sizes

### 4. **Comparison of Methods**

   | Method | Speed | Parameters | Cluster Shape | Use Case |
   |--------|-------|------------|---------------|----------|
   | Otsu | Very Fast | None | Binary | High contrast images |
   | Local Threshold | Fast | Block size | Binary | Variable lighting |
   | K-Means | Fast | K | Spherical | Quick segmentation |
   | Mean Shift | Slow | Bandwidth | Any | Natural segmentation |

### 5. **Segmentation Quality Factors**

   - **Homogeneity**: Pixels in same segment should be similar
   - **Connectivity**: Segments should be spatially connected
   - **Boundary**: Segment boundaries should align with image features
   - **Overfitting**: Avoiding too many or too few clusters

## Implementation Highlights

- **Automatic Threshold Selection**: Otsu's method eliminates manual tuning
- **Adaptive Processing**: Local/Adaptive thresholding handles varied lighting
- **Clustering Variety**: Demonstrates parametric (K-Means) and non-parametric (Mean Shift)
- **Color Space Handling**: RGB normalization for Mean Shift
- **Bandwidth Estimation**: Automatic selection of Mean Shift parameters
- **Parallel Processing**: Multi-core acceleration for Mean Shift
- **Error Resilience**: Graceful handling of missing files

## Expected Outcomes

- Understanding of binary thresholding approaches
- Knowledge of automatic threshold selection
- Practical experience with K-Means clustering
- Understanding of Mean Shift algorithm
- Ability to choose appropriate segmentation method
- Proficiency in comparing segmentation results
- Knowledge of parameter effects on segmentation quality
- Understanding of computational complexity tradeoffs

## Segmentation Method Selection Guide

**Use Global Thresholding (Otsu) when:**
- Image has clear bimodal histogram
- High contrast between foreground and background
- Uniform lighting conditions
- Speed is critical

**Use Local/Adaptive Thresholding when:**
- Illumination varies across image
- Shadows or highlights present
- Need to handle non-uniform lighting
- Willing to trade speed for robustness

**Use K-Means when:**
- Number of objects/regions is known
- Need fast segmentation
- Roughly uniform cluster sizes
- Working with intensity values

**Use Mean Shift when:**
- Number of clusters unknown
- Want automatic cluster discovery
- Need high-quality natural segmentation
- Have computational resources available
- Working with color image

## Prerequisites

- Python 3.x
- OpenCV (cv2) or scikit-image
- scikit-learn for clustering
- NumPy
- Matplotlib
- Image file in JPEG format (update path in code)

## Required Libraries Installation

```bash
pip install scikit-image scikit-learn numpy matplotlib opencv-python
```

## Run Instructions

1. Install required libraries
2. Place image file (e.g., "image22.jpeg") in the working directory
3. Run notebook cells sequentially:
   - First cell loads dependencies
   - Cells 2-4: Test thresholding methods
   - Cells 5-7: Test K-Means with K=2,3,4
   - Cell 8: Test Mean Shift segmentation
4. Observe and compare segmentation results
5. Analyze which method works best for your image

## Parameter Tuning Guide

### Thresholding
- **Block size for local/adaptive**: Larger = coarser segmentation (try 31, 51, 101)
- **Offset**: Larger offset = lower threshold = more white pixels (try 0, 0.2, 0.4, 0.6)

### K-Means
- **K (number of clusters)**: Start with 2-4, increase for more detail
- **n_init**: Higher = better results but slower (try 10-100)

### Mean Shift
- **quantile in estimate_bandwidth**: Lower = finer segmentation (try 0.1-0.3)
- **n_samples**: Lower = faster but less accurate (try 100-1000)

## Example Interpretation

For a landscape image:
- Otsu: Sky vs. ground with artifacts
- Local threshold: Better detail preservation with lighting adaptation
- K-Means with K=3: Sky, mid-tones, ground
- Mean Shift: Natural color grouping (sky, clouds, vegetation, ground)

---

**Task Type**: Image Segmentation & Clustering  
**Difficulty Level**: Intermediate to Advanced  
**Key Skills**: Image analysis, clustering algorithms, thresholding, parameter tuning, segmentation quality assessment, algorithm comparison
