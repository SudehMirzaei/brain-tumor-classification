# Brain Tumor Classification using Deep Learning

A deep learning project for automatic brain tumor classification from MRI images. This repository compares multiple convolutional neural network architectures ranging from a custom CNN to state-of-the-art transfer learning models.

---

# Project Overview

Brain tumors are among the most challenging neurological diseases, where early and accurate diagnosis plays a critical role in treatment planning. Magnetic Resonance Imaging (MRI) is the primary imaging modality used by radiologists for brain tumor diagnosis.

In this project, four different deep learning models were implemented and compared for multiclass brain tumor classification:

- CNN (Custom Architecture)
- VGG16 (Transfer Learning)
- ResNet50 (Transfer Learning)
- DenseNet121 (Transfer Learning)

The objective is to classify MRI scans into four categories:

- Glioma
- Meningioma
- Pituitary Tumor
- No Tumor

---

# Dataset

The dataset consists of brain MRI images belonging to four classes.

| Class | Description |
|---------|------------|
| Glioma | Intra-axial brain tumor |
| Meningioma | Extra-axial brain tumor |
| Pituitary | Pituitary gland tumor |
| No Tumor | Normal brain MRI |

All images were resized to:

128 × 128 × 3
before training.

---

# Data Augmentation

To improve model generalization and reduce overfitting, real-time data augmentation was applied during training.

The augmentation pipeline includes:

- Random Rotation
- Width Shift
- Height Shift
- Zoom
- Horizontal Flip
- Shear Transformation
- Filling Missing Pixels

Data augmentation increases the diversity of the training dataset by generating slightly modified versions of MRI images while preserving their diagnostic characteristics.

Benefits include:

- Better generalization
- Reduced overfitting
- Increased robustness to image variations
- Improved performance on unseen MRI scans

---

# Deep Learning Models

This project evaluates four different architectures.

| Model | Type |
|--------|------|
| CNN | Custom CNN |
| VGG16 | Transfer Learning |
| ResNet50 | Transfer Learning |
| DenseNet121 | Transfer Learning |

Detailed explanations are available in the documentation:

📘 [CNN Architecture](docs/CNN.md)

📘 [VGG16](docs/VGG16.md)

📘 [ResNet50](docs/ResNet50.md)

📘 [DenseNet121](docs/DenseNet121.md)

---

# Model Comparison

| Model | Accuracy | Macro F1-score |
|--------|----------|---------------|
| CNN | 78% | 0.78 |
| VGG16 | 87% | 0.87 |
| DenseNet121 | 87% | 0.87 |
| ResNet50 | 93% | 0.93 |

---

# Performance Analysis

### CNN

- Lightweight architecture
- Fast training
- Good baseline model
- Lower performance compared with transfer learning models

---

### VGG16

- Excellent feature extraction
- Stable convergence
- Significant improvement over the custom CNN

---

### DenseNet121

- Efficient feature reuse through dense connections
- Strong performance with fewer parameters
- Better gradient propagation

---

### ResNet50

ResNet50 achieved the highest performance among all evaluated models.

Reasons include:

- Residual Learning
- Deep architecture
- ImageNet pretrained weights
- Excellent transfer learning capability
- Strong feature extraction from MRI images

---

# Final Results

ResNet50 obtained the best overall performance.

| Metric | Value |
|---------|-------|
| Accuracy | 93% |
| Macro F1-score | 0.93 |

---

# Technologies

- Python
- TensorFlow / Keras
- NumPy
- OpenCV
- Matplotlib
- Scikit-learn

---

# Future Work

Possible future improvements include:

- Vision Transformers (ViT)
- EfficientNet
- ConvNeXt
- Explainable AI (Grad-CAM)
- Cross-validation
- Hyperparameter optimization

---

# References

The transfer learning models are based on pretrained ImageNet weights provided by TensorFlow/Keras.
