# 🧠 Cortical Thickness Estimation from Brain MRI

## 📌 Overview
This neuroimaging project focuses on estimating the cortical thickness map of T1-weighted MRI brain scans. The cortical thickness—the distance between the gray/white matter boundary and the outer (pial) surface—is an important biomarker in neuroscience and disease diagnosis. We developed a method to extract this thickness map from raw brain scans using Python-based image processing.

## 🧬 Objective
To segment the white and gray matter in T1-weighted brain MRIs and calculate cortical thickness using voxel-wise Euclidean distances.

## 🧠 Dataset & Tools
- `raw_t1_subject_01.nii.gz`: Raw T1 MRI scan (subject 1)
- `raw_t1_subject_02.nii.gz`: Raw T1 MRI scan (subject 2)
- `thickness_map_subject_01.nii.gz`: Ground-truth cortical thickness map for validation
- **Libraries Used**: NumPy, SciPy, scikit-image, NiBabel, Matplotlib

## ⚙️ Methodology

### 1. Image Preparation
- Loaded `.nii.gz` files using `nibabel`
- Applied a Gaussian filter to smooth the raw images for better segmentation

### 2. White Matter Segmentation
- Used a threshold to extract high-intensity voxels representing white matter
- Applied binary dilation and subtraction to isolate the gray/white matter boundary

### 3. Gray Matter Segmentation & Pial Surface Extraction
- Segmented gray matter using intensity thresholds
- Applied dilation and subtraction to identify the pial surface
- Cleaned up results by removing negative voxel values

### 4. Coordinate Extraction
- Used `np.argwhere()` to extract non-zero coordinates for all relevant masks (gray/white boundary, pial surface)

### 5. Cortical Distance Calculation
- Calculated Euclidean distances from each gray/white voxel to its nearest pial voxel using:
  ```python
  from scipy.spatial import distance
  ```
- Stored the minimum distance at each gray/white voxel

### 6. Cortical Thickness Map Generation
- Used KDTree for efficient nearest-neighbor search
- Assigned thickness values to all gray matter voxels to generate the final map

## 📈 Results
- Cortical thickness maps were generated for both subject 1 and subject 2.
- Comparison with the provided reference map showed a similar structure, though with slight deviations.
- Identified visual inconsistencies in specific brain regions—mainly due to thresholding errors and segmentation imperfections.

## 🚧 Challenges
- Long computation time due to nested loops and 3D voxel comparisons
- Difficulty in fine-tuning thresholds for clean segmentation of brain tissues
- Variability in brain anatomy caused generalization challenges for different subjects

## 📊 Technologies Used
- Python (NumPy, SciPy, skimage, NiBabel)
- Jupyter Notebook
- Git / GitHub for version control

## 👏 Author
**Reza Zare** — Implemented full segmentation pipeline and analysis as part of an academic project at Bishop’s University.

## 📎 Credits
Academic research project under Bishop’s University — guided by Dr. Russel Butler
