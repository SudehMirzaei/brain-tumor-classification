# Convolutional Neural Network (CNN)

## Introduction

A **Convolutional Neural Network (CNN)** is a specialized type of deep neural network designed to process image data. Unlike traditional fully connected neural networks, CNNs automatically learn spatial features directly from images by applying convolution operations.

CNNs have become the standard architecture for computer vision tasks such as:

- Image Classification
- Object Detection
- Medical Image Analysis
- Face Recognition
- Image Segmentation

Instead of manually designing image features, CNNs learn hierarchical representations automatically during training.

---

# Why CNNs Work So Well for Images

Images contain strong spatial relationships between neighboring pixels.

A CNN preserves these spatial relationships by using small learnable filters (kernels) that slide across the image.

Rather than treating every pixel independently, CNNs learn local patterns such as:

- Edges
- Corners
- Curves
- Textures
- Shapes
- High-level objects

As the network becomes deeper, these simple features gradually combine into more complex visual concepts.

---

# CNN Architecture

A typical CNN consists of several building blocks:

```
Input Image
      │
Convolution Layer
      │
Activation (ReLU)
      │
Pooling Layer
      │
Convolution Layer
      │
Activation
      │
Pooling
      │
...
      │
Flatten
      │
Fully Connected Layers
      │
Softmax Output
```

---

# Convolution Layer

The convolution layer is the core component of a CNN.

Instead of analyzing the entire image at once, the network scans the image using small filters called **kernels**.

Each kernel extracts a specific visual pattern.

Examples include:

- Vertical edges
- Horizontal edges
- Curves
- Texture patterns

The output of a convolution operation is called a **feature map**.

---

# Kernel (Filter)

A kernel is a small matrix of learnable weights.

Typical kernel sizes include:

- 3 × 3
- 5 × 5
- 7 × 7

Example:

```
3 × 3 Kernel

[
 1  0 -1
 1  0 -1
 1  0 -1
]
```

As training progresses, CNN automatically learns the optimal kernel values.

---

# Kernel Size

Kernel size determines how much local information is captured at each convolution.

Small kernels (3×3)

Advantages:

- Capture fine details
- Require fewer parameters
- Enable deeper networks

Large kernels (7×7)

Advantages:

- Larger receptive field
- Capture broader context

Disadvantages:

- More parameters
- Higher computational cost

Modern CNN architectures typically use multiple 3×3 kernels instead of a single large kernel.

---

# Stride

Stride defines how far the kernel moves after each convolution.

Stride = 1

```
□□□□
□□□□
□□□□
```

The filter moves one pixel at a time.

Stride = 2

The filter skips every other pixel.

Effects of larger stride:

- Smaller feature maps
- Faster computation
- Less spatial detail

---

# Padding

Padding adds extra pixels around the image border before convolution.

Without padding:

Image size gradually shrinks.

With padding:

Image dimensions are preserved.

Common padding types:

- Valid Padding (no padding)
- Same Padding (preserve image size)

Padding helps retain important information near image boundaries.

---

# Number of Filters

Each convolution layer usually contains multiple filters.

Example:

Layer 1:

32 filters

↓

32 feature maps

Layer 2:

64 filters

↓

64 feature maps

Layer 3:

128 filters

↓

128 feature maps

Increasing the number of filters allows the network to learn richer visual representations.

---

# Activation Function (ReLU)

After convolution, the output passes through an activation function.

The most common activation is ReLU:

```
ReLU(x) = max(0, x)
```

Advantages:

- Introduces non-linearity
- Faster convergence
- Reduces vanishing gradient problems

---

# Max Pooling

Pooling reduces the spatial size of feature maps.

The most common pooling operation is **Max Pooling**.

Example:

```
2 × 2 Window

6 3
1 5

↓

6
```

The maximum value is retained.

Benefits:

- Reduces computation
- Reduces overfitting
- Improves translation invariance

---

# Flatten Layer

Convolution layers produce 3D feature maps.

Before classification, these feature maps are flattened into a one-dimensional vector.

Example:

```
7 × 7 × 64

↓

3136
```

This vector becomes the input to the fully connected layers.

---

# Fully Connected Layer

The fully connected layers combine all extracted image features and perform the final classification.

These layers learn relationships between high-level features.

---

# Softmax Layer

The final layer converts network outputs into class probabilities.

For example:

```
Glioma       0.93
Meningioma   0.03
Pituitary    0.02
No Tumor     0.02
```

The class with the highest probability becomes the predicted label.

---

# Hierarchical Feature Learning

One of the most important characteristics of CNNs is hierarchical feature extraction.

Early layers learn simple patterns:

- Edges
- Brightness changes
- Corners
- Basic textures

Middle layers combine these features into more meaningful structures:

- Tissue boundaries
- Ventricles
- Tumor margins
- Shape patterns

Deep layers learn semantic concepts:

- Tumor presence
- Tumor location
- Tumor morphology
- Tumor type

This hierarchical learning enables CNNs to automatically discover informative visual features without manual feature engineering.

---

# Advantages of CNNs

- Automatic feature extraction
- Parameter sharing
- Translation invariance
- High classification accuracy
- Efficient learning from image data
- Excellent performance in medical imaging

---

# Limitations of CNNs

- Require large datasets
- Computationally expensive
- Can overfit on small datasets
- Limited ability to model long-range dependencies compared with Transformer-based models

---

# CNN for Brain Tumor MRI Classification

Brain MRI images contain complex anatomical structures and subtle intensity variations.

Traditional machine learning approaches require handcrafted features designed by domain experts.

CNNs eliminate this requirement by learning discriminative features directly from MRI scans.

During training:

- Early convolution layers detect edges, intensity transitions, and simple textures within brain tissues.
- Intermediate layers learn anatomical structures such as ventricles, white matter, gray matter, and lesion boundaries.
- Deeper layers integrate these features into high-level representations describing tumor shape, size, internal texture, surrounding edema, and overall morphology.

These hierarchical representations enable the network to distinguish among different tumor types, including:

- Glioma
- Meningioma
- Pituitary Tumor
- No Tumor

Because tumor classification depends heavily on complex visual patterns rather than handcrafted measurements, CNNs are particularly well suited for this task.

---

# CNN in This Project

In this project, a custom CNN was developed as the baseline deep learning model for multiclass brain tumor classification using MRI images.

The model receives preprocessed MRI scans as input and progressively extracts increasingly complex visual features through multiple convolution and pooling layers.

The extracted features are then passed to fully connected layers for final classification into four categories:

- Glioma
- Meningioma
- Pituitary Tumor
- No Tumor

This baseline CNN serves as a reference model and provides a foundation for comparison with more advanced transfer learning architectures such as VGG16, ResNet50, and DenseNet121.

---

# Summary

CNNs learn visual representations in a hierarchical manner.

Rather than relying on manually designed image features, they automatically discover meaningful patterns ranging from simple edges to complex tumor structures.

This ability has made CNNs one of the most successful architectures for medical image classification, particularly in MRI-based brain tumor diagnosis.


