# AD32231: Deep Learning
## Unit II: Optimization and Regularization in Deep Learning
### Course Outcome 2 (CO2): Apply loss functions, optimize using gradient descent variants, and implement regularization techniques.

---

## 2.1 Loss Functions

### What is a Loss Function?
A **loss function** (also called a cost function or error function) measures **how wrong** a model's predictions are compared to the actual correct answers.

The goal of training is to **minimize the loss** — the smaller the loss, the better the model.

**Analogy:**
> Imagine you're throwing darts at a target. The loss function measures how far each dart lands from the bullseye. Your job is to adjust your throw (weights) so darts land closer to center.

---

### Loss Function Notation
- `y` = actual (true) value
- `ŷ` (y-hat) = predicted value
- `n` = number of samples
- `L` or `J` = loss value

---

### 2.1.1 Loss Functions for Regression

Regression tasks predict **continuous values** (e.g., house prices, temperature).

#### 1. Mean Squared Error (MSE)
- **Formula:** `MSE = (1/n) × Σ(y - ŷ)²`
- Squares the error, so **large errors are penalized more**
- Sensitive to outliers
- **Example:** Predicting house price
  - Actual: ₹50 Lakhs, Predicted: ₹45 Lakhs
  - Error = (50-45)² = 25

#### 2. Mean Absolute Error (MAE)
- **Formula:** `MAE = (1/n) × Σ|y - ŷ|`
- Treats all errors equally (no squaring)
- More **robust to outliers** than MSE
- **Example:** Actual: 50, Predicted: 45 → Error = |50-45| = 5

#### 3. Huber Loss
- **Combines** MSE and MAE
- Uses MSE for small errors, MAE for large errors (outliers)
- Best of both worlds!

---

### 2.1.2 Loss Functions for Classification

Classification tasks predict **categories** (e.g., spam/not spam, cat/dog/bird).

#### 1. Binary Cross-Entropy Loss
- Used when there are **2 classes** (Yes/No, 0/1)
- **Formula:** `L = -[y × log(ŷ) + (1-y) × log(1-ŷ)]`
- **Example:** Is this email spam?
  - Actual: 1 (spam), Predicted: 0.9 → Low loss (confident and correct)
  - Actual: 1 (spam), Predicted: 0.1 → High loss (confident but WRONG!)

#### 2. Categorical Cross-Entropy
- Used when there are **multiple classes**
- **Formula:** `L = -Σ(y × log(ŷ))`
- Usually paired with **Softmax** output
- **Example:** Classifying animals (cat, dog, bird)
  - Actual: cat → [1, 0, 0], Predicted: [0.8, 0.1, 0.1] → Low loss ✓

#### Key Insight:
> Cross-Entropy **heavily penalizes** confident wrong predictions.
> Saying "I'm 99% sure it's a cat" when it's actually a dog is much worse than saying "I'm 51% sure it's a cat."

---

### 2.1.3 Loss Functions for Reconstruction

Used in **autoencoders** where the goal is to reconstruct the input.

#### 1. MSE Reconstruction Loss
- Measures pixel-by-pixel difference between original and reconstructed image
- `L = (1/n) × Σ(original_pixel - reconstructed_pixel)²`

#### 2. Binary Cross-Entropy Reconstruction Loss
- Used when pixel values are between 0 and 1
- Treats each pixel as a binary classification problem

---

## 2.2 Gradient Descent and its Variants

### What is Gradient Descent?
**Gradient Descent** is the core optimization algorithm used to train neural networks — it's the method that **adjusts weights** to minimize the loss function.

**Analogy:**
> Imagine you're blindfolded on a hilly terrain and want to reach the lowest point (minimum loss). You feel the slope under your feet (gradient) and take a step in the downhill direction. Repeat until you reach the bottom.

**Update Rule:**
```
new_weight = old_weight - learning_rate × gradient
```
- **Learning Rate (α):** How big a step you take. Too large = overshoot. Too small = very slow.
- **Gradient:** The slope of the loss function at current weights (which direction is downhill)

---

### Types of Gradient Descent:

#### 1. Batch Gradient Descent (BGD)
- Uses the **entire dataset** to compute gradient before updating
- **Pros:** Stable, accurate gradient
- **Cons:** Very slow for large datasets, memory-intensive
- **Example:** 1 million training samples → compute gradient on all 1M before 1 update

#### 2. Stochastic Gradient Descent (SGD)
- Updates weights after **each single sample**
- **Pros:** Fast, good for large datasets
- **Cons:** Very noisy updates, may jump around a lot

