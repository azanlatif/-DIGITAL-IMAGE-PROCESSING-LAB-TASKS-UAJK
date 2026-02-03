# LAB 11 – MORPHOLOGICAL OPERATIONS (Python – Colab)
# Submitted By: AZAN LATIF - 2023-SE-14

## Task Objective

This laboratory task focuses on **Morphological Operations**, a fundamental image processing technique used to extract meaningful information from binary images. Morphological operations are used to simplify images, identify shapes, remove noise, fill holes, and perform boundary detection.

## What is This Task About?

Morphological operations are techniques that process images based on their shape. These operations work on binary images and use a **structuring element** (kernel) to probe and extract information from the image. The two fundamental operations are:

- **Erosion**: Removes pixels from object boundaries, shrinking white regions
- **Dilation**: Adds pixels to object boundaries, expanding white regions

These basic operations combine to create more advanced operations like Opening, Closing, Boundary Extraction, and Hole Filling.

## Learning Objectives

By completing this task, you will:
1. Understand the theory behind morphological operations
2. Learn how to apply erosion and dilation to binary images
3. Implement advanced morphological techniques (Opening, Closing)
4. Perform boundary extraction on image objects
5. Fill holes in binary images using morphological reconstruction
6. Remove noise from images using morphological filtering
7. Detect specific shapes using structuring elements

## Lab Procedure & Requirements

### Step 1: Install & Import Libraries
Install required libraries and import:
- **OpenCV (cv2)**: For image processing operations
- **NumPy (numpy)**: For numerical computations
- **Matplotlib (matplotlib.pyplot)**: For image visualization

### Step 2: Load Image
- Read an image file (JPEG, PNG, etc.)
- Convert to grayscale
- Convert to binary image using thresholding (127 threshold value with binary method)
- Display the original binary image

### Step 3: Create Structuring Element
- Define a kernel/structuring element (typically 3×3 with all ones)
- This element is used for all morphological operations

### Step 4: Implement Morphological Operations

#### 4.1 Erosion
- Apply erosion using `cv2.erode()`
- Erosion removes boundary pixels from white objects
- Useful for separating touching objects
- Display the eroded image with title "Erosion"

#### 4.2 Dilation
- Apply dilation using `cv2.dilate()`
- Dilation adds pixels to object boundaries
- Useful for filling small holes and connecting nearby objects
- Display the dilated image with title "Dilation"

#### 4.3 Opening
- Apply opening using `cv2.morphologyEx(binary, cv2.MORPH_OPEN, kernel)`
- Opening = Erosion followed by Dilation
- Removes small white noise while preserving object shape
- Display with title "Opening"

#### 4.4 Closing
- Apply closing using `cv2.morphologyEx(binary, cv2.MORPH_CLOSE, kernel)`
- Closing = Dilation followed by Erosion
- Fills small holes in objects while preserving object size
- Display with title "Closing"

### Step 5: Advanced Morphological Applications

#### 5.1 Boundary Extraction
- Extract object boundaries using: `boundary = binary - erosion`
- Shows only the outline of objects
- Display with title "Boundary Extraction"

#### 5.2 Fill Holes using Reconstruction
- Apply closing operation multiple times (iterations=3)
- Fills holes and gaps in binary objects
- Display with title "Hole Filled Image"

#### 5.3 Remove Noise using Morphology
- Combine Opening and Closing operations
- Opening removes small white noise
- Closing fills small black holes
- Display with title "Noise Removed Image"

#### 5.4 Detect Specific Shapes
- Create a larger structuring element using `cv2.getStructuringElement(cv2.MORPH_RECT, (15,15))`
- Apply erosion with this larger kernel
- Helps detect/isolate specific shape sizes
- Display with title "Detected Shape"

## Expected Output

Your notebook should produce:
1. Original binary image visualization
2. Erosion result
3. Dilation result
4. Opening result
5. Closing result
6. Boundary extraction result
7. Hole-filled image
8. Noise-removed image
9. Detected shapes image

All visualizations should be displayed using Matplotlib with appropriate titles and no axes.

## Key Concepts to Understand

| Operation | What It Does | Use Case |
|-----------|-------------|----------|
| **Erosion** | Shrinks white objects | Separating connected objects |
| **Dilation** | Expands white objects | Filling small holes, connecting gaps |
| **Opening** | Erosion + Dilation | Remove small noise |
| **Closing** | Dilation + Erosion | Fill small holes |
| **Boundary** | Object edges only | Edge detection, object outline |

## Tips for Success

- Use grayscale images for morphological operations
- Always convert to binary before applying operations
- Experiment with different kernel sizes
- Increase iterations for stronger effects
- Use `plt.axis('off')` to hide axes for cleaner visualizations
- Use `cmap='gray'` for displaying binary images

## Submission Requirements

- Complete all steps as outlined in the procedure
- Ensure all visualizations are properly labeled with titles
- Add comments explaining each operation
- Test with at least one image file
- Verify all cells execute without errors
- Save the notebook with `.ipynb` format

---

**Note**: This lab can be run in Google Colab or local Jupyter environment. If using Colab, upload your image file first using the file upload feature.
