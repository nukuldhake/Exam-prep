# AD32231: Deep Learning
## Unit III: Convolutional Neural Networks (CNN)
### Course Outcome 3 (CO3): Design and train CNNs for image tasks, implement transfer learning, and apply object detection algorithms.

---

## 3.1 Motivation for CNNs in Image Processing

### Why not just use regular (Fully Connected) Neural Networks for images?

Consider a small 64×64 pixel grayscale image:
- Number of input neurons = 64 × 64 = **4,096**
- If first hidden layer has 1,000 neurons: **4,096 × 1,000 = 4 million parameters!**
- For color images (3 channels) at 224×224: **150,528 inputs!**

**Problems with using plain ANN for images:**
1. **Too many parameters** → computationally expensive, slow
2. **No spatial awareness** → doesn't understand that nearby pixels are related
3. **Not translation invariant** → if a cat moves to a different corner of the image, ANN may not recognize it

### How CNNs Solve These Problems:
- **Local connectivity:** Each neuron only looks at a small region (patch) of the image
- **Parameter sharing:** The same filter is applied across the entire image → fewer parameters
- **Hierarchical feature learning:** Early layers detect edges, later layers detect shapes and objects

**Analogy:**
> Instead of looking at a painting all at once (overwhelming), CNNs look at it through a small sliding window, scanning for patterns piece by piece.

---

## 3.2 CNN Architecture

A typical CNN consists of:
```
Input Image → [CONV → ReLU → POOL] × N → Flatten → FC Layers → Output
```

### 3.2.1 Convolution Layer

**What it does:** Slides a small filter (also called a kernel) over the image and computes a dot product at each position.

**Filter/Kernel:** A small matrix of learnable weights (e.g., 3×3 or 5×5)

**Example: Edge Detection**
```
Image patch:       Filter (edge detector):   Result:
[10, 10, 10]      [-1, -1, -1]
[10, 10, 10]  ×   [ 0,  0,  0]   →   large value (edge found!)
[0,  0,  0 ]      [ 1,  1,  1]
```

**Key Terms:**
- **Stride:** How many pixels the filter moves at each step. Stride=1 → move 1 pixel. Stride=2 → skip 1 pixel.
- **Padding:** Adding zeros around the border of the image. Keeps output size same as input.
  - 'Valid' padding: No padding, output is smaller
  - 'Same' padding: Zero-pad so output size = input size

**Output Size Formula:**
```
Output Size = (Input Size - Filter Size + 2 × Padding) / Stride + 1
```
Example: Input=32, Filter=3, Padding=0, Stride=1 → Output = (32-3+0)/1 + 1 = 30

---

### 3.2.2 Feature Maps
- After applying a filter to the input image, we get a **feature map** (also called activation map)
- Each filter detects a **different feature** (e.g., vertical edges, horizontal edges, curves)
- With 32 filters, we get 32 feature maps!

```
Input Image → Filter 1 → Feature Map 1 (detects horizontal edges)
            → Filter 2 → Feature Map 2 (detects vertical edges)
            → Filter 3 → Feature Map 3 (detects diagonals)
            ...
```

As we go deeper in the network:
- Early layers detect: **edges, colors, gradients**
- Middle layers detect: **shapes, textures, patterns**
- Deep layers detect: **objects, faces, complete structures**

---

### 3.2.3 Pooling Layers

**What it does:** Reduces the **spatial size** of the feature maps (downsampling).

**Why pool?**
1. Reduces computation
2. Reduces number of parameters
3. Provides a degree of **translation invariance** (feature detected even if slightly shifted)

#### Max Pooling ⭐ Most Common
- Takes the **maximum value** from each pooling window
- Preserves the most prominent feature

```
Input (4×4):          Max Pool (2×2, stride=2):   Output (2×2):
[1, 3, 2, 4]          [max(1,3,5,9)=9, max(2,4,7,2)=7]
[5, 9, 7, 2]    →     [max(4,3,1,2)=4, max(1,5,8,3)=8]
[4, 3, 1, 5]
[2, 1, 8, 3]
```

#### Average Pooling
- Takes the **average value** from each pooling window
- Less common than max pooling
- Used in some architectures like GoogLeNet for the final pooling layer

---

### 3.2.4 Fully Connected Layers (FC Layers)
- After several CONV and POOL layers, the feature maps are **flattened** into a 1D vector
- This vector is passed through regular fully connected (dense) layers
- The final FC layer produces the output (class probabilities using Softmax)

