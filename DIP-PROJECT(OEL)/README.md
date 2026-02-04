# Automated Melanoma Detection System - Digital Image Processing Project

## Project Overview

This project develops an **automated system for melanoma detection** from dermoscopic images using digital image processing and machine learning techniques. The system processes dermoscopic images through a comprehensive pipeline including image enhancement, lesion segmentation, feature extraction, and classification to distinguish between benign lesions and melanoma.

---

## Project Information

- **Submitted By:** AZAN LATIF
- **Roll No:** 2023-SE-14
- **Project Type:** Digital Image Processing (Phase 2)
- **Dataset:** PH2 Dataset (Dermatology Images)

---

## Project Pipeline Overview

The automated melanoma detection system is organized into four main stages:

### **Stage 1: Lesion Segmentation & Mask Generation**

This initial phase preprocesses dermoscopic images to isolate the lesion area from surrounding skin.

#### Key Operations:

1. **Image Enhancement**
   - Uses **CLAHE (Contrast Limited Adaptive Histogram Equalization)** to improve image contrast
   - Enhances visibility of lesion boundaries
   - Operates on the L-channel of LAB color space for better results

2. **Hair Removal**
   - Applies **black-hat morphological transform** to detect hair artifacts
   - Uses binary thresholding to create a hair mask
   - Applies **Telea inpainting algorithm** to remove hair while preserving lesion structure
   - Parameters: 17×17 morphological kernel

3. **Lesion Segmentation**
   - Converts image to grayscale and applies Gaussian blur (5×5)
   - Uses **Otsu's automatic thresholding** for optimal binarization
   - Applies **morphological closing** (7×7 elliptical kernel) to connect boundaries
   - Implements **flood-fill algorithm** to remove small holes and fill gaps
   - Generates binary mask distinguishing lesion from surrounding skin

**Output:** Binary segmentation masks for each dermoscopic image

---

### **Stage 2: Feature Extraction**

Once lesions are segmented, quantitative features are extracted from masked regions to characterize lesion properties.

#### Extracted Features:

For each image, 6 features are extracted (2 per color channel):
- **Blue Channel:** Mean and Standard Deviation
- **Green Channel:** Mean and Standard Deviation
- **Red Channel:** Mean and Standard Deviation

These color statistics capture the characteristic color distribution of lesions, which is a key discriminator between benign and malignant lesions.

**Feature Vector:** 6-dimensional feature space per image

---

### **Stage 3: Classification**

Machine learning classification distinguishes between benign and melanoma lesions based on extracted features.

#### Classifier: Random Forest

**Configuration:**
- Number of estimators: 50 decision trees
- Maximum tree depth: 5 (controls model complexity)
- Minimum samples per split: 5
- Random state: 42 (reproducibility)

**Training Approach:**
- 80% training data, 20% test data split
- Stratified sampling to preserve class distribution
- Binary classification: 0 = Benign, 1 = Melanoma

---

### **Stage 4: Evaluation**

Both segmentation and classification stages are rigorously evaluated using appropriate metrics.

#### Segmentation Evaluation Metrics:

Evaluated against ground truth masks using pixel-level confusion matrix:

- **Accuracy:** $(TP + TN) / (TP + TN + FP + FN)$ - Overall correctness
- **Sensitivity (Recall):** $TP / (TP + FN)$ - True positive rate
- **Specificity:** $TN / (TN + FP)$ - True negative rate

Where:
- TP = True Positives (correctly segmented lesion pixels)
- TN = True Negatives (correctly identified non-lesion pixels)
- FP = False Positives (incorrectly segmented non-lesion pixels)
- FN = False Negatives (missed lesion pixels)

#### Classification Evaluation Metrics:

Measured on held-out test set using sample-level metrics:

- **Accuracy:** Overall correctness of classifications
- **Precision:** $TP / (TP + FP)$ - Reliability of positive predictions
- **Recall:** $TP / (TP + FN)$ - Ability to detect all melanoma cases
- **F1-Score:** $2 \times (Precision \times Recall) / (Precision + Recall)$ - Harmonic mean balancing precision and recall

---

## Technology Stack & Libraries

### Core Libraries:
- **OpenCV (cv2):** Image processing and computer vision operations
- **NumPy:** Numerical computations and array operations
- **Pandas:** Data manipulation and analysis
- **Scikit-learn:** Machine learning algorithms and metrics

### Key Components:
```python
import cv2              # Image processing
import numpy as np      # Numerical operations
import pandas as pd     # Data handling
from sklearn.ensemble import RandomForestClassifier  # Classifier
from sklearn.model_selection import train_test_split  # Data splitting
from sklearn.metrics import confusion_matrix, classification_report  # Evaluation
from tqdm import tqdm   # Progress bars
```

