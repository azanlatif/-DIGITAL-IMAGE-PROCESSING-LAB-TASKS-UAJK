# Task 9: Advanced Color Space Manipulation & Image Analysis
# Submitted By: AZAN LATIF - 2023-SE-14

## Task Overview

This task focuses on **advanced color space transformations and image analysis techniques** using OpenCV, NumPy, and Matplotlib. The objective is to learn how to:

- Extract and analyze individual color channels (R, G, B)
- Convert images between multiple color spaces (RGB, HSV, YCbCr, Lab)
- Implement white balance correction algorithms
- Apply color-based image masking and segmentation
- Compare segmentation effectiveness across different color spaces
- Visualize and analyze color space properties

## Lab Task Prompt

**Prompt:**
```
Write a comprehensive Python program that demonstrates advanced color space manipulation 
and image analysis techniques by:

1. **Load and Prepare Image**: Read a colored image and convert from BGR to RGB for proper display

2. **Extract Color Channels**: Separate the RGB image into individual Red, Green, and Blue channels
   and visualize each channel in grayscale format

3. **Color Space Conversions**: Convert the RGB image to multiple color spaces:
   - HSV (Hue, Saturation, Value)
   - YCbCr (Luminance, Chrominance Blue, Chrominance Red)
   - Lab (Lightness, a-axis, b-axis)
   Display all converted color spaces side by side

4. **White Balance Correction**: Implement the Gray World Algorithm to correct 
   color balance issues:
   - Calculate average intensity for each channel
   - Calculate overall gray average
   - Scale each channel to match the gray average
   - Clip values to valid range [0, 255]

5. **Color Masking in HSV**: Create a mask to extract a specific color range:
   - Define lower and upper bounds for red color in HSV space
   - Apply cv2.inRange() to create a binary mask
   - Apply the mask using cv2.bitwise_and() to extract masked regions
   - Display both the mask and masked result

6. **Comparative Segmentation Analysis**: Compare segmentation effectiveness 
   across different color spaces:
   - Apply binary thresholding to different channels:
     * Red channel from RGB
     * Hue channel from HSV
     * Chrominance channel from YCbCr
   - Display all segmentation results side by side
   - Analyze which color space provides the best segmentation for the given image
```
## What This Task Does

### Step-by-Step Process:

1. **Import Required Libraries**
   - OpenCV (cv2) for image processing operations
   - NumPy for numerical computations and array manipulation
   - Matplotlib for visualization and plotting

2. **Load and Display Image**
   - Reads image file in BGR format (OpenCV default)
   - Converts BGR to RGB for correct color representation
   - Displays original image with title

3. **Extract Color Channels**
   - Separates RGB image into three individual channels: R, G, B
   - Visualizes each channel in grayscale colormap
   - Helps understand color composition of the image

4. **Color Space Conversions**
   - **RGB to HSV**: Converts from RGB (device-dependent) to HSV (human-intuitive)
     * H (Hue): Color information (0-180 in OpenCV)
     * S (Saturation): Color intensity (0-255)
     * V (Value): Brightness (0-255)
   - **RGB to YCbCr**: Converts to television standard
     * Y (Luminance): Overall brightness
     * Cb, Cr (Chrominance): Color information
   - **RGB to Lab**: Converts to perceptually uniform color space
     * L (Lightness): Brightness (0-100)
     * a, b (Color channels): Opponent color dimensions
   - All conversions are displayed for comparison

5. **White Balance Correction (Gray World Algorithm)**
   - Calculates mean intensity for each RGB channel
   - Computes overall gray average: (R + G + B) / 3
   - Scales each channel proportionally to the gray average
   - Corrects color casts and improves overall image color balance
   - Clips pixel values to valid range [0, 255]

6. **Color-Based Masking**
   - Converts image to HSV color space for better color range selection
   - Defines lower and upper bound thresholds for red color in HSV
   - Creates binary mask using cv2.inRange() function
   - Applies mask using bitwise AND operation to extract colored regions
   - Displays both the mask and the resulting masked image

7. **Comparative Segmentation Analysis**
   - Applies binary thresholding to different color space channels
   - **RGB Channel Thresholding**: Uses Red channel with threshold value 120
   - **HSV Channel Thresholding**: Uses Hue channel with threshold value 50
   - **YCbCr Channel Thresholding**: Uses Cb (Chrominance Blue) channel with threshold value 120
   - Compares segmentation quality across color spaces
   - Analyzes which color space best separates objects of interest

## Key Concepts Covered

### Color Spaces Explained

1. **RGB (Red, Green, Blue)**
   - Device-dependent color space
   - Each channel represents intensity (0-255)
   - Intuitive for display but less intuitive for image analysis

2. **HSV (Hue, Saturation, Value)**
   - Hue: Color type (0-180°)
   - Saturation: Color intensity (0-255)
   - Value: Brightness (0-255)
   - **Advantage**: Better for color-based selection and segmentation
   - Color ranges are continuous and intuitive

3. **YCbCr (Luminance, Chrominance)**
   - Y: Luminance (brightness information)
   - Cb, Cr: Chrominance (color information)
   - **Advantage**: Separates brightness from color, useful for compression and analysis

4. **Lab (Perceptually Uniform)**
   - L: Lightness (0-100)
   - a, b: Opponent color channels
   - **Advantage**: Perceptually uniform, consistent distance between colors represents human perception

### Algorithms Implemented

1. **White Balance Correction (Gray World Assumption)**
   - Assumes the average color in the image should be gray
   - Formula: corrected_channel = original_channel × (average_gray / average_channel)
   - Effective for automatic white balance correction

2. **Color Masking (Range-Based Segmentation)**
   - Selects pixels within a specific color range
   - Useful for object detection based on color
   - Creates binary masks for further processing

3. **Binary Thresholding**
   - Separates image into foreground and background
   - Useful for segmentation and object detection
   - Different channels provide different segmentation results

## Implementation Highlights

- **Function Definitions**: Custom white_balance() function for reusable color correction
- **Array Operations**: NumPy for efficient pixel-level operations
- **Color Space Handling**: Proper conversion between BGR (OpenCV), RGB (Display), and other spaces
- **Visualization**: Multiple subplots for comprehensive comparison
- **Analysis**: Comparative study of segmentation effectiveness

## Expected Outcomes

- Understanding of multiple color space representations and their use cases
- Practical knowledge of color space conversions
- Ability to implement white balance correction
- Proficiency in color-based image masking and segmentation
- Comparative analysis skills for evaluating segmentation techniques
- Knowledge of which color spaces work best for specific image analysis tasks

## Prerequisites

- Python 3.x
- OpenCV (cv2)
- NumPy
- Matplotlib
- Sample image file for processing

## Run Instructions

1. Ensure all libraries are installed: `pip install opencv-python numpy matplotlib`
2. Prepare input image and update the image path in the code
3. Run the Jupyter notebook cell by cell
4. Observe outputs and analyze results for each task

---

**Task Type**: Color Space Analysis & Image Manipulation  
**Difficulty Level**: Intermediate to Advanced  
**Key Skills**: Color theory, image processing, algorithm implementation, data visualization
