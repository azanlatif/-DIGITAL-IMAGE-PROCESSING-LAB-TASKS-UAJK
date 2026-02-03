# Task 5: Image Filtering - Mean, Median, Mode, and Gaussian Filters
# Submitted By: AZAN LATIF - 2023-SE-14

## Task Overview

This task demonstrates the application of various image smoothing and noise reduction filters to a digital image. The objective is to apply multiple filtering techniques to an image and visually compare the effects of each filter on image quality and characteristics.

## Lab Prompt
```
**Objective:** Apply mean, median, mode, and Gaussian filters to the image located at `/content/img5.jpg` and display the original along with all filtered versions for comparison.

**What You Need to Do:**
1. Load an image from the specified path
2. Apply four different types of filters to the image:
   - **Mean Filter (BoxBlur):** Smooths the image by averaging pixel values in a neighborhood
   - **Median Filter:** Removes salt-and-pepper noise while preserving edges
   - **Mode Filter:** Replaces each pixel with the most frequent value in its neighborhood
   - **Gaussian Filter:** Applies Gaussian blur for smooth, natural-looking noise reduction
3. Display the original image alongside all filtered versions for comparative analysis
4. Analyze and document the effects of each filter on the image
```
## Implementation Details

### Filters Applied

1. **Mean Filter (BoxBlur with radius 3)**
   - Creates a smoothed version by averaging neighboring pixels
   - Effective for general noise reduction
   - May blur edges

2. **Median Filter (Size 3)**
   - Excellent for removing salt-and-pepper noise
   - Better edge preservation compared to mean filter
   - Uses the median value in the neighborhood

3. **Mode Filter (Size 3)**
   - Replaces pixels with the most frequent value in the neighborhood
   - Useful for specific noise reduction scenarios
   - Can create posterization effects

4. **Gaussian Filter (Radius 2)**
   - Uses Gaussian function for smooth blurring
   - Natural-looking results
   - Effective for Gaussian noise reduction

### Output

The notebook generates a comparative visualization displaying:
- Original image (unfiltered)
- Mean filtered image
- Median filtered image
- Mode filtered image
- Gaussian filtered image

All images are displayed side-by-side in a 2x3 grid layout for easy comparison.

## Key Findings

- **Different filters excel at different tasks:** Each filter produces distinct effects on the image
- **Noise reduction varies:** The median filter is particularly effective for salt-and-pepper noise, while Gaussian filter provides smooth, general-purpose smoothing
- **Edge preservation:** Median and mode filters generally preserve edges better than mean filters
- **Visual quality:** Gaussian filtering typically produces the most natural-looking results for general smoothing

## How to Run This Task

1. Ensure you have the required libraries installed:
   ```bash
   pip install pillow matplotlib
   ```

2. Load the image and view it:
   - Run the first code cell to load and display the original image
   
3. Apply individual filters:
   - Run cells 2-5 to see the effects of each filter individually compared to the original

4. View all filters together:
   - Run the final cell to see all filtered versions in a single comparative display

## Notes

- The image path is set to `/content/img5.jpg`. Adjust this path if your image is located elsewhere
- Filter parameters (radius, size) can be modified to achieve different levels of smoothing
- The combination of multiple filters can be used for more sophisticated image processing tasks

## File Structure

- `2023-SE-14-DIP-TASK-05.ipynb` - Main notebook with all filter implementations and visualizations
- `README.md` - This documentation file

## References

- PIL (Pillow) ImageFilter documentation
- Image Processing concepts: Spatial filtering, kernel-based operations
- Matplotlib for image visualization
