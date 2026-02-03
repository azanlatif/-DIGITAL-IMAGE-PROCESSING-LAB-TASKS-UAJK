# Digital Image Processing Task 8: Motion Blur Restoration
# Submitted By: AZAN LATIF - 2023-SE-14

## Task Overview

This task focuses on **Image Restoration and Deblurring** - techniques used to recover sharp images from motion-blurred photographs. Students will implement multiple restoration methods and compare their effectiveness in recovering image quality from degradation caused by motion blur.

## Objectives

Students will learn to:
1. Understand motion blur degradation and its characteristics
2. Implement five different image restoration techniques:
   - **Unsharp Masking**: Classical enhancement technique
   - **Deconvolution**: Inverse filtering approach
   - **Bilateral Filtering with Sharpening**: Edge-preserving restoration
   - **Adaptive Sharpening**: Smart enhancement based on local variance
   - **Frequency Domain Filtering**: Wiener-inspired restoration
3. Compare different restoration methods objectively and subjectively
4. Evaluate image quality using sharpness metrics
5. Understand trade-offs between restoration methods
6. Apply practical image restoration in real-world scenarios

## Lab Task Prompt
```
### Problem Statement

**Implement a comprehensive motion blur restoration system that:**

1. **Load and prepare images**:
   - Read motion-blurred images (color and grayscale)
   - Display original blurred image
   - Record image dimensions for reference

2. **Implement Method 1: Unsharp Masking**:
   - Create a Gaussian blurred version of the original image
   - Apply unsharp masking formula: 
     $$\text{Restored} = \text{Original} + \text{amount} \times (\text{Original} - \text{Blurred})$$
   - Use adjustable amount parameter (typical: 1.0-2.0)
   - Clip values to valid pixel range [0, 255]

3. **Implement Method 2: Simple Deconvolution**:
   - Create a motion blur kernel (horizontal or directional)
   - Design inverse kernel for deconvolution
   - Apply filter2D operation with inverse kernel
   - Handle edge effects and boundary conditions

4. **Implement Method 3: Bilateral Filter + Sharpening**:
   - Apply bilateral filtering to preserve edges while reducing noise
   - Create strong sharpening kernel:
     $$K = \begin{bmatrix} -1 & -1 & -1 \\ -1 & 9 & -1 \\ -1 & -1 & -1 \end{bmatrix}$$
   - Combine edge-preserving smoothing with edge enhancement

5. **Implement Method 4: Adaptive Sharpening**:
   - Calculate local variance at each pixel location
   - Use variance map as mask for adaptive enhancement
   - Apply stronger sharpening to low-variance (blurred) regions
   - Apply weaker sharpening to high-variance (already sharp) regions
   - Formula: 
     $$\text{Result} = \text{Variance}_{\text{norm}} \times \text{Sharpened} + (1 - \text{Variance}_{\text{norm}}) \times \text{Original}$$

6. **Implement Method 5: Wiener-inspired Frequency Domain Filtering**:
   - Transform image to frequency domain using FFT
   - Create high-pass filter mask in frequency domain
   - Apply inverse FFT to return to spatial domain
   - Enhance high-frequency components (edges)

7. **Compare all methods**:
   - Display original and all 5 restored versions in a grid
   - Visual comparison of quality and artifacts
   - Identify strengths and weaknesses of each method

8. **Evaluate restoration quality**:
   - Calculate sharpness metric using Laplacian variance
   - Measure improvement percentage
   - Compare before and after metrics

9. **Select best method** and create:
   - Before/After comparison visualization
   - Quality assessment report
   - Result files for download
```
### Expected Deliverables

1. **Working Implementation** of all 5 restoration methods
2. **Visualization outputs**:
   - Original motion-blurred image
   - Restored images from each method
   - Side-by-side comparison grid
   - Before/After comparison for best method
   - Quality metrics report

3. **Quality Metrics**:
   - Original sharpness value
   - Restored sharpness value
   - Improvement percentage
   - Comparison table of all methods