---

## Dataset Information

### PH2 Dataset Structure

**Dataset Location:** `PH2 Dataset/PH2 Dataset images/`

**Folder Organization:**
```
PH2_Dataset_images/
├── IMD_XXX/
│   ├── IMD_XXX_Dermoscopic_Image/
│   │   └── [dermoscopic image file]
│   ├── IMD_XXX_lesion/
│   │   └── [ground truth mask]
│   └── IMD_XXX_clinical_diagnosis_image/
│       └── [clinical photo]
├── IMD_YYY/
└── ...
```

**Label Information:** `PH2_dataset.txt`
- Contains image metadata including Clinical Diagnosis
- Clinical Diagnosis '2' = Melanoma (Class 1)
- Clinical Diagnosis other values = Benign (Class 0)

**Dataset Statistics:**
- Total Samples: 200 images
- Benign (Class 0): 167 samples (83.5%)
- Melanoma (Class 1): 33 samples (16.5%)
- **Note:** Significant class imbalance present

---

## Project File Structure

```
DIP_PH2_Project.ipynb
├── Cell 1: Project Overview (Markdown)
├── Cell 2-7: Data exploration and validation
├── Cell 8-10: Required libraries and imports
├── Cell 11-22: Image processing helper functions
│   ├── enhance_image() - CLAHE enhancement
│   ├── remove_hairs() - Hair removal pipeline
│   └── segment_lesion() - Lesion segmentation
├── Cell 23-24: Mask generation main loop
├── Cell 25-26: Segmentation evaluation
├── Cell 27-35: Feature extraction and data loading
├── Cell 36: Train-test split
├── Cell 37: Random Forest classifier training
└── Cell 38: Classification evaluation
```

---

## Key Functions

### Image Enhancement
```python
def enhance_image(img):
    """Apply CLAHE for contrast enhancement"""
    - Converts BGR to LAB color space
    - Applies CLAHE on L-channel
    - Returns enhanced BGR image
```

### Hair Removal
```python
def remove_hairs(img):
    """Remove hair artifacts using morphological operations"""
    - Uses black-hat transform (17×17 kernel)
    - Binary thresholding on hair mask
    - Telea inpainting for artifact removal
```

### Lesion Segmentation
```python
def segment_lesion(img):
    """Segment lesion from background"""
    - Grayscale conversion and Gaussian blur
    - Otsu's automatic thresholding
    - Morphological closing (7×7 elliptical kernel)
    - Flood-fill for hole removal
    - Returns binary segmentation mask
```

### Feature Extraction
```python
def extract_features(img, mask):
    """Extract color statistics from masked lesion region"""
    - Computes mean and std for each BGR channel
    - Returns 6-element feature vector
    - Normalized pixel values
```

---

## Usage Instructions

### Prerequisites
- Python 3.7+
- Google Colab environment (for dataset access via Google Drive)
- GPU recommended for faster processing

### Installation
```bash
pip install opencv-python numpy pandas scikit-learn tqdm matplotlib
```

### Running the Project

1. **Mount Google Drive** (if using Colab):
   ```python
   from google.colab import drive
   drive.mount('/content/drive')
   ```

2. **Set Dataset Paths:**
   ```python
   BASE_PATH = "/path/to/PH2 Dataset images"
   SAVE_PATH = "/path/for/generated_masks"
   LABEL_TXT = "/path/to/PH2_dataset.txt"
   ```

3. **Execute Each Stage:**
   - Run image enhancement, hair removal, and segmentation cells
   - Run mask generation loop to create segmentation masks
   - Load features and labels
   - Perform train-test split
   - Train Random Forest classifier
   - Evaluate performance

4. **Analyze Results:**
   - Check confusion matrix and classification metrics
   - Review class distribution in train/test sets
   - Assess model performance on both classes

---

## Key Results & Findings

### Label Distribution
- Successfully corrected label extraction from 'Clinical Diagnosis' column
- Balanced stratification in train-test split

### Segmentation Performance
- Pixel-level evaluation against ground truth masks
- Metrics: Accuracy, Sensitivity, Specificity
- [Insert actual values when executed]

### Classification Performance

**Overall Accuracy:** 85%

**Class-wise Metrics:**
- **Benign (Class 0):** Precision 0.85, Recall 1.00
- **Melanoma (Class 1):** Precision 1.00, Recall 0.14

