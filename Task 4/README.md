# Task 4: Image Enhancement Techniques
# Submitted By: AZAN LATIF - 2023-SE-14

## Overview
This lab task focuses on implementing various **image enhancement techniques** to improve image quality by adjusting contrast, brightness, and pixel intensity distribution. The task covers both built-in OpenCV functions and manual implementations of enhancement algorithms.

## Objectives
- Understand image enhancement and its importance in Digital Image Processing
- Implement multiple image enhancement techniques
- Compare the effects of different enhancement methods
- Learn the mathematical foundations behind each technique

## Task Description

This task implements the following image enhancement techniques:

### 1. **Histogram Equalization (Built-in Method)**
- **Concept**: Redistributes pixel intensity values to improve contrast
- **Process**:
  - Convert image from BGR to YCrCb color space
  - Apply histogram equalization only to the Y channel (luminance)
  - Preserve color information by keeping Cr and Cb channels unchanged
  - Convert back to RGB for display
- **Benefit**: Enhances contrast while preserving natural color appearance

### 2. **Manual Histogram Equalization**
- **Concept**: Implements histogram equalization from scratch using:
  - Histogram calculation
  - CDF (Cumulative Distribution Function) computation
  - Normalization and pixel mapping
- **Process**:
  1. Convert image to grayscale
  2. Calculate histogram of pixel intensities
  3. Compute and normalize CDF
  4. Map each pixel value using the normalized CDF
- **Benefit**: Demonstrates the mathematical principles behind histogram equalization

### 3. **Contrast Stretching**
- **Concept**: Extends the range of pixel intensities to use the full available spectrum (0-255)
- **Formula**: `stretched = ((gray - min) / (max - min)) * 255`
- **Benefit**: Improves visibility when image has poor contrast due to limited intensity range

### 4. **Log Transform**
- **Concept**: Compresses the range of bright values and expands the range of dark values
- **Formula**: `log_img = c * log(1 + gray)` where c is a scaling constant
- **Benefit**: Useful for images with large intensity variations; reveals details in dark regions

### 5. **Gamma Transform**
- **Concept**: Applies a power-law transformation to adjust image brightness
- **Formula**: `gamma_corrected = normalized^gamma`
- **Parameters**:
  - gamma > 1: Darkens the image (brightens shadows)
  - gamma < 1: Brightens the image (darkens highlights)
- **Benefit**: Non-linear brightness adjustment with perceptual control

## How to Run This Lab

### Requirements
```
opencv-python (cv2)
numpy
matplotlib
```

### Steps to Execute

1. **Prepare Your Image**
   - Replace the image path in the notebook with your own image file
   - Current path: `/content/WhatsApp Image 2025-10-29 at 1.23.12 AM.jpeg`
   - Supported formats: JPG, PNG, BMP, etc.

2. **Run Each Cell Sequentially**
   - Cell 1: Import required libraries
   - Cell 2: Load and display the original image
   - Cell 3: Apply histogram equalization (built-in method)
   - Cell 4: Implement and apply manual histogram equalization
   - Cell 5: Compare histograms (before and after)
   - Cell 6: Apply contrast stretching
   - Cell 7: Apply log and gamma transforms

3. **Observe Results**
   - Compare the visual differences between techniques
   - Analyze histogram changes
   - Evaluate which method works best for your image

## Expected Outputs

| Technique | Effect | Use Case |
|-----------|--------|----------|
| Histogram Equalization | Improves overall contrast | Low-contrast images |
| Contrast Stretching | Stretches intensity range | Images with limited dynamic range |
| Log Transform | Enhances dark regions | Images with bright highlights |
| Gamma Transform | Non-linear brightness adjustment | Compensating for camera/display characteristics |

## Lab Prompt & Instructions
```
**Objective**: Implement and compare image enhancement techniques

**Task Requirements**:
1. Load an image using OpenCV
2. Implement histogram equalization using two methods:
   - Using OpenCV's built-in `equalizeHist()` function
   - Manual implementation using CDF calculation
3. Apply contrast stretching to normalize pixel intensities
4. Implement log and gamma transforms for non-linear enhancement
5. Display and compare results visually
6. Create histogram plots to show the effect of equalization

**Expected Deliverables**:
- ✓ Original image display
- ✓ Histogram equalization (built-in and manual)
- ✓ Histogram comparison plots
- ✓ Contrast stretching results
- ✓ Log and gamma transform comparisons
```
## Key Concepts

### Why Image Enhancement Matters
- Improves visibility of important features
- Corrects poor lighting conditions
- Prepares images for further processing (object detection, recognition, etc.)
- Enhances visual quality for human interpretation

### Mathematical Foundations
- **Histogram**: Graphical representation of pixel intensity distribution
- **CDF**: Cumulative sum of histogram values
- **Normalization**: Scaling values to a specific range (0-255)
- **Power-law transform**: General form of gamma correction

## Tips for Success

1. **Start with different types of images**: Try low-contrast, overexposed, and underexposed images
2. **Adjust gamma values**: Experiment with different gamma values (0.5, 1.5, 2.0) to see effects
3. **Compare histograms**: Always visualize histograms before and after enhancement
4. **Preserve color information**: When working with color images, apply enhancement only to intensity/luminance
5. **Handle edge cases**: Check for division by zero in contrast stretching

## Troubleshooting

- **Image path error**: Ensure the image file path is correct and accessible
- **Color space confusion**: Remember OpenCV uses BGR, not RGB (convert using `cv2.cvtColor()`)
- **Normalization issues**: Always normalize pixel values to 0-255 range for proper display
- **Memory issues**: For large images, consider resizing before processing

## References

- OpenCV Documentation: https://docs.opencv.org/
- Image Processing Theory: Digital Image Processing by Gonzalez & Woods
- Histogram Equalization: Understanding intensity distribution transformation
- Gamma Correction: Display and camera calibration techniques

---

**Author**: DIP Task 4 Lab Exercise  
**Date**: 2025  
**Course**: Digital Image Processing (2023-SE-14)
