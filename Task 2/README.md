# Task 2: Image Processing - Color Channel Separation & Connected Components Labeling
# Submitted By: AZAN LATIF - 2023-SE-14

## Task Overview

This task focuses on **fundamental image processing operations** using OpenCV and Python. It demonstrates how to:

1. **Load and display images** using OpenCV
2. **Separate color channels** (Red, Green, Blue) from a colored image
3. **Convert color space** from RGB to Grayscale
4. **Apply binary thresholding** to create binary images
5. **Detect connected components** in binary images
6. **Label and visualize** connected components with random colors

## Objectives

- Understand color space representations (BGR vs RGB)
- Learn how to manipulate individual color channels
- Convert images between different color spaces (RGB, Grayscale, Binary)
- Apply thresholding techniques for image segmentation
- Implement connected component labeling for object detection
- Visualize and analyze multiple image transformations

## Key Concepts Covered

### 1. **Color Channel Separation**
   - Extract individual R, G, B channels from a colored image
   - Visualize each channel independently
   - Understand how colors are composed from individual channels

### 2. **Color Space Conversion**
   - BGR to RGB conversion (OpenCV default is BGR)
   - RGB to Grayscale conversion using weighted averaging
   - Importance of proper color space handling

### 3. **Image Thresholding**
   - Convert grayscale images to binary (black and white only)
   - Use threshold value (127) to create binary classification
   - Binary images are essential for object detection

### 4. **Connected Components Labeling**
   - Detect separate objects/regions in binary images
   - Label each connected region with a unique identifier
   - Count total number of objects in an image
   - Visualize each component with random colors for easy identification

## Implementation Steps

### Step 1: Load and Display Original Image
```python
img = cv2.imread("/content/dip.jpeg")
img = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
plt.imshow(img)
```

### Step 2: Extract Individual Color Channels
- Red Component: Keep R channel, set G=0, B=0
- Green Component: Keep G channel, set R=0, B=0
- Blue Component: Keep B channel, set R=0, G=0

### Step 3: Convert to Grayscale
```python
gray = cv2.cvtColor(img, cv2.COLOR_RGB2GRAY)
```

### Step 4: Apply Binary Thresholding
```python
ret, binary = cv2.threshold(gray, 127, 255, cv2.THRESH_BINARY)
```

### Step 5: Detect Connected Components
```python
num_labels, labels = cv2.connectedComponents(binary)
```

### Step 6: Visualize Components with Random Colors
```python
for label in range(1, num_labels):
    label_colored[labels == label] = np.random.rand(3)
```

## Required Libraries

- **OpenCV** (`cv2`): Image processing operations
- **Matplotlib** (`matplotlib.pyplot`): Image visualization
- **NumPy** (`numpy`): Numerical operations and array manipulation

## Input Requirements

- Image file path: `/content/dip.jpeg`
- Image should be a standard image format (JPEG, PNG, etc.)

## Expected Output

1. Original colored image
2. Red component image
3. Green component image
4. Blue component image
5. Grayscale image
6. Binary image
7. Connected components labeled image with unique colors for each object

## Lab Task Prompt (As Given)

**Prompt:** 
> "Perform image processing operations including color channel separation, color space conversion, binary thresholding, and connected component labeling to detect and visualize individual objects within an image."

**Detailed Lab Requirements:**
1. Load an image from the provided path
2. Separate and visualize individual RGB color channels
3. Convert the image to grayscale
4. Apply binary thresholding with an appropriate threshold value (127)
5. Use connected component labeling to detect separate objects
6. Count the total number of objects detected
7. Create a visualization where each connected component is displayed with a distinct color
8. Ensure all visualizations have appropriate titles and labels

## Expected Outcomes

- Understanding of how color channels work in digital images
- Knowledge of color space conversions
- Ability to apply thresholding for image segmentation
- Skills in connected component analysis for object detection
- Practical experience with OpenCV and image visualization

## Running the Notebook

1. Open the notebook file: `2023-SE-14-DIP-TASK-02.ipynb`
2. Ensure the image file path is correctly set to your image location
3. Run each cell sequentially from top to bottom
4. Observe the output visualizations for each step

## Notes

- The `cv2.imread()` function reads images in BGR format by default, not RGB
- The `cv2.connectedComponents()` function detects connected regions in binary images
- Label 0 represents the background (black pixels), so iteration starts from label 1
- Random colors are used to make each component visually distinct

## Troubleshooting

- **Image not found error**: Verify the image file path is correct
- **Empty output**: Ensure the image contains distinct objects with good contrast
- **Poor connected component detection**: Adjust the threshold value (127) to better separate foreground and background

---

**Course:** Digital Image Processing (DIP)  
**Task:** Task 2 - Color Channel Separation & Connected Components Labeling  
**Date:** 2026
