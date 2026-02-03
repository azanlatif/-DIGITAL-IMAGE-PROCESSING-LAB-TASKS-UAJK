# Task 10: Image Compression - Huffman Coding & JPEG-like DCT Compression
# Submitted By: AZAN LATIF - 2023-SE-14

## Task Overview

This task focuses on **image compression techniques and their analysis** using OpenCV, NumPy, and Python. The objective is to learn how to:

- Implement Huffman coding for entropy-based compression
- Build Huffman trees and generate optimal binary codes
- Apply JPEG-like DCT (Discrete Cosine Transform) compression
- Understand quantization matrices and their effects
- Calculate compression metrics: MSE, PSNR, Compression Ratio
- Analyze rate-distortion tradeoffs in image compression
- Compare original and compressed images visually

## Lab Task Prompt

**Prompt:**
```
Write a comprehensive Python program that demonstrates image compression techniques 
and analysis by:

1. **Huffman Coding Implementation**:
   - Create a HuffmanNode class to represent nodes in the Huffman tree
   - Implement comparison operators for heap operations (__lt__ method)
   - Build a Huffman tree from image pixel frequency distribution:
     * Flatten the image into a 1D array of pixel values
     * Count frequency of each pixel value using Counter
     * Create heap of Huffman nodes for each pixel value
     * Merge nodes iteratively until a single tree remains
   - Generate binary codes for each pixel value:
     * Traverse the tree to create optimal variable-length codes
     * Store codes in a dictionary mapping symbols to bit strings
   - Calculate compressed size using Huffman codes

2. **JPEG-like DCT Compression**:
   - Implement block-based DCT compression:
     * Divide image into 8×8 blocks
     * Apply padding if image dimensions aren't multiples of 8
     * Shift pixel values (subtract 128) for DCT processing
   - Apply Discrete Cosine Transform (DCT) to each block using OpenCV
   - Implement quantization:
     * Use JPEG standard quantization matrix Q
     * Scale quantization matrix based on quality parameter (q)
     * Divide DCT coefficients by quantization matrix
     * Round to nearest integer (lossy step)
   - Apply inverse quantization and IDCT:
     * Multiply by quantization matrix to restore DCT coefficients
     * Apply inverse DCT to reconstruct pixel values
     * Shift back (add 128) to correct range
     * Remove padding and clip values to [0, 255]

3. **Compression Quality Parameter**:
   - Use quality parameter q to control compression-quality tradeoff
   - Lower q values = higher compression but lower quality
   - Higher q values = better quality but lower compression
   - Default q=50 represents medium compression

4. **Compression Metrics Calculation**:
   - **MSE (Mean Squared Error)**:
     * Calculate mean of squared differences between original and compressed
     * Formula: MSE = mean((original - compressed)²)
     * Lower MSE indicates better compression quality
   - **PSNR (Peak Signal-to-Noise Ratio)**:
     * Formula: PSNR = 10 × log₁₀((255²) / MSE)
     * Measured in decibels (dB)
     * Higher PSNR indicates better quality (typical range: 20-50 dB)
   - **Compression Ratio (CR)**:
     * Formula: CR = original_size / compressed_size
     * Ratio of original to compressed data size
   - **Rate Distortion (RD)**:
     * Formula: RD = compressed_size / image_size (in bytes)
     * Bits per pixel metric

5. **Image Loading and Processing**:
   - Load image in grayscale format (single channel)
   - Apply Huffman coding to entire image
   - Apply JPEG-like DCT compression
   - Calculate all metrics for both compression methods

6. **Visualization and Comparison**:
   - Create side-by-side comparison of original and compressed images
   - Display original image in grayscale
   - Display JPEG-compressed image for visual comparison
   - Print all compression metrics and analysis results
```

## What This Task Does

### Step-by-Step Process:

1. **Import Required Libraries**
   - OpenCV (cv2) for image processing and DCT operations
   - NumPy for numerical computations and array operations
   - heapq for heap-based priority queue operations
   - math for logarithmic calculations
   - Counter for frequency counting
   - Matplotlib for visualization

2. **Huffman Coding Implementation**

   **HuffmanNode Class**:
   - Stores symbol (pixel value), frequency, and left/right child references
   - Implements `__lt__` operator for min-heap comparison based on frequency
   
   **build_huffman_tree() Function**:
   - Flattens image into 1D pixel array
   - Counts frequency of each unique pixel value
   - Creates heap with HuffmanNode for each pixel value
   - Repeatedly pops two lowest-frequency nodes and merges them
   - Parent node frequency = sum of children frequencies
   - Process continues until single root node remains
   - Returns tree root and frequency dictionary
   
   **generate_codes() Function**:
   - Recursively traverses Huffman tree
   - Appends '0' when going left, '1' when going right
   - Stores final bit string for each leaf node (pixel value)
   - Returns dictionary of symbol→code mappings
   - Creates optimal variable-length codes
   
   **Huffman Compression Analysis**:
   - Calculates total encoded bits: sum of (frequency × code_length) for all symbols
   - Represents theoretical minimum bits needed using Huffman coding

3. **JPEG-like DCT Compression**

   **Image Preprocessing**:
   - Calculates padding needed to make dimensions multiples of 8
   - Pads image using edge-padding strategy
   - Subtracts 128 from all pixels (center data around zero for DCT)
   
   **Quantization Matrix**:
   - Uses JPEG standard 8×8 quantization matrix Q
   - Scales Q based on quality parameter: Q_scaled = Q × (100 / q)
   - Lower q values → larger scaling factors → more quantization → higher compression
   
   **Block Processing Loop**:
   - Processes image in non-overlapping 8×8 blocks
   - For each block:
     * Apply DCT transformation using cv2.dct()
     * Divide by scaled quantization matrix (lossy compression)
     * Round to nearest integer (further quantization)
     * Multiply by quantization matrix (inverse quantization)
     * Apply inverse DCT using cv2.idct()
   
   **Post-Processing**:
   - Adds 128 back to shift pixel values to original range
   - Removes padding (crop to original dimensions)
   - Clips values to valid range [0, 255]
   - Returns compressed grayscale image