```
Feature Map (7×7×512) → Flatten → [25,088 neurons] → FC(4096) → FC(4096) → FC(1000, softmax)
```

---

## 3.3 Classic CNN Architectures

### 3.3.1 AlexNet (2012) — The Game Changer
- **Created by:** Alex Krizhevsky, Ilya Sutskever, Geoffrey Hinton
- **Achievement:** Won ImageNet competition in 2012 with huge margin → sparked the deep learning revolution
- **Architecture:** 5 CONV layers + 3 FC layers
- **Innovations introduced:**
  - ReLU activation (instead of Sigmoid/Tanh)
  - Dropout regularization
  - Data augmentation
  - GPU training

```
Architecture:
Input(227×227×3) → CONV1(96 filters, 11×11) → Pool → CONV2 → Pool → CONV3 → CONV4 → CONV5 → Pool → FC1 → FC2 → Output(1000)
```

---

### 3.3.2 VGGNet (2014) — Simple but Deep
- **Created by:** Visual Geometry Group, Oxford University
- **Key idea:** Use **very small filters (3×3)** but go very **deep (16-19 layers)**
- Two main versions: **VGG-16** (16 layers) and **VGG-19** (19 layers)
- **Why small filters?** Two 3×3 filters have the same effective receptive field as one 5×5 filter, but fewer parameters

**Architecture Pattern:**
```
[CONV 3×3, CONV 3×3, Pool] × 2 → [CONV 3×3, CONV 3×3, CONV 3×3, Pool] × 3 → FC × 3 → Output
```

**Pros:** Simple, uniform architecture; great features for transfer learning
**Cons:** Very slow, 138 million parameters (huge!)

---

### 3.3.3 ResNet (Residual Networks, 2015) — The Skip Connection Revolution
- **Created by:** Microsoft Research (He et al.)
- **Achievement:** Won ImageNet 2015; introduced networks with **152 layers!**
- **Problem it solved:** Deeper networks were performing WORSE due to vanishing gradients

**Key Innovation: Residual / Skip Connections**
```
Normal layer:   output = F(input)
Residual layer: output = F(input) + input   ← Add the input directly!
```

**Why this helps:**
- If the layer learns nothing useful (F(input) ≈ 0), the output is at least equal to the input
- Gradients can flow **directly** through skip connections → no vanishing gradient!

**Analogy:**
> Like a highway with express lanes — even if a local road is jammed, you can still travel via the express lane.

```
ResNet Block:
input → CONV → BN → ReLU → CONV → BN → (+input) → ReLU → output
         └────────────────────────────────────┘
                    Skip connection
```

**Variants:** ResNet-18, ResNet-34, ResNet-50, ResNet-101, ResNet-152

---

## 3.4 Transfer Learning and Fine-Tuning

### What is Transfer Learning?
**Transfer Learning** means taking a model that was trained on a **large dataset** (like ImageNet with 1.2 million images) and reusing it for a **different but related task**.

**Why use it?**
- Training a deep CNN from scratch requires:
  - Millions of labeled images
  - Days/weeks of training on expensive GPUs
- With transfer learning: achieve great results with **small datasets in hours!**

**Analogy:**
> You already know how to ride a bicycle. Learning to ride a motorbike is much easier because many skills transfer (balance, steering). You don't start from zero.

### How Transfer Learning Works:

**Step 1:** Take a pre-trained model (e.g., ResNet-50 trained on ImageNet)

**Step 2:** Remove the final output layer (it was designed for 1000 classes)