4. **Analysis Report** including:
   - Which method produced best results
   - Artifacts or issues with each method
   - Computational efficiency of each approach
   - Recommendations for practical use
   - When to use each method

5. **Saved Results**:
   - original_blurred.jpg
   - restored_unsharp.jpg
   - restored_bilateral.jpg
   - restored_adaptive.jpg
   - comparison_before_after.jpg

## Key Concepts

### Motion Blur Degradation Model

$$g(x,y) = \int h(x,y,\alpha) \cdot f(x-x_0, y-y_0) \, d\alpha + n(x,y)$$

Where:
- $g(x,y)$ = Blurred image
- $f(x,y)$ = Original sharp image
- $h(x,y,\alpha)$ = Motion blur kernel
- $n(x,y)$ = Additive noise

### Sharpness Metric (Laplacian Variance)

$$\text{Sharpness} = \text{Var}(\nabla^2 I)$$

Where $\nabla^2$ is the Laplacian operator (detects edges).

### Restoration Methods Comparison

| Method | Speed | Quality | Artifacts | Best For |
|--------|-------|---------|-----------|----------|
| Unsharp Masking | Very Fast | Good | Minimal | General purpose |
| Deconvolution | Fast | Moderate | Ringing | Known blur kernel |
| Bilateral + Sharp | Medium | Very Good | Minimal | Preserving edges |
| Adaptive Sharpening | Medium | Excellent | Rare | Variable blur regions |
| Frequency Domain | Slow | Good | Possible | Large blur patterns |

## Implementation Details

### Functions and Operations

1. **Image Loading**: `cv2.imread()`, `cv2.cvtColor()`
2. **Gaussian Blur**: `cv2.GaussianBlur(image, (0,0), sigma)`
3. **Bilateral Filter**: `cv2.bilateralFilter(image, d, sigmaColor, sigmaSpace)`
4. **Convolution**: `cv2.filter2D(image, ddepth, kernel)`
5. **FFT Operations**: `np.fft.fft2()`, `np.fft.fftshift()`, `np.fft.ifft2()`
6. **Quality Metrics**: `cv2.Laplacian()`, variance calculation

### Parameters

| Parameter | Typical Range | Effect |
|-----------|---------------|--------|
| Unsharp amount | 1.0 - 3.0 | Higher = stronger enhancement |
| Gaussian sigma | 1.0 - 5.0 | Higher = more blur (for unsharp) |
| Bilateral d | 5 - 15 | Diameter of pixel neighborhood |
| Bilateral sigmaColor | 50 - 150 | Color similarity threshold |
| Bilateral sigmaSpace | 50 - 150 | Spatial similarity threshold |
| Motion kernel size | 5 - 21 | Length of motion blur direction |
| FFT filter radius | 10 - 50 | Low-pass region size |

## Running the Code

### Prerequisites
```bash
pip install opencv-python numpy matplotlib
```

For Google Colab:
```bash
pip install opencv-python-headless
```

### Execution Steps

1. **Upload image**: Use `files.upload()` for Colab or load from local path
2. **Run all cells**: Execute the notebook sequentially
3. **View results**: 
   - Original blurred image display
   - Individual method results
   - Comparison grid
   - Before/After comparison
   - Quality metrics
4. **Download results**: Save and download restored images

### Input Image Requirements

- **Format**: JPG, PNG, or BMP
- **Size**: Preferably 256x256 to 1024x1024 pixels
- **Content**: Any subject (landscape, people, objects)
- **Blur Type**: Motion blur (horizontal, vertical, or diagonal)

## Expected Results

### Method Performance Ranking (Typical)

1. **Adaptive Sharpening** (Often Best)
   - Best visual quality
   - Minimal artifacts
   - Intelligent enhancement
   - Drawback: Computationally slower

2. **Bilateral Filter + Sharpening**
   - Excellent edge preservation
   - Good restoration quality
   - Low artifact generation

3. **Unsharp Masking**
   - Fast and stable
   - Good for moderate blur
   - Simple implementation
   - May over-sharpen noise