```
For each sample:
  compute gradient
  update weights
```

#### 3. Mini-Batch Gradient Descent ⭐ Most Used
- Divides data into **small batches** (e.g., 32, 64, 128 samples)
- Updates weights after processing each mini-batch
- **Best balance** between speed and stability

```
For each mini-batch of 32 samples:
  compute gradient
  update weights
```

---

### Advanced Optimizers:

#### 4. Momentum
- Adds a **velocity** term to gradient descent
- Keeps track of previous gradients and continues in that direction
- Helps overcome small bumps and noisy gradients
- Analogy: Like a ball rolling downhill — it gains momentum and doesn't stop at every small bump

```
velocity = momentum × old_velocity - learning_rate × gradient
weight = weight + velocity
```

#### 5. RMSprop (Root Mean Square Propagation)
- Adapts the learning rate for **each weight individually**
- Divides learning rate by a moving average of squared gradients
- Works well for **non-stationary** problems (gradients change a lot)
- Good for RNNs

#### 6. Adam (Adaptive Moment Estimation) ⭐ Most Popular Optimizer
- Combines **Momentum** + **RMSprop**
- Maintains both:
  - First moment (mean of gradients) → like momentum
  - Second moment (variance of gradients) → like RMSprop
- Adapts learning rate for each weight
- Works well in most situations with minimal tuning

**Why Adam is popular:**
- Handles sparse gradients
- Works well out of the box
- Converges faster

#### Optimizer Comparison:

| Optimizer | Speed | Stability | Memory | Use Case |
|---|---|---|---|---|
| BGD | Slow | Very Stable | High | Small datasets |
| SGD | Fast | Noisy | Low | Large datasets |
| Mini-batch SGD | Balanced | Good | Medium | General use |
| Momentum | Faster | Better | Low | Smooth loss surfaces |
| RMSprop | Fast | Good | Medium | RNNs, NLP |
| Adam | Fast | Good | Medium | Most DL tasks ⭐ |

---

## 2.3 Hyperparameter Tuning

**Hyperparameters** are settings you configure **before** training — the model does NOT learn these automatically.

Contrast with **Parameters** (weights, biases) which the model learns during training.

### Key Hyperparameters:

#### 1. Learning Rate (α)
- Controls how fast the model learns (how big each weight update step is)
- Most important hyperparameter!

| Learning Rate | Effect |
|---|---|
| Too large (e.g., 1.0) | Overshoots minimum, loss may increase (diverges) |
| Too small (e.g., 0.0001) | Very slow learning, may get stuck |
| Just right (e.g., 0.001) | Smooth convergence to minimum |

**Techniques for setting Learning Rate:**
- **Learning Rate Schedule:** Decrease LR over time (start fast, slow down)
- **Learning Rate Finder:** Try different LRs, pick the one with fastest loss decrease

#### 2. Batch Size
- Number of samples processed before weights are updated
- Small batch (8-32): Noisy but good generalization
- Large batch (256-512): Stable but may overfit
- Common values: **32, 64, 128**