### Key Insights
1. **Class Imbalance Issue:** The 5:1 benign-to-melanoma ratio significantly impacts minority class detection
2. **High Precision, Low Recall for Melanoma:** All predicted melanoma cases are correct, but many actual cases are missed
3. **Perfect Recall for Benign:** All benign samples correctly identified
4. **Performance Gap:** The low recall for melanoma (0.14) indicates the model struggles to identify positive cases

---

## Addressing Class Imbalance

### Recommended Techniques

1. **SMOTE (Synthetic Minority Oversampling Technique)**
   ```python
   from imblearn.over_sampling import SMOTE
   smote = SMOTE(random_state=42)
   X_train_balanced, y_train_balanced = smote.fit_resample(X_train, y_train)
   ```

2. **Class Weight Adjustment**
   ```python
   clf = RandomForestClassifier(
       class_weight='balanced',  # Automatically adjust for imbalance
       n_estimators=50
   )
   ```

3. **Alternative Metrics**
   - Use F1-Score instead of Accuracy
   - Compute ROC-AUC for better imbalance assessment
   - Use weighted F1-Score

4. **Threshold Adjustment**
   - Modify prediction threshold to improve recall
   - Trade-off between precision and recall based on clinical needs

---

## Future Improvements

### Machine Learning Enhancements
- [ ] Implement SMOTE for class balance
- [ ] Try advanced classifiers (SVM, XGBoost, Deep Learning)
- [ ] Perform hyperparameter tuning with Grid Search
- [ ] Cross-validation for robust performance estimation
- [ ] Ensemble methods combining multiple classifiers

### Feature Engineering
- [ ] Add texture features (LBP, GLCM, Gabor filters)
- [ ] Include shape descriptors (circularity, asymmetry)
- [ ] Incorporate morphological features (size, border irregularity)
- [ ] Deep learning feature extraction (CNN-based)

### Segmentation Improvements
- [ ] Implement watershed segmentation
- [ ] Use active contours (snakes)
- [ ] Apply U-Net for semantic segmentation
- [ ] Ensemble segmentation methods

### Model Optimization
- [ ] Transfer learning with pre-trained models
- [ ] Dilated convolutional networks (DilatedCNN)
- [ ] Attention mechanisms for focus on important regions
- [ ] Multi-task learning (segmentation + classification)

### Evaluation Enhancements
- [ ] Stratified k-fold cross-validation
- [ ] ROC-AUC and PR-AUC curves
- [ ] Per-image segmentation quality assessment
- [ ] Clinical validation with dermatologists

---

## Important Notes

### Class Imbalance Warning
The dataset exhibits significant class imbalance (83.5% Benign vs. 16.5% Melanoma). This affects:
- Model training and convergence
- Metric interpretation (accuracy misleading)
- Minority class performance (low recall)

**Mitigation:** Use balanced metrics (F1-score, weighted metrics) and imbalance-handling techniques.

### Ground Truth Masks
Segmentation evaluation requires ground truth masks. Ensure masks are properly:
- Aligned with original images
- Binary format (0 for background, 255 for lesion)
- Matched with corresponding image filenames

### Reproducibility
Set `random_state=42` across all operations for reproducible results:
- Data splitting: `random_state=42`
- Random Forest: `random_state=42`
- SMOTE (if used): `random_state=42`

---

## References & Resources

### Relevant Techniques
- **CLAHE:** Zuiderveld, K. (1994). "Contrast Limited Adaptive Histogram Equalization"
- **Otsu's Thresholding:** Otsu, N. (1979). "A Threshold Selection Method from Gray-Level Histograms"
- **Morphological Operations:** Serra, J. (1982). "Image Analysis and Mathematical Morphology"
- **Random Forest:** Breiman, L. (2001). "Random Forests"

### Datasets
- PH2 Dataset: Mendoza-Procel et al., "Dermoscopy Image Analysis"
- Available at: [PH2 Dataset Official Source]

### Tools & Libraries
- OpenCV Documentation: https://opencv.org/
- Scikit-learn: https://scikit-learn.org/
- Pandas: https://pandas.pydata.org/

---

## Contact & Support

**Project Author:** AZAN LATIF  
**Roll No:** 2023-SE-14  
**Institution:** [Your Institution Name]

For questions or improvements, please contact the project author.

---

## License

[Specify License - e.g., MIT, GPL, etc.]

---

## Acknowledgments

- PH2 Dataset creators and contributors
- OpenCV and Scikit-learn communities
- Digital Image Processing course instructors

---

**Last Updated:** February 3, 2026  
**Project Status:** Active Development