4. **Wiener-inspired Frequency Domain**
   - Good edge enhancement
   - Possible ringing artifacts
   - Better for specific blur patterns

5. **Deconvolution**
   - Moderate results
   - Sensitive to kernel accuracy
   - Can amplify noise

### Quality Metrics Expected

| Method | Sharpness Improvement | Artifacts | Noise Amplification |
|--------|----------------------|-----------|-------------------|
| Unsharp | 30-50% | Low | Medium |
| Deconvolution | 20-40% | Medium | High |
| Bilateral | 40-60% | Very Low | Low |
| Adaptive | 50-70% | Very Low | Very Low |
| FFT | 25-45% | Medium | Medium |

## Analysis Questions to Answer

1. **Which method produced the sharpest result?**
   - Analyze the sharpness metrics
   - Consider visual quality, not just numbers

2. **Which method preserved edges best?**
   - Examine edge detail preservation
   - Look for halo artifacts or over-sharpening

3. **Which method was fastest to compute?**
   - Compare computational complexity
   - Consider practical applicability

4. **How does adaptive sharpening compare to simple unsharp masking?**
   - Analyze variance-based approach
   - Discuss benefits of adaptive methods

5. **When would you recommend each method?**
   - Consider blur characteristics
   - Think about noise levels
   - Evaluate application requirements

6. **What artifacts did you observe?**
   - Ringing effects
   - Noise amplification
   - Color shifts (if using color images)
   - Halo effects around edges

7. **How would you improve the worst-performing method?**
   - Parameter tuning
   - Hybrid approaches
   - Pre/post-processing

8. **How does motion blur differ from other types of blur?**
   - Directional vs isotropic
   - Recovery feasibility
   - Kernel identification challenges

## Common Issues and Solutions

| Issue | Cause | Solution |
|-------|-------|----------|
| Black/Dark output | Clipping not applied | Add `np.clip(result, 0, 255)` |
| Over-sharpened noise | Amount too high | Reduce unsharp amount |
| Ringing artifacts | Deconvolution artifacts | Use bilateral or adaptive methods |
| Loss of detail | Bilateral filter too strong | Reduce bilateral sigma values |
| Slow execution | FFT on large images | Downsampling or optimize kernel |
| Color shifts | Color/grayscale mismatch | Process channels separately if needed |

## Enhancement Ideas

1. **Multi-scale Restoration**: Apply methods at different image scales
2. **Hybrid Approach**: Combine best aspects of multiple methods
3. **Motion Direction Detection**: Estimate blur kernel from image
4. **Noise Handling**: Pre-filter noise before restoration
5. **GPU Acceleration**: Use CUDA for large images
6. **Blind Deconvolution**: Estimate blur kernel and restore simultaneously
7. **Deep Learning**: Train neural networks for restoration

## References

- Gonzalez & Woods: "Digital Image Processing" (Image Restoration chapter)
- OpenCV Documentation: Filters and transformations
- "Image Restoration by Deconvolution" research papers
- NumPy FFT documentation
- "Bilateral Filtering for Gray and Color Images" (Tomasi & Manduchi)

## Notes

- **Unsharp Masking** is the most practical for real-world use (fast, stable)
- **Adaptive Sharpening** provides best quality but requires more computation
- **Bilateral filtering** excels at edge preservation without over-sharpening
- **Frequency domain** methods work best with known blur characteristics
- Image quality depends heavily on blur severity and noise levels
- Richardson-Lucy deconvolution may diverge with real noisy images
- Multi-method averaging can sometimes produce best results

## Practical Applications

- **Photography**: Correcting camera shake blur
- **Medical Imaging**: Enhancing blurred medical images
- **Surveillance**: Improving security footage quality
- **Astronomy**: Deblurring telescope images
- **Microscopy**: Enhancing microscope images
- **Document Scanning**: Improving scanned document clarity

---

**Task Version**: 2023-SE-14-DIP-TASK-08  
**Subject**: Digital Image Processing  
**Topic**: Image Restoration and Deblurring  
**Difficulty Level**: Advanced  
**Focus**: Practical restoration techniques and comparative analysis
