# Brain Tumor Classification using Deep Learning

A deep learning project for automatic brain tumor classification from MRI images. This repository compares multiple convolutional neural network architectures ranging from a custom CNN to state-of-the-art transfer learning models.

---

## 📋 Project Overview

Brain tumors are among the most challenging neurological diseases, where early and accurate diagnosis plays a critical role in treatment planning. Magnetic Resonance Imaging (MRI) is the primary imaging modality used by radiologists for brain tumor diagnosis.

In this project, four different deep learning models were implemented and compared for multiclass brain tumor classification:

- **CNN** (Custom Architecture)
- **VGG16** (Transfer Learning)
- **ResNet50** (Transfer Learning)
- **DenseNet121** (Transfer Learning)

The objective is to classify MRI scans into four categories:

- Glioma
- Meningioma
- Pituitary Tumor
- No Tumor

---

## 📊 Evaluation & Results Overview

All models were evaluated using confusion matrices, accuracy, and Macro F1-score metrics. The comprehensive analysis of these evaluations is located in the **[`Evaluation/`](Evaluation)** folder, broken down by architecture and performance metrics.

### 📁 [Confusion Matrices](Evaluation)
Detailed prediction breakdowns for each model are available here:
- 🔍 **[CNN Confusion Matrix & Analysis](Evaluation/CNN/Confusion%20Matrix/README.md)**
- 🔍 **[VGG16 Confusion Matrix & Analysis](Evaluation/VGG16/Confusion%20Matrix/README.md)**
- 🔍 **[ResNet50 Confusion Matrix & Analysis](Evaluation/ResNet50/Confusion%20Matrix/README.md)**
- 🔍 **[DenseNet121 Confusion Matrix & Analysis](Evaluation/DenseNet121/Confusion%20Matrix/README.md)**

### 📊 [Performance Comparisons](Evaluation)
- 📈 **[Overall Accuracy & F1-Score Charts](Evaluation/Performance%20Comparison/README.md)**: Visual comparison of the models' overall accuracy.
- 🏆 **[Macro F1-Score Comparison](Evaluation/F1-Comparison/README.md)**: A detailed look at the balanced performance across all classes.

---

## 🧠 Deep Learning Models

This project evaluates four different architectures. Each model has its own dedicated folder within the `Evaluation` directory containing its trained weights, confusion matrix, and specific analysis.

| Model | Type | Description |
|--------|------|-------------|
| [**CNN**](Evaluation/CNN) | Custom CNN | A baseline lightweight architecture built from scratch. |
| [**VGG16**](Evaluation/VGG16) | Transfer Learning | Classic architecture with excellent feature extraction. |
| [**ResNet50**](Evaluation/ResNet50) | Transfer Learning | Deep residual learning architecture (Best Performer). |
| [**DenseNet121**](Evaluation/DenseNet121) | Transfer Learning | Dense connectivity for efficient feature reuse. |

---

## 📈 Model Performance Comparison

Based on the final evaluations (see the comparison charts in the `Evaluation` folder), the models achieved the following metrics:

| Model | Accuracy | Macro F1-score |
|--------|----------|---------------|
| CNN | 78% | 0.78 |
| VGG16 | 87% | 0.87 |
| DenseNet121 | 87% | 0.87 |
| **ResNet50** | **93%** | **0.93** |

### 🏆 Best Model: ResNet50

**ResNet50** achieved the highest performance among all evaluated models. Reasons include:

- **Residual Learning** (Skip connections) allowing for very deep networks.
- **ImageNet pretrained weights** providing excellent transfer learning capability.
- Superior ability to differentiate between complex tumor boundaries and normal tissue.

---

## 📁 Dataset

The dataset consists of brain MRI images belonging to four classes.

| Class | Description |
|---------|------------|
| Glioma | Intra-axial brain tumor |
| Meningioma | Extra-axial brain tumor |
| Pituitary | Pituitary gland tumor |
| No Tumor | Normal brain MRI |

**Preprocessing:** All images were resized to **128 × 128 × 3** before training.

---

## 🔄 Data Augmentation

To improve model generalization and reduce overfitting, real-time data augmentation was applied during training.

The augmentation pipeline includes:

- Random Rotation
- Width & Height Shift
- Zoom
- Horizontal Flip
- Shear Transformation
- Filling Missing Pixels

**Benefits:** Better generalization, reduced overfitting, and increased robustness to image variations.

---

## 🛠 Technologies & Libraries

- **Python**
- **TensorFlow / Keras** (Model development and training)
- **NumPy** (Data manipulation)
- **OpenCV** (Image preprocessing)
- **Matplotlib** (Visualization)
- **Scikit-learn** (Metric evaluation)

---

## 🔮 Future Work

Possible future improvements include:

- Applying **Vision Transformers (ViT)** and **EfficientNet** architectures.
- **Explainable AI (Grad-CAM)** to visualize model decision-making.
- **K-Fold Cross-Validation** for more robust performance estimation.
- Advanced **Hyperparameter Optimization**.

