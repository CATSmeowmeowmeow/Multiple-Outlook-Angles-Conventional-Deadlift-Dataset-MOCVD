# 📘 Multiple Outlook-Angles Conventional Deadlift Dataset (MOCVD)

## 1. Overview

This dataset contains multi-view recordings of the conventional deadlift exercise.  
It is designed for motion analysis, error detection, and biomechanics research, with five synchronized camera views:

- Left (L)  
- Front (F)  
- Front-Left (FL)  
- Rear-Left (RL)  
- Rear-Right-Upper (RRU)  

The dataset includes correct and incorrect deadlift techniques, annotated with barbell positions, 2D/3D joint coordinates, and joint angles.

---

## 2. Dataset Structure

The dataset is organized by movement class → subject → set →
`Clips/Coordinate/Angle/Chessboard`.

```
correct/
└── subject1/
    ├── Clips/
    │   ├── L/
    │   │   └── *.mp4
    │   ├── F/
    │   │   └── *.mp4
    │   ├── FL/
    │   │   └── *.mp4
    │   ├── RL/
    │   │   └── *.mp4
    │   └── RRU/
    │       └── *.mp4
    ├── Coordinate/
    │   ├── 2D_L/
    │   │   └── *.csv
    │   ├── 2D_FL/
    │   │   └── *.csv
    │   ├── 2D_RL/
    │   │   └── *.csv
    │   ├── bar/
    │   │   └── *.csv
    │   └── 3D/
    │       └── *.json
    ├── Angle/
    │   ├── 2D_L/
    │   │   └── *.csv
    │   ├── 2D_FL/
    │   │   └── *.csv
    │   ├── 2D_RL/
    │   │   └── *.csv
    │   └── 3D/
    │       └── *.csv
    └── Chessboard/
        ├── extri.yml
        └── intri.yml

```

### 🔹 Special Notes
- The **Chessboard** folder includes two parameter files:  
  - **`intri.yml`**: stores **intrinsic parameters** of each camera, including the camera matrix (focal length, principal point) and distortion coefficients.  
  - **`extri.yml`**: stores **extrinsic parameters**, including rotation matrices (R) and translation vectors (T) describing each camera’s position and orientation relative to the world coordinate system.    
- **Multi-error samples** (e.g., *Hips_rising_before_the_barbell_leaves_the_ground + Lower_back_rounding*) are listed in the file **`multierror.json`** at the dataset root. This file maps each subject repetition to multiple error labels.  

---

## 3. Classes

The dataset contains **5 primary classes**:

1. correct  
2. barbell_moving_away_from_shins  
3. hips_rising_before_barbell_lift  
4. barbell_colliding_with_knees  
5. lower_back_rounding  

---

## 4. Data Modalities

- **Clip data**: `.mp4` format, five synchronized camera views.  

- **Coordinate data**:  
  - `Bar`
    - positions extracted with a custom YOLOv11n model
  - `2D_FL/`,`2D_L/`,`2D_RL/`:
    - extracted with YOLOv11-Pose
    - Col1 = frame index  
    - Col2 = YOLOv11 skeleton keypoint ID  
    - Col3 = X coordinate  
    - Col4 = Y coordinate
  - `3D/`:
    - reconstructed using custom proccess from multi-view 2D keypoints extracted with YOLOv11x model
    - Field `keypoints_3d` follows **COCO17** joint order
    - Each keypoint has: (x, y, z)

- **Angle data**: Computed joint angles from 2D and 3D coordinates.  
  - `2D_FL/`:  
    - Col1 = frame index  
    - Col2 = right hip angle  
    - Col3 = right knee angle  
  - `2D_L/`:  
    - Col1 = frame index  
    - Col2 = horizontal distance between left shoulder & bar endpoint  
    - Col3 = body length  
  - `2D_RL/`:  
    - Col1 = frame index  
    - Col2 = left hip angle  
    - Col3 = left knee angle  
  - `3D/`:  
    - Col1 = frame index  
    - Col2 = left knee angle  
    - Col3 = left hip angle  
    - Col4 = right knee angle  
    - Col5 = right hip angle  
    - Col6 = body length  
    - Col7 = left arm–torso angle  
    - Col8 = right arm–torso angle  

---

## 5. Statistics

- **Total samples**: 1,109 sets including 8,506 repetitions  
- **Participants**: 156 subjects (134 male, 22 female)  
- **Views per repetition**: 5 synchronized videos  
- **3D reconstructions**: 7,342 valid sequences 
- **Annotations**: barbell bounding boxes, 2D/3D keypoints, joint angles  

---

## 6. Datasets & Download Links

The models heavily rely on coordinate and temporal feature data. The datasets should be placed in the `data/` directory, organized into `deadlift` and `benchpress` subdirectories.

### Deadlift Dataset (MOCVD)
Utilizes the **Multiple Outlook-Angles Conventional Deadlift Dataset (MOCVD)**.

**Download Links (Split 7z Archives):**
- [DeadliftDataset.7z.001](https://catslab.ee.ncku.edu.tw/public/DeadliftDataset/DeadliftDataset.7z.001)
- [DeadliftDataset.7z.002](https://catslab.ee.ncku.edu.tw/public/DeadliftDataset/DeadliftDataset.7z.002)
- [DeadliftDataset.7z.003](https://catslab.ee.ncku.edu.tw/public/DeadliftDataset/DeadliftDataset.7z.003)
- [DeadliftDataset.7z.004](https://catslab.ee.ncku.edu.tw/public/DeadliftDataset/DeadliftDataset.7z.004)
- [DeadliftDataset.7z.005](https://catslab.ee.ncku.edu.tw/public/DeadliftDataset/DeadliftDataset.7z.005)
- [DeadliftDataset.7z.006](https://catslab.ee.ncku.edu.tw/public/DeadliftDataset/DeadliftDataset.7z.006)

*Note: You will need to download all parts and use a tool like 7-Zip to extract them.*

---

## 7. License

This dataset is provided for **academic research purposes only**.  
For commercial use, please contact the authors.

---

## 8. Citation

If you use this dataset, please cite:

```bibtex
@dataset{deadlift_multiview_2025,
  title     = {Multiple Outlook-Angles Conventional Deadlift Dataset (MOCVD)},
  author    = {Guan-Ting Chen and Collaborators},
  year      = {2025},
  publisher = {National Cheng Kung University}
}
```
