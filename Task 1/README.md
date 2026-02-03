# Digital Image Processing - Task 1: Image Color Space Manipulation
# Submitted By: AZAN LATIF - 2023-SE-14

## Task Overview

This task focuses on fundamental image processing operations using OpenCV and Matplotlib. The objective is to learn how to:
- Load and read images using OpenCV
- Convert between different color spaces (BGR to RGB, Grayscale, Binary)
- Split images into individual color channels
- Apply image thresholding techniques
- Visualize multiple image transformations simultaneously

## Lab Task Prompt

**Prompt:** 
```
>Write a Python program that demonstrates comprehensive image manipulation techniques by:

1. **Load an Image**: Read a colored image file (coins.jpeg) using OpenCV
2. **Color Space Conversion**: Convert the image from BGR (OpenCV default) to RGB for proper display
3. **Channel Separation**: Split the image into individual Red, Green, and Blue color components
4. **Grayscale Conversion**: Convert the original image to grayscale format
5. **Binary Thresholding**: Apply binary thresholding to create a black-and-white image using a threshold value of 127
6. **Visualization**: Display all transformed images in a 2×3 subplot grid showing:
   - Row 1: Original Image (RGB), Red Component, Green Component
   - Row 2: Blue Component, Grayscale Image, Binary Image
```
## What This Task Does

### Step-by-Step Process:

1. **Import Libraries**
   - OpenCV (cv2) for image processing
   - Matplotlib for visualization

2. **Image Loading**
   - Reads the coins.jpeg image file
   - Includes error handling to check if the image loaded successfully

3. **Color Space Conversions**
   - BGR → RGB: Corrects color channel ordering for proper display
   - BGR → Grayscale: Converts to single-channel 8-bit image

4. **Channel Separation**
   - Splits RGB image into three separate channels
   - Each channel is visualized with an appropriate colormap

5. **Binary Thresholding**
   - Applies threshold value of 127 to grayscale image
   - Creates binary (black and white) image for segmentation tasks

6. **Visualization**
   - Creates a figure with 2×3 subplots
   - Displays all transformations for comparison and analysis

## Expected Output

A figure displaying 6 images in a grid layout:
- **Position 1,1**: Original colored coins image
- **Position 1,2**: Red channel visualization
- **Position 1,3**: Green channel visualization
- **Position 2,1**: Blue channel visualization
- **Position 2,2**: Grayscale version
- **Position 2,3**: Binary (thresholded) version

## Key Concepts Learned

- **Color Spaces**: Understanding BGR, RGB, and Grayscale formats
- **Channel Operations**: Decomposing and analyzing individual color channels
- **Image Thresholding**: Creating binary images for segmentation
- **Image Visualization**: Using Matplotlib for multi-image display
- **OpenCV Fundamentals**: Image I/O, color conversion, and basic processing

## How to Run

1. Ensure you have OpenCV and Matplotlib installed:
   ```bash
   pip install opencv-python matplotlib
   ```

2. Place the `coins.jpeg` image in the `/content/` directory (or update the file path in the code)

3. Open the Jupyter notebook and run all cells sequentially

4. The final cell will display the comparison visualization

## Prerequisites

- Python 3.x
- OpenCV (cv2)
- Matplotlib (pyplot)
- Sample image file (coins.jpeg)

## Notes

- The threshold value of 127 is the midpoint of the 8-bit grayscale range (0-255)
- Different threshold values can produce different binary image results
- The colormap applied to individual channels helps visualize their intensity distribution