**Step 3 — Feature Extraction:**
- Freeze all existing layers (don't train them)
- Add new output layers for your task (e.g., 5 skin disease classes)
- Only train the new layers

**Step 4 — Fine-Tuning (optional, more advanced):**
- Unfreeze some of the later layers
- Train them with a very small learning rate
- Adjusts the pre-trained features for your specific task

```
Pre-trained ResNet → [Frozen Layers] → [New FC Layer] → [Your Output]
                          ↑
                     Don't update          Update!
```

### When to use what:
| Scenario | Approach |
|---|---|
| Small dataset, similar to ImageNet | Feature Extraction (freeze all) |
| Small dataset, different from ImageNet | Feature Extraction from early layers |
| Large dataset, similar to ImageNet | Fine-tune later layers |
| Large dataset, very different | Train from scratch |

**Popular pre-trained models available in Keras/PyTorch:**
- VGG16, VGG19
- ResNet50, ResNet101
- MobileNet, EfficientNet
- InceptionV3

---

## 3.5 Object Detection

**Image Classification:** "Is there a cat in this image?" → Yes/No + class label
**Object Detection:** "Where is the cat? Draw a box around it." → Class label + bounding box coordinates

---

### 3.5.1 R-CNN (Region-based CNN, 2014)
**How it works:**
1. Use a traditional algorithm (Selective Search) to propose ~2000 candidate regions
2. Warp each region to fixed size
3. Pass each region through a CNN to extract features
4. Classify each region with SVM

**Problem:** Very slow! ~47 seconds per image (because CNN runs 2000 times!)

**Fast R-CNN:** Feed the entire image through CNN ONCE, then extract region features from the feature map (much faster)

**Faster R-CNN:** Use a **Region Proposal Network (RPN)** instead of Selective Search — end-to-end trainable, real-time possible

---

### 3.5.2 YOLO (You Only Look Once, 2016) ⭐
**Key Idea:** Instead of region proposals, look at the **whole image at once** in a single forward pass.

**How YOLO works:**
1. Divide image into an S×S grid (e.g., 13×13)
2. Each grid cell predicts:
   - B bounding boxes (x, y, width, height)
   - Confidence score for each box
   - Class probabilities
3. Use Non-Maximum Suppression (NMS) to remove duplicate detections

**Why YOLO is amazing:**
- **Speed:** 45–155 frames per second (real-time!)
- **End-to-end:** Single neural network for the entire detection pipeline
- Used in autonomous vehicles, surveillance, drone detection

**Versions:** YOLOv1 → YOLOv3 → YOLOv5 → YOLOv8 (each version faster and more accurate)

---

### 3.5.3 SSD (Single Shot Detector, 2016)
- Like YOLO, makes predictions in a single forward pass
- Predicts detections at **multiple scales** (good for detecting objects of different sizes)
- More accurate than YOLO (original) on small objects
- Faster than R-CNN family

**Comparison:**

| Algorithm | Speed | Accuracy | Architecture |
|---|---|---|---|
| R-CNN | Very Slow | High | 2-stage |
| Fast R-CNN | Moderate | High | 2-stage |
| Faster R-CNN | Fast | Very High | 2-stage |
| YOLO | Very Fast | Good | 1-stage |
| SSD | Fast | Good | 1-stage |

---

## 3.6 Applications of CNNs

### Image Classification
- Classify images into categories
- Example: Is this image a cat, dog, or bird?
- Used in: Google Photos, Instagram filters

### Medical Imaging
- **Chest X-ray analysis:** Detecting pneumonia, COVID-19
- **Skin lesion classification:** Melanoma detection
- **Retinal scan analysis:** Diabetic retinopathy detection
- **Brain MRI:** Tumor detection
- CNN can match or exceed radiologist performance in some tasks!

### Other Applications:
- **Autonomous Vehicles:** Object detection (pedestrians, cars, signs)
- **Face Recognition:** Security systems, phone unlock
- **Agricultural Monitoring:** Detecting plant diseases from drone images
- **Document Analysis:** Optical Character Recognition (OCR)
- **Quality Control:** Defect detection in manufacturing

---

## Unit III Summary

| Topic | Key Takeaway |
|---|---|
| Why CNN? | Regular ANNs can't scale to images; CNNs use local connectivity and parameter sharing |
| Convolution | Slide a filter over image, detect local patterns |
| Feature Maps | Output of applying filters; show where features are detected |
| Max Pooling | Take max in each window; reduce size, keep strongest feature |
| AlexNet | First big CNN success; introduced ReLU, dropout |
| VGGNet | Deep network with small 3×3 filters; simple and effective |
| ResNet | Skip connections solve vanishing gradient; enables very deep networks |
| Transfer Learning | Reuse pre-trained models for new tasks; saves data and compute |
| R-CNN | Region proposals + CNN; accurate but slow |
| YOLO | Single-pass detection; real-time, end-to-end |
| SSD | Multi-scale single-pass detection |
| Medical Imaging | CNN excels at detecting patterns in X-rays, MRIs, skin images |

---
*End of Unit III*
