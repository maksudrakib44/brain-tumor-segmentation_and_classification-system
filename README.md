
### Segmentation-Guided Deep Learning Framework for Early Brain Tumor Detection in MRI Scans

```markdown
# Brain Tumor Segmentation and Classification System

[![Python](https://img.shields.io/badge/Python-3.8%2B-blue)](https://www.python.org/)
[![TensorFlow](https://img.shields.io/badge/TensorFlow-2.10%2B-orange)](https://www.tensorflow.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A deep learning framework for early brain tumor detection in MRI scans, combining U-Net-based tumor segmentation with ROI-guided CNN classification.

## 📋 Overview

This project implements a novel **segmentation-guided deep learning pipeline** that first accurately segments tumor regions from MRI slices and then uses these segmented regions of interest (ROIs) for focused classification. This integrated approach enhances both diagnostic accuracy and clinical interpretability compared to systems that treat segmentation and classification as separate tasks.

**Key Features:**
- 🧠 **U-Net Architecture** for precise tumor segmentation
- 🔍 **ROI-Guided CNN Classifier** for focused diagnostic classification
- 📊 **Comprehensive Visual Outputs**: Segmentation masks, bounding boxes, heatmaps, and confidence scores
- 🏥 **Clinical Interpretability**: Designed for computer-aided diagnostic systems
- 📈 **High Performance**: Validated on the BraTS 2020 dataset

## 🎯 Key Results

| Task | Metric | Score |
|------|--------|-------|
| **Segmentation** | Dice Coefficient | 0.9234 |
| | IoU | 0.8588 |
| **Classification** | Accuracy | 97.36% |
| | Precision | 98.22% |
| | Recall (Sensitivity) | 95.59% |
| | F1-Score | 96.89% |
| | ROC-AUC | 0.9963 |

## 🏗️ Architecture

The proposed framework follows a systematic pipeline:

```
Input MRI Slice → Preprocessing → U-Net Segmentation → ROI Extraction → CNN Classification → Diagnosis + Visual Outputs
```

### 1. Segmentation Module (U-Net)
- Encoder-decoder structure with skip connections
- Trained with Dice loss for handling class imbalance
- Outputs tumor probability masks

### 2. ROI Extraction
- Binarizes predicted masks (threshold > 0.5)
- Extracts bounding boxes around detected tumor regions
- Resizes ROIs to 64×64 pixels for classification

### 3. Classification Module (CNN)
- Processes ROI patches for focused diagnosis
- Binary classifier (tumor vs. no tumor)
- Provides confidence scores for predictions

## 📊 Dataset

We used the **BraTS 2020 dataset**, which contains:
- **57,195 MRI slices** from 369 patients
- Multi-modal scans: T1, T1ce, T2, FLAIR
- Expert-annotated tumor masks (WT, TC, ET regions)

**Preprocessing:**
- FLAIR modality selection (optimal tumor visibility)
- Resizing to 128×128 pixels
- Z-score normalization (non-zero voxels only)
- Binary mask merging (WT + TC + ET → tumor presence)

## 🚀 Installation

```bash
# Clone the repository
git clone https://github.com/maksudrakib44/brain-tumor-segmentation_and_classification-system.git
cd brain-tumor-segmentation_and_classification-system

# Install dependencies
pip install -r requirements.txt
```

### Requirements
```
tensorflow>=2.10
numpy>=1.21
matplotlib>=3.5
scikit-learn>=1.0
opencv-python>=4.5
h5py>=3.6
```

## 💻 Usage

### Training

```python
# Train segmentation model
python train_segmentation.py --epochs 25 --batch_size 16 --lr 1e-4

# Train classification model
python train_classification.py --epochs 15 --batch_size 64 --lr 1e-4
```

### Inference

```python
from inference import BrainTumorDetector

# Initialize detector
detector = BrainTumorDetector(
    seg_model_path='models/unet_best.h5',
    clf_model_path='models/cnn_best.h5'
)

# Predict on single slice
result = detector.predict(mri_slice)

# Access outputs
print(f"Diagnosis: {'Tumor' if result['has_tumor'] else 'No Tumor'}")
print(f"Confidence: {result['confidence']:.2f}")
print(f"Dice Score: {result['dice_score']:.4f}")

# Visualize results
detector.visualize(mri_slice, result)
```

## 📈 Results Visualization

The system provides comprehensive visual outputs:
- **Segmentation masks** (ground truth vs. predicted)
- **Bounding boxes** for tumor localization
- **Heatmaps** showing tumor probability
- **Classification confidence scores**

## 📚 Citation

If you use this code or find our work helpful for your research, please cite our paper:

```bibtex
@article{haque2025segmentation,
  title={Segmentation-Guided Deep Learning Framework for Early Brain Tumor Detection in MRI Scans},
  author={Haque, Md. Maksudul and Shipon, Md. Mostakim Rahman and Ony, Nadira Jahan and Kabir, Syed Ahsanul and Habiba, Umme},
  journal={arXiv preprint},
  year={2025}
}
```

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👥 Authors

- **Md. Maksudul Haque** - [221002127@student.green.edu.bd](mailto:221002127@student.green.edu.bd)
- **Md. Mostakim Rahman Shipon** - [221002098@student.green.edu.bd](mailto:221002098@student.green.edu.bd)
- **Nadira Jahan Ony** - [221902391@student.green.edu.bd](mailto:221902391@student.green.edu.bd)
- **Syed Ahsanul Kabir** - [kabir@cse.green.edu.bd](mailto:ahsan@cse.green.edu.bd)
- **Umme Habiba** - [habiba@cse.green.edu.bd](mailto:habiba@cse.green.edu.bd)

## 🙏 Acknowledgments

- BraTS 2020 organizers for providing the dataset
- Green University of Bangladesh for research support

## 📬 Contact

Mail: research.maksud@gmail.com
Get in touch: https://maksud-portfolio.vercel.app/

---

**Note:** This implementation is based on the paper "Segmentation-Guided Deep Learning Framework for Early Brain Tumor Detection in MRI Scans". The code will be updated regularly with improvements and new features.
```

