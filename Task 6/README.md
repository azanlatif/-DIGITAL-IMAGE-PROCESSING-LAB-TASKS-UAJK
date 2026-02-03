# Task 6: Frequency Domain Analysis and Filtering
# Submitted By: AZAN LATIF - 2023-SE-14

## Task Overview

This task focuses on **Digital Image Processing (DIP)** in the **frequency domain** using **Fourier Transform**. The objective is to understand and implement frequency domain filtering techniques to analyze and manipulate images.

## What This Task Does

This Jupyter Notebook implements the following key concepts:

### 1. **Fourier Transform (FFT) - Fast Fourier Transform**
   - Converts images from the spatial domain to the frequency domain
   - Uses `np.fft.fft2()` to compute the 2D Discrete Fourier Transform
   - Shifts zero frequency components to the center using `np.fft.fftshift()`

### 2. **Magnitude and Phase Spectra**
   - **Magnitude Spectrum**: Represents the strength of different frequency components
   - **Phase Spectrum**: Represents the phase information of frequency components
   - Both are visualized using logarithmic scaling for better visualization

### 3. **Low-Pass Filtering**
   - Creates a circular mask centered at the frequency origin
   - Preserves low-frequency components (blurs the image)
   - Removes high-frequency details and noise

### 4. **High-Pass Filtering**
   - Creates the complement of the low-pass filter mask
   - Preserves high-frequency components (edge detection)
   - Removes low-frequency information

### 5. **Inverse FFT (IFFT)**
   - Converts filtered frequency domain data back to spatial domain
   - Obtains the resulting filtered images
   - Uses `np.fft.ifftshift()` and `np.fft.ifft2()` to reverse the transformation

## Implementation Details

### Libraries Used
- **NumPy**: Numerical operations and FFT computations
- **OpenCV (cv2)**: Image loading and manipulation
- **Matplotlib**: Image visualization

### Processing Steps (for each image)

1. **Load Image**: Read grayscale images using OpenCV
2. **Apply FFT**: Transform image to frequency domain
3. **Compute Spectra**: Calculate magnitude and phase spectra
4. **Create Masks**: Define circular low-pass and high-pass filter masks
5. **Apply Filters**: Multiply FFT with masks
6. **Inverse Transform**: Convert back to spatial domain
7. **Visualize Results**: Display original, low-pass, and high-pass filtered images

### Test Images
- **Image 1**: `/Dip_Tasks/cat.jpg`
- **Image 2**: `/Dip_Tasks/building.jpg`

## Lab Task Prompt
```
### **Original Prompt:**
"Implement frequency domain filtering using Fourier Transform to demonstrate the difference between low-pass and high-pass filtering on grayscale images. Show the magnitude and phase spectra, and apply circular filters to separate low and high-frequency components."
```
### **Detailed Requirements:**

1. **Load and Display Images**
   - Load grayscale images using OpenCV
   - Display original images

2. **Compute 2D FFT**
   - Apply Fast Fourier Transform to the images
   - Shift zero frequency to the center
   - Display both magnitude and phase spectra with proper scaling

3. **Design Frequency Domain Filters**
   - Create a circular low-pass filter with adjustable radius (currently set to r=30)
   - Generate corresponding high-pass filter (complement of low-pass)

4. **Apply Filters and IFFT**
   - Apply filters to the FFT coefficients
   - Apply inverse FFT to obtain filtered images
   - Take absolute values to get magnitudes

5. **Visualization**
   - Display low-frequency components (blurred images)
   - Display high-frequency components (edge-enhanced images)
   - Compare results side-by-side with original images

## Expected Outputs

1. Original grayscale image
2. Magnitude spectrum (log-scaled)
3. Phase spectrum
4. Low-pass filtered image (smooth, blurred)
5. High-pass filtered image (edges, details highlighted)
6. Comparison of original vs. filtered results for both test images

## Key Concepts Learned

- **Frequency Domain Analysis**: Understanding how images are represented in frequency space
- **Fourier Properties**: Zero frequency (DC component), low frequencies (smooth areas), high frequencies (edges and details)
- **Filter Design**: Creating spatial frequency filters using circular masks
- **Image Enhancement**: Using frequency domain techniques for filtering and enhancement
- **Dual Representation**: Converting between spatial and frequency domains

## Usage Instructions

1. Ensure required images are available at `/Dip_Tasks/cat.jpg` and `/Dip_Tasks/building.jpg`
2. Run all cells sequentially to see the progressive steps of FFT analysis and filtering
3. Modify the filter radius (r parameter) to observe the effects on filtering
4. Observe how different frequencies contribute to image structure

## Learning Outcomes

After completing this task, you will understand:
- How to apply Fourier Transform to images
- How to interpret magnitude and phase spectra
- How frequency domain filters affect image appearance
- The relationship between frequency components and image features
- How to implement and visualize frequency domain operations in Python
