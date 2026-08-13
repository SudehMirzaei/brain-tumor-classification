# ResNet50

## Introduction

Deep learning has revolutionized the field of computer vision by enabling computers to automatically learn meaningful visual features directly from images. Among the many convolutional neural network (CNN) architectures, **ResNet (Residual Network)** is considered one of the most influential models ever developed.

Before ResNet, researchers attempted to improve image classification performance simply by increasing the number of neural network layers. Although deeper networks theoretically have greater learning capacity, training them became increasingly difficult due to optimization problems such as the **vanishing gradient**. As a result, very deep networks often performed worse than their shallower counterparts.

To overcome this challenge, Microsoft Research introduced **Residual Networks (ResNet)** in 2015. Instead of forcing each layer to learn a complete transformation, ResNet allows layers to learn only the **residual (difference)** between the input and the desired output through shortcut connections.

Among the different versions of ResNet, **ResNet50** is one of the most widely used because it provides an excellent balance between classification performance, computational efficiency, and transfer learning capability. Today, it is extensively applied in medical imaging, including MRI, CT, X-ray, retinal imaging, and pathology.

---

# What is ResNet?

**ResNet (Residual Network)** is a deep convolutional neural network architecture proposed by **Kaiming He et al.** in the paper:

> *Deep Residual Learning for Image Recognition* (CVPR 2016)

The key innovation of ResNet is the introduction of **residual learning**, which allows information to bypass one or more layers using **skip connections** (shortcut connections).

Instead of directly learning a mapping:

\[
H(x)
\]

ResNet learns the residual:

\[
F(x)=H(x)-x
\]

Therefore,

\[
H(x)=F(x)+x
\]

This simple idea enables extremely deep neural networks to train successfully.

---

# Why ResNet was Introduced?

Before ResNet, increasing network depth generally improved accuracy only up to a certain point.

Beyond approximately 20–30 layers, researchers observed:

- Training became unstable.
- Optimization became difficult.
- Gradients became extremely small.
- Accuracy saturated.
- Even training error increased.

This phenomenon is known as the **degradation problem**.

ResNet solved this issue by making optimization significantly easier through residual learning.

---

# Vanishing Gradient Problem

Deep neural networks are trained using **backpropagation**.

During training, gradients are propagated from the output layer toward the earlier layers.

If gradients become very small:

- Early layers receive almost no learning signal.
- Weight updates approach zero.
- Learning nearly stops.

This is called the **vanishing gradient problem**.

As networks become deeper, this issue becomes more severe.

ResNet greatly reduces this problem because shortcut connections allow gradients to flow directly through the network.

---

# Residual Learning

Instead of forcing a stack of convolutional layers to learn an entire mapping, ResNet asks them to learn only the difference between input and output.

If the desired mapping is:

\[
H(x)
\]

the residual function becomes:

\[
F(x)=H(x)-x
\]

The final output is:

\[
Output = F(x)+x
\]

Learning residuals is often much easier than learning complete mappings, especially in very deep networks.

---

# Skip Connections

A **skip connection** (also called a shortcut connection) directly passes the input of a block to its output.

```
Input
  │
  ▼
Convolution Layers
  │
  ▼
Residual Output
  │
  ├──────────────┐
  ▼              │
Addition ◄───────┘
  │
  ▼
Output
```

These shortcut connections:

- preserve important information,
- improve gradient flow,
- stabilize training,
- reduce optimization difficulty,
- enable very deep architectures.

---

# Residual Blocks

ResNet is constructed from many **Residual Blocks**.

A residual block typically contains:

- Convolution
- Batch Normalization
- ReLU Activation
- Convolution
- Batch Normalization
- Skip Connection
- Addition
- ReLU

Each block learns a residual representation rather than a complete transformation.

---

# Identity Block vs Convolutional Block

ResNet50 mainly uses two types of residual blocks.

## Identity Block

The input and output dimensions are identical.

The shortcut connection directly copies the input.

```
Input
 │
 ├───────────────┐
 │               │
 ▼               │
Conv → Conv → Conv
 │               │
 └────Add────────┘
        │
      Output
```

---

## Convolutional Block

Sometimes the spatial size or number of channels changes.

In these cases, the shortcut itself performs a convolution to match dimensions.

```
Input
 │
 ├────Conv───────┐
 │               │
 ▼               │
Conv → Conv → Conv
 │               │
 └────Add────────┘
        │
      Output
```

---

# ResNet50 Architecture

ResNet50 contains **50 learnable layers**.

Its overall architecture consists of:

- Initial Convolution (7×7)
- Max Pooling
- Four residual stages
- Global Average Pooling
- Fully Connected Layer
- Softmax Classification

Architecture summary:

| Stage | Output Size | Blocks |
|--------|------------|---------|
| Conv1 | 112×112 | 7×7 Conv |
| MaxPool | 56×56 | Pooling |
| Conv2_x | 56×56 | 3 Residual Blocks |
| Conv3_x | 28×28 | 4 Residual Blocks |
| Conv4_x | 14×14 | 6 Residual Blocks |
| Conv5_x | 7×7 | 3 Residual Blocks |
| Average Pool | 1×1 | Global Average Pooling |
| FC | Classes | Dense Layer |

ResNet50 contains approximately **25 million parameters**.

---

# Transfer Learning

Training a deep neural network from scratch requires:

- massive datasets,
- powerful GPUs,
- long training times.

Medical datasets are usually much smaller than natural image datasets.

Instead of training from scratch, we use **Transfer Learning**.

Transfer learning means:

> Reusing knowledge learned from a large dataset and adapting it to a new task.

Rather than initializing all weights randomly, we start with a pretrained model and fine-tune it for our dataset.

---

# ImageNet Pretrained Weights

ResNet50 is commonly pretrained on **ImageNet**, a large-scale dataset containing over **1 million images** across **1000 categories**.

During pretraining, the network learns general visual features such as:

- edges,
- corners,
- textures,
- shapes,
- patterns,
- object structures.

These learned representations are useful for many different computer vision tasks, including medical image analysis.

---

# Frozen Backbone

When using transfer learning, the pretrained convolutional layers are often called the **backbone**.

Initially, these layers can be **frozen**, meaning their weights remain unchanged during training.

Benefits include:

- faster training,
- reduced computational cost,
- lower risk of overfitting,
- preservation of useful low-level visual features.

After training the classifier, selected deeper layers may be **unfrozen** and fine-tuned to better adapt to the medical imaging domain.

---

# Classification Head

The original ResNet50 model ends with a classifier designed for ImageNet's 1000 classes.

For a brain MRI classification task, this final layer is replaced with a new **classification head** that matches the number of target classes.

A typical custom head includes:

- Global Average Pooling
- Dropout (optional)
- Fully Connected (Dense) Layer
- Softmax activation for multi-class classification

For example, in a four-class brain MRI dataset, the final Dense layer outputs probabilities for:

- Glioma
- Meningioma
- Pituitary Tumor
- No Tumor

The class with the highest probability is selected as the predicted label.

---

# Why ResNet50 for Brain MRI?

Brain MRI classification presents several challenges:

- limited annotated datasets,
- subtle anatomical differences,
- low contrast between tissues,
- high similarity among tumor types,
- risk of overfitting.

ResNet50 addresses these challenges by:

- leveraging pretrained ImageNet features,
- enabling efficient transfer learning,
- learning deep hierarchical image representations,
- mitigating vanishing gradients with residual connections,
- performing well even with relatively small medical datasets.

Its ability to capture both low-level textures and high-level structures makes it highly suitable for distinguishing between different brain tumor types.

---

# How ResNet50 Works in Our Project

In this project, ResNet50 is used as the feature extraction backbone for classifying brain MRI images into four categories:

- Glioma
- Meningioma
- Pituitary Tumor
- No Tumor

The workflow is as follows:

1. Brain MRI images are resized to the required input size (typically 224×224 pixels).
2. Images are normalized using ImageNet preprocessing.
3. The pretrained ResNet50 backbone extracts hierarchical visual features.
4. The custom classification head processes these features.
5. Softmax produces class probabilities.
6. The class with the highest probability is selected as the final prediction.

During training, transfer learning enables the model to converge faster and achieve higher accuracy than training from scratch.

---

# Advantages

ResNet50 offers several important advantages:

- Excellent classification accuracy.
- Effective training of deep networks.
- Reduced vanishing gradient problem.
- Strong transfer learning performance.
- Extensive community support.
- Proven effectiveness in medical imaging.
- Robust feature extraction.
- Good balance between accuracy and computational cost.

---

# Limitations

Despite its strengths, ResNet50 also has limitations:

- Large model size (~25 million parameters).
- Higher computational requirements than lightweight models.
- Longer inference time compared to MobileNet or EfficientNet-B0.
- Originally trained on natural images rather than medical images.
- Fine-tuning may still require careful hyperparameter selection.

---

# Summary

ResNet50 is one of the most successful convolutional neural network architectures developed for image recognition. Its introduction of residual learning and skip connections solved the degradation and vanishing gradient problems that previously limited the depth of neural networks.

Combined with transfer learning from ImageNet, ResNet50 has become a standard backbone for many medical imaging applications, including brain MRI analysis. By leveraging pretrained visual representations and adapting them through fine-tuning, the model achieves strong performance even on relatively small datasets.

For brain tumor classification, ResNet50 provides a reliable balance of accuracy, robustness, and computational efficiency, making it an excellent choice for distinguishing between Glioma, Meningioma, Pituitary Tumor, and healthy brain MRI images.


