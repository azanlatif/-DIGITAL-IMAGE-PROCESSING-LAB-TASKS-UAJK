# Task 3: Display RGB Components, Grayscale, and Binary Image
# Submitted By: AZAN LATIF - 2023-SE-14

## Objective

This task demonstrates fundamental image processing techniques using OpenCV and Matplotlib. The objective is to:

- Read a colored image and display its **Red**, **Green**, and **Blue** components separately
- Convert the image into **Grayscale** format
- Convert the Grayscale image into a **Binary** image using thresholding
- Visualize all results in a single figure with subplots

## Input Image

**Filename:** `Coin.jpg`

## Steps Involved

1. **Read the Image**: Load the image using OpenCV's `cv2.imread()` function
2. **Convert Color Space**: Convert from BGR (OpenCV's default) to RGB for correct color display
3. **Split RGB Channels**: Separate the image into individual Red, Green, and Blue components using `cv2.split()`
4. **Convert to Grayscale**: Transform the image to grayscale using `cv2.cvtColor()` with `COLOR_BGR2GRAY`
5. **Apply Thresholding**: Convert the grayscale image to binary using `cv2.threshold()` with threshold value of 127
6. **Display Results**: Create a visualization with 6 subplots showing:
   - Original RGB Image
   - Red Component (with 'Reds' colormap)
   - Green Component (with 'Greens' colormap)
   - Blue Component (with 'Blues' colormap)
   - Grayscale Image (with 'gray' colormap)
   - Binary Image (with 'gray' colormap)

## Implementation Details

### Libraries Used
- **OpenCV (cv2)**: For image reading and processing operations
- **Matplotlib**: For visualization and display

### Key Operations

| Operation | Function | Purpose |
|-----------|----------|---------|
| Read Image | `cv2.imread('Coin.jpg')` | Load the image file |
| Color Conversion | `cv2.cvtColor(img, cv2.COLOR_BGR2RGB)` | Convert BGR to RGB |
| Split Channels | `cv2.split(img_rgb)` | Separate into R, G, B components |
| Grayscale | `cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)` | Convert to grayscale |
| Thresholding | `cv2.threshold(gray, 127, 255, cv2.THRESH_BINARY)` | Create binary image |

## Expected Output

The program displays a 2×3 grid of images showing the original image and its various transformations, allowing visualization of how different color spaces and processing techniques affect the image representation.

## Lab Task Prompt
```
**Complete the following image processing task:**

1. Load the image `Coin.jpg` using OpenCV
2. Extract and display the individual RGB channels as separate grayscale images
3. Demonstrate color space conversion by converting the RGB image to grayscale
4. Apply binary thresholding to the grayscale image using a threshold value of 127
5. Create a comprehensive visualization showing all six images (original RGB, R channel, G channel, B channel, grayscale, and binary)
6. Ensure proper image formatting and labeling for clarity
7. Use appropriate colormaps for visual distinction between different components
```
---

**Note:** Ensure that the `Coin.jpg` file is in the same directory as the notebook before running the code.