4. **Quality Metrics Calculation**

   **MSE (Mean Squared Error)**:
   - Measures average squared difference between pixel values
   - Formula: MSE = (1/N) × Σ(original - compressed)²
   - N = total number of pixels
   - Lower values = better preservation of original
   
   **PSNR (Peak Signal-to-Noise Ratio)**:
   - Standard metric for image compression quality
   - Formula: PSNR = 10 × log₁₀((255²) / MSE)
   - Special case: if MSE = 0 (lossless), PSNR = infinity
   - Measured in decibels (dB)
   - Typical ranges:
     * < 20 dB: Poor quality
     * 20-30 dB: Low quality
     * 30-40 dB: Good quality
     * > 40 dB: Excellent quality
   
   **Compression Ratio**:
   - Ratio of original size to compressed size
   - Formula: CR = original_size / compressed_size
   - CR > 1 means compression achieved
   - Higher CR = better compression
   
   **Rate Distortion**:
   - Average bits per pixel in compressed data
   - Formula: RD = compressed_size / image_size (in bytes)
   - Represents efficiency of compression

5. **Image Load and Process**
   - Loads image in grayscale format using cv2.imread() with cv2.IMREAD_GRAYSCALE flag
   - Applies all compression and analysis techniques
   - Calculates complete set of metrics

6. **Results Display**
   - Prints compression ratio, MSE, PSNR, and rate-distortion metrics
   - Creates figure with two subplots:
     * Original image (grayscale)
     * Compressed image after JPEG-like DCT compression
   - Side-by-side comparison for visual quality assessment

## Key Concepts Covered

### 1. **Huffman Coding**
   - **Entropy-based compression**: Assigns shorter codes to more frequent symbols
   - **Optimal property**: Produces codes with minimum average length
   - **Variable-length encoding**: Different symbols get different code lengths
   - **Tree structure**: Binary tree where leaves are symbols, paths are codes

### 2. **DCT (Discrete Cosine Transform)**
   - Converts pixel values from spatial domain to frequency domain
   - Concentrates information in low-frequency coefficients
   - High-frequency components often represent noise/details
   - Allows selective discard of less important information

### 3. **Quantization**
   - Reduces precision of coefficients (lossy step)
   - Larger divisors → more aggressive quantization → more compression but lower quality
   - JPEG standard matrix emphasizes human visual system's sensitivity
   - Different quantization for different frequency components

### 4. **Compression Tradeoff**
   - **Lossy Compression**: Some data permanently lost (DCT compression)
   - **Lossless Compression**: No data lost, original recoverable (Huffman coding)
   - **Quality vs Size**: Higher compression usually means lower quality
   - **Rate-Distortion**: Fundamental tradeoff between file size and quality

### 5. **Image Block-Based Processing**
   - Division into 8×8 blocks reduces computational complexity
   - Allows independent processing of image regions
   - Padding ensures block-aligned dimensions
   - Standard in JPEG format

## Implementation Highlights

- **Object-Oriented Design**: HuffmanNode class for tree representation
- **Heap Data Structure**: Efficient priority queue for building Huffman tree
- **Dictionary Mapping**: Fast lookup of symbols to codes
- **Numpy Array Operations**: Efficient block-level image processing
- **OpenCV DCT/IDCT**: Optimized implementations for transform operations
- **Error Handling**: Special case for MSE = 0 in PSNR calculation
- **Padding Strategy**: Edge-padding preserves image characteristics

## Expected Outcomes

- Understanding of lossless compression (Huffman coding)
- Understanding of lossy compression (DCT + Quantization)
- Practical knowledge of JPEG compression pipeline
- Ability to calculate and interpret compression metrics
- Understanding of rate-distortion tradeoff
- Proficiency in block-based image processing
- Knowledge of frequency domain analysis and image compression

## Compression Comparison

### Huffman Coding
- **Type**: Lossless
- **Typical Ratio**: 2-5:1 depending on image content
- **PSNR**: Infinite (no loss)
- **Use Case**: Text, medical images, archival

### JPEG-like DCT
- **Type**: Lossy
- **Typical Ratio**: 10-100:1 depending on quality
- **PSNR**: Variable (quality-dependent)
- **Use Case**: Photography, web images, streaming

## Prerequisites

- Python 3.x
- OpenCV (cv2)
- NumPy
- Matplotlib
- Image file in JPEG format (update path in code)

## Run Instructions

1. Install required libraries: `pip install opencv-python numpy matplotlib`
2. Place image file (e.g., "image11.jpeg") in the working directory
3. Update image path in the code if using different filename
4. Run the notebook cell to process and display results
5. Analyze compression metrics and visual quality

## Quality Parameter Testing

Experiment with different quality values:
- q = 10: Extreme compression, very poor quality
- q = 30: High compression, acceptable quality
- q = 50: Moderate compression, good quality (default)
- q = 80: Low compression, excellent quality
- q = 100: Minimal compression, near-original quality

---

**Task Type**: Image Compression & Quality Analysis  
**Difficulty Level**: Advanced  
**Key Skills**: Data compression, frequency domain analysis, information theory, algorithm implementation, metric calculation, image quality assessment