#### 3. Epochs
- One **epoch** = one complete pass through the entire training dataset
- Too few epochs → underfitting (model hasn't learned enough)
- Too many epochs → overfitting (model memorizes training data)
- **Early Stopping:** Stop training when validation loss stops improving

```
Training for 100 epochs:
Epoch 1: Training Loss=2.1, Val Loss=2.3
Epoch 50: Training Loss=0.5, Val Loss=0.6  ← Good!
Epoch 100: Training Loss=0.1, Val Loss=1.8  ← Overfitting!
```

---

## 2.4 Vanishing and Exploding Gradient Problems

These are critical problems that can prevent deep neural networks from learning.

### Vanishing Gradient Problem
- During backpropagation, gradients are **multiplied** as they move backward through layers
- If gradients are small (< 1), repeated multiplication makes them **exponentially smaller**
- Layers near the input receive **near-zero gradients** → weights barely update → those layers don't learn

**Why it happens:** Sigmoid and Tanh activation functions have gradients between 0 and 0.25, causing gradients to shrink with each layer.

**Example:**
```
Gradient at output: 0.5
After layer 3: 0.5 × 0.2 = 0.1
After layer 2: 0.1 × 0.2 = 0.02
After layer 1: 0.02 × 0.2 = 0.004 ← basically zero!
```

**Solutions:**
- Use **ReLU** instead of Sigmoid/Tanh
- Use **Batch Normalization**
- Use **Residual connections** (ResNet)
- Better weight initialization (Xavier, He)

### Exploding Gradient Problem
- Opposite problem: gradients become **exponentially large**
- Weights get huge updates → model becomes unstable → loss goes to infinity (NaN)

**Common in:** RNNs with long sequences

**Solutions:**
- **Gradient Clipping:** Cap the gradient at a maximum value (e.g., clip at 5.0)
- Better weight initialization
- Use LSTM/GRU instead of vanilla RNN

---

## 2.5 Regularization Techniques

**Regularization** helps prevent **overfitting** — where the model performs well on training data but poorly on new, unseen data.

**Overfitting Analogy:**
> A student memorizes all exam questions and answers perfectly. But when asked a new question, they fail because they memorized instead of understanding.

---

### 2.5.1 Dropout
**What it is:** During training, randomly "drop out" (set to zero) a fraction of neurons.

**How it works:**
- Each neuron has a probability `p` of being dropped (e.g., p=0.5 means 50% chance of being dropped)
- Different neurons are dropped each batch
- Forces the network to **not rely on any single neuron**
- At test time: all neurons are active, but outputs are scaled

**Example:**
```
Without Dropout:
Layer: [n1=0.8, n2=0.6, n3=0.9, n4=0.3]

With Dropout (p=0.5):
Layer: [n1=0.0, n2=0.6, n3=0.0, n4=0.3]  ← n1, n3 dropped!
```

**Benefits:**
- Prevents overfitting
- Acts like training many different networks simultaneously (ensemble effect)
- Common dropout rates: 0.2–0.5

**Code:**
```python
model = tf.keras.Sequential([
    tf.keras.layers.Dense(128, activation='relu'),
    tf.keras.layers.Dropout(0.5),  # Drop 50% of neurons
    tf.keras.layers.Dense(10, activation='softmax')
])
```

---

### 2.5.2 Batch Normalization
**What it is:** Normalizes the **output of each layer** (zero mean, unit variance) before passing to the next layer.

**Why it helps:**
- Reduces internal covariate shift (inputs to each layer keep changing during training)
- Allows higher learning rates → faster training
- Acts as a mild regularizer (reduces need for dropout)
- Helps with vanishing/exploding gradient problem

**How it works:**
```
For each batch:
1. Compute mean (μ) of the batch
2. Compute variance (σ²) of the batch
3. Normalize: x_normalized = (x - μ) / sqrt(σ² + ε)
4. Scale and shift: output = γ × x_normalized + β
   (γ and β are learnable parameters)
```

**Analogy:**
> Like standardizing exam scores so that every class has scores in the same range, regardless of how hard the exam was.

---

### 2.5.3 Weight Decay (L2 Regularization)
**What it is:** Adds a penalty to the loss function for having **large weights**.

**Formula:**
```
Total Loss = Original Loss + λ × Σ(weight²)
```
- `λ` (lambda) is the regularization strength
- Large weights are penalized → model prefers smaller weights
- Smaller weights = simpler model = less overfitting

**L1 Regularization:** Similar but uses absolute value instead of square:
```
Total Loss = Original Loss + λ × Σ|weight|
```
L1 can drive weights to **exactly zero** (feature selection effect)

### Comparison of Regularization Techniques:

| Technique | How it Works | Best Used When |
|---|---|---|
| Dropout | Randomly disables neurons | Deep networks, overfitting |
| Batch Normalization | Normalizes layer outputs | Deep networks, training instability |
| Weight Decay (L2) | Penalizes large weights | General regularization |
| L1 | Penalizes sum of weights | Feature selection needed |
| Early Stopping | Stop when val loss increases | Any network |

---

## Unit II Summary

| Topic | Key Takeaway |
|---|---|
| MSE | Regression loss; squares errors |
| Cross-Entropy | Classification loss; penalizes confident wrong predictions |
| Gradient Descent | Adjust weights by going downhill on loss surface |
| Adam | Most popular optimizer; combines momentum + RMSprop |
| Learning Rate | Most important hyperparameter; too high or low causes problems |
| Batch Size | 32-128 is typical; trade-off between speed and stability |
| Epochs | Too many → overfitting; use early stopping |
| Vanishing Gradient | Gradients shrink → early layers don't learn; fix with ReLU, BN |
| Exploding Gradient | Gradients blow up → fix with gradient clipping |
| Dropout | Randomly deactivate neurons to prevent overfitting |
| Batch Normalization | Normalize layer outputs for stable, fast training |
| Weight Decay | Penalize large weights to keep model simple |

---
*End of Unit II*
