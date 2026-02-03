# Digital Image Processing Task 7: Frequency Domain Filtering
# Submitted By: AZAN LATIF - 2023-SE-14

## Task Overview

This task focuses on **Frequency Domain Image Filtering** - a fundamental technique in Digital Image Processing (DIP) where images are transformed from the spatial domain to the frequency domain using Fourier Transform, filtered using various filter masks, and then transformed back to the spatial domain.

## Objectives

Students will learn to:
1. Compute the 2D Fourier Transform of images
2. Design and implement different types of filters in the frequency domain:
   - **Low Pass Filters (LPF)**: Smoothing and blurring effects
   - **High Pass Filters (HPF)**: Edge detection and sharpening effects
3. Apply three popular filter types:
   - **Ideal Filters**: Sharp frequency cutoff (theoretical)
   - **Butterworth Filters**: Smooth transition (practical alternative)
   - **Gaussian Filters**: Smooth, natural rolloff
4. Compare frequency domain filtering with spatial domain filtering
5. Understand the advantages and disadvantages of each filtering approach

## Lab Task Prompt
```
### Problem Statement

**Implement a comprehensive frequency domain filtering system that:**

1. **Load and prepare images**: Read images in grayscale format for processing
2. **Implement FFT operations**:
   - Compute 2D Fourier Transform using FFT
   - Apply proper shifting (fftshift) for centered frequency components
   - Perform Inverse FFT to convert back to spatial domain

3. **Design three types of Low Pass Filters (LPF)**:
   - **Ideal LPF**: Create a circular mask with sharp cutoff at radius = cutoff frequency
     - Formula: H(u,v) = 1 if D(u,v) ≤ D₀, else 0
   - **Butterworth LPF**: Create a smooth filter with adjustable order
     - Formula: H(u,v) = 1 / (1 + (D(u,v)/D₀)^(2n))
   - **Gaussian LPF**: Create a Gaussian-shaped filter
     - Formula: H(u,v) = exp(-(D(u,v)²) / (2D₀²))

4. **Design three types of High Pass Filters (HPF)**:
   - Create HPF versions by taking the complement of each LPF (H_HPF = 1 - H_LPF)
   - HPFs enhance edges and high-frequency components

5. **Apply filters and visualize results**:
   - Apply each filter type to test images
   - Display original and filtered images
   - Compare the visual effects and observe ringing artifacts

6. **Comparison Analysis**:
   - Compare frequency domain filtering with spatial domain Gaussian blur
   - Discuss advantages and limitations of each approach
```
### Expected Deliverables

1. Working implementation of all filter types
2. Clear visualization of:
   - Original grayscale image
   - Ideal LPF result
   - Butterworth LPF result
   - Gaussian LPF result
   - Ideal HPF result
   - Butterworth HPF result
   - Gaussian HPF result
   - Spatial Gaussian blur comparison

3. Observations about:
   - Filter behavior and visual quality
   - Ringing artifacts in Ideal filters
   - Smooth transitions in Butterworth filters
   - Natural appearance of Gaussian filters
   - Trade-offs between frequency and spatial domain approaches

## Key Concepts

### Frequency Domain Filtering Steps

```
Spatial Image → FFT → Frequency Domain → Apply Filter Mask → 
Inverse FFT → Filtered Spatial Image
```

### Distance Function
For each point (u,v) in frequency domain, the distance from center is:
$$D(u,v) = \sqrt{(u - u_c)^2 + (v - v_c)^2}$$

Where (u_c, v_c) is the center of the frequency spectrum.

### Filter Parameters
- **Cutoff Frequency (D₀)**: Controls the frequency at which filtering occurs
- **Order (n)**: For Butterworth filters, controls the steepness of the transition
- **Kernel Size**: For spatial filters, defines the neighborhood for processing

## Implementation Details

### Functions Implemented

1. **load_image(image_path)**: Loads image as grayscale
2. **compute_fft(image)**: Computes centered 2D Fourier Transform
3. **create_lpf_ideal(shape, cutoff)**: Creates Ideal LPF mask
4. **create_lpf_butterworth(shape, cutoff, order)**: Creates Butterworth LPF mask
5. **create_lpf_gaussian(shape, cutoff)**: Creates Gaussian LPF mask
6. **create_hpf_ideal(shape, cutoff)**: Creates Ideal HPF mask
7. **create_hpf_butterworth(shape, cutoff, order)**: Creates Butterworth HPF mask
8. **create_hpf_gaussian(shape, cutoff)**: Creates Gaussian HPF mask
9. **apply_filter(image, filter_mask)**: Applies filter and returns filtered image
10. **display_image(image, title)**: Displays image with title

### Parameters to Experiment With

- **Cutoff Value**: Typically 30-100 pixels depending on image size
  - Smaller values: More aggressive filtering (more blurring for LPF)
  - Larger values: Less aggressive filtering (more detail retained for LPF)
- **Butterworth Order**: Typically 1-4
  - Order 1: Smooth transition
  - Order 4+: Sharper transition (closer to ideal)

## Running the Code

### Prerequisites
```bash
pip install numpy opencv-python matplotlib
```

### Execution
1. Replace image paths with your test images (or use available images)
2. Adjust `cutoff_value` parameter (default: 60)
3. Run each cell in the notebook to see results
4. Observe the visual differences between filter types

### Typical Test Images
- Simple patterns (circles, rectangles)
- Natural images (cat, building, landscape)
- High-frequency images (texture, patterns)

## Expected Results

### Low Pass Filters
- **Ideal LPF**: Smooth image with visible ringing artifacts (Gibbs phenomenon)
- **Butterworth LPF**: Smooth image with slight ringing, more natural than ideal
- **Gaussian LPF**: Smooth image with minimal ringing, most natural appearance

### High Pass Filters
- **Ideal HPF**: Edge enhancement with ringing artifacts
- **Butterworth HPF**: Edge enhancement with less ringing
- **Gaussian HPF**: Edge enhancement with smooth gradients

## Analysis Questions to Answer

1. Which filter type produces the smoothest results for LPF?
2. Which filter shows the most ringing artifacts?
3. How does the cutoff frequency affect the filtering result?
4. What is the advantage of Butterworth over Ideal filters?
5. How does frequency domain filtering compare to spatial domain filtering?
6. Why does Gaussian filtering produce the most natural results?

## Common Issues and Solutions

| Issue | Solution |
|-------|----------|
| Black/Dark output images | Check FFT normalization; ensure inverse FFT uses absolute values |
| Ringing artifacts too severe | Use Butterworth or Gaussian filters instead of Ideal |
| Image appears unchanged | Increase cutoff value (you're filtering too aggressively at too high frequency) |
| Memory errors with large images | Consider downsampling or using smaller test images |

## References

- Gonzalez & Woods: "Digital Image Processing" (Frequency Domain)
- OpenCV Documentation: FFT and filtering operations
- NumPy FFT: https://numpy.org/doc/stable/reference/fft.html

## Notes

- All filters work in the frequency domain for efficiency
- The `fftshift` operation centers the DC component for visualization
- The `ifftshift` operation reverses the shift before inverse FFT
- Results are converted to absolute values to get magnitude information
- This approach is more efficient than spatial filtering for large kernels

---

**Task Version**: 2023-SE-14-DIP-TASK-07  
**Subject**: Digital Image Processing  
**Topic**: Frequency Domain Filtering  
**Difficulty Level**: Intermediate
