# AD32231: Deep Learning
## Unit V: Deep Generative Models
### Course Outcome 5 (CO5): Implement generative models like VAEs and GANs, understand BERT/GPT architecture, and apply explainability techniques.

---

## 5.1 Introduction to Deep Generative Models

### What are Generative Models?
**Discriminative models** (like classifiers) learn to distinguish between classes:
- Input → Label (Is this a cat or a dog?)

**Generative models** learn the **underlying distribution of the data** and can:
- Generate new, realistic samples (e.g., create new images of faces that don't exist)
- Understand data structure and representation

**Analogy:**
> A discriminative model is like a judge who knows good vs bad art.
> A generative model is like an artist who can CREATE new art.

### Types of Generative Models covered:
1. **Autoencoders (AE)**
2. **Variational Autoencoders (VAE)**
3. **Generative Adversarial Networks (GANs)**
4. **Boltzmann Machines**
5. **Deep Belief Networks (DBNs)**
6. **Transformers + BERT**

---

## 5.2 Autoencoders (AE)

### What is an Autoencoder?
An Autoencoder is a neural network trained to **reconstruct its input** at the output.

```
Input X → Encoder → Latent Vector z (compressed) → Decoder → Output X̂ ≈ X
```

The network is forced to learn a **compressed representation** (bottleneck) of the data.

### Architecture:
```
Input(784) → Dense(256) → Dense(64) → [Latent z: 32] → Dense(64) → Dense(256) → Output(784)
             ←─── Encoder ────────────────────────────────── Decoder ───────────────────────→
```

### What does the Latent Vector learn?
The latent space captures the **most important features** of the data.
- Example: For face images, latent dimensions might encode gender, age, hair color, expression — even without labels!

### Loss Function:
```
Reconstruction Loss = MSE(X, X̂)   or   Binary Cross-Entropy(X, X̂)
```
Goal: Make X̂ as close to X as possible.

### Applications:
- **Dimensionality Reduction:** Like PCA but non-linear
- **Anomaly Detection:** Normal data reconstructs well; anomalies have high reconstruction error
  - Example: Detect fraudulent transactions (they reconstruct poorly)
- **Image Denoising:** Train with noisy input, clean image as target
- **Feature Learning:** Extract useful features for downstream tasks
- **Data Compression:** Compress images/audio

### Limitation:
- The latent space is NOT continuous or structured
- You can't randomly sample from it to generate meaningful new data
- Solution: Variational Autoencoder (VAE)

---

## 5.3 Variational Autoencoders (VAE)

### What's different from regular AE?
In a regular AE, the encoder maps input to a **single point** in latent space.

In a VAE, the encoder maps input to a **distribution** (mean μ and variance σ²):
- Encoder outputs: `μ (mean)` and `σ² (variance)` for each latent dimension
- We **sample** from this distribution: `z = μ + σ × ε` (where ε is random noise)

```
Input X → Encoder → [μ, σ²] → Sample z ~ N(μ, σ²) → Decoder → Output X̂
```

### Why this matters:
- The latent space is now **continuous and smooth**
- You can sample ANY point from the distribution and the decoder generates a meaningful output
- Nearby points in latent space produce similar outputs (interpolation works!)

### VAE Loss Function:
```
VAE Loss = Reconstruction Loss + KL Divergence
```
- **Reconstruction Loss:** How well does the output match the input?
- **KL Divergence:** How close is the learned distribution to a standard normal distribution N(0,1)?
  - Forces the latent space to be organized and smooth

**Analogy:**
> Regular AE is like a messy closet — you can find your stuff, but can't easily search between locations.
> VAE is like an organized closet — everything is in a predictable place, and between two items you'll find something in-between.

### Applications:
- Generating new realistic images (faces, handwriting)
- **Image interpolation:** Blend between two images smoothly
- Data augmentation
- Drug molecule generation (pharmaceutical research)

---

## 5.4 Generative Adversarial Networks (GANs)

### The Big Idea
Introduced by **Ian Goodfellow et al. (2014)** — one of the most exciting ideas in deep learning!

A GAN has **two neural networks** competing against each other:

1. **Generator (G):** Creates fake data (like a counterfeiter making fake currency)
2. **Discriminator (D):** Judges whether data is real or fake (like a police officer detecting fake currency)

### The Adversarial Game:
```
Random Noise (z) → [Generator G] → Fake Image
                                         ↓
Real Images ─────────────────────→ [Discriminator D] → Real or Fake?
```

**Generator** tries to fool the Discriminator: "My fake image should look real!"
**Discriminator** tries to catch the Generator: "This looks fake because..."

Both improve over time through competition until the Generator creates perfectly realistic images!

**Analogy:**
> Counterfeiters (Generator) keep making better fake bills, while detectives (Discriminator) keep getting better at detecting fakes. Eventually, the fake bills are indistinguishable from real ones.

### GAN Training Algorithm:
```
Repeat for each epoch:
  Step 1: Train Discriminator
    - Feed real images → D should output 1 (real)
    - Feed fake images from G → D should output 0 (fake)
    - Update D weights

  Step 2: Train Generator
    - Feed noise z → G creates fake image
    - Feed fake image to D → we want D to output 1 (fooled!)
    - If D is fooled, Generator is doing well
    - Update G weights (but NOT D weights in this step)
```

### Loss Functions:
**Discriminator Loss:**
```
L_D = -[log(D(real)) + log(1 - D(G(z)))]
```
Maximize the chance of correctly classifying real as real and fake as fake.

**Generator Loss:**
```
L_G = -log(D(G(z)))
```
Maximize the chance of fooling the Discriminator (make D(G(z)) close to 1).

### GAN Training Challenges:
1. **Mode Collapse:** Generator produces only a few types of outputs (e.g., only one digit when trained on MNIST)
   - Solution: Wasserstein GAN (WGAN), spectral normalization
2. **Non-convergence:** Training oscillates, never stabilizes
3. **Vanishing Gradient for Generator:** If Discriminator is too good early on
4. **Hyperparameter sensitivity:** Very sensitive to learning rate and architecture choices

### Famous GAN Variants:

| GAN Variant | Key Innovation | Application |
|---|---|---|
| DCGAN (2015) | Uses CNN in G and D | Image generation |
| CGAN (2014) | Condition on class label | Controlled generation |
| CycleGAN (2017) | Unpaired image translation | Horse → Zebra, Photos → Art |
| StyleGAN (2019) | Style-based generator | Ultra-realistic faces (thispersondoesnotexist.com) |
| WGAN | Wasserstein distance loss | Stable training |

### GAN Applications:
- **Image Generation:** Create photorealistic images of non-existent people
- **Image-to-Image Translation:** CycleGAN (day → night, summer → winter)
- **Data Augmentation:** Generate synthetic training data
- **Super-Resolution:** Enhance low-resolution images (SRGAN)
- **Deep Fakes:** (Also a concern for misuse)
- **Drug Discovery:** Generate molecular structures

---

## 5.5 Boltzmann Machines

### What is a Boltzmann Machine?
A **Boltzmann Machine** is an **energy-based model** — a type of probabilistic neural network.

- Consists of **visible units** (v) — the data we observe
- And **hidden units** (h) — latent representations

All units can be connected to each other (including hidden-to-hidden).

**Energy function:**
```
E(v, h) = -Σ b_i × v_i - Σ c_j × h_j - Σ W_ij × v_i × h_j
```
Lower energy = more likely state.

**Problem:** Full Boltzmann Machines are computationally intractable (too many connections).

### Restricted Boltzmann Machine (RBM)
**Restriction:** No connections **within** the same layer (no visible-to-visible or hidden-to-hidden connections).

```
Visible:  v1 -- v2 -- v3 -- v4
           |  × |  × |  × |
Hidden:   h1 -- h2 -- h3
```
(Full connections BETWEEN layers but not within)

**Training:** Contrastive Divergence (CD) algorithm

**Applications:**
- Collaborative filtering (Netflix-style recommendation)
- Feature learning
- Dimensionality reduction
- Building blocks for Deep Belief Networks

---

## 5.6 Deep Belief Networks (DBN)

### What is a DBN?
A **Deep Belief Network** is a stack of **Restricted Boltzmann Machines**.

```
Data → [RBM 1] → [RBM 2] → [RBM 3] → Output
```

**Training Process (Greedy Layer-wise Pretraining):**
1. Train RBM 1 on raw data
2. Use hidden states of RBM 1 as input, train RBM 2
3. Use hidden states of RBM 2 as input, train RBM 3
4. Fine-tune all layers together using backpropagation

**Historical Significance:**
- DBNs (by Geoffrey Hinton, 2006) helped revive interest in deep learning!
- Showed that deep networks CAN be trained effectively
- Paved the way for modern deep learning

**Applications:**
- Image recognition (pre-CNN era)
- Speech recognition
- Feature learning for pre-training

---

## 5.7 Transformers and Self-Attention Mechanism

### The Problem with RNNs:
1. **Sequential processing:** Can't process all words simultaneously (slow!)
2. **Long-range dependency:** Still struggles even with LSTM for very long sequences
3. **Fixed context vector:** Seq2Seq bottleneck loses information

### The Attention Mechanism
Before Transformers, **Attention** was added to Seq2Seq models to help the Decoder focus on relevant parts of the Encoder's hidden states.

```
Instead of: Encoder → One context vector → Decoder
Now:        Encoder → All hidden states → Decoder uses attention to pick relevant states at each step
```

**Example:** Translating "The cat sat on the mat" → French
- When generating "chat" (cat), model attends strongly to "cat" in input
- When generating "assis" (sat), model attends to "sat"

### Self-Attention
The key innovation of Transformers: A word can attend to **all other words in the same sequence** to understand context.

**For the word "bank" in "I went to the bank to deposit money":**
- "bank" attends to "deposit" and "money" → high attention weights
- Determines that this is a financial institution, not a river bank

**Self-Attention Computation (Scaled Dot-Product Attention):**
```
Step 1: Create 3 vectors for each word:
  - Query (Q): "What am I looking for?"
  - Key (K): "What do I offer?"
  - Value (V): "What information do I carry?"

Step 2: Compute attention scores:
  Score = Q × K^T / √d_k   (d_k = dimension of key vectors)

Step 3: Apply Softmax to get attention weights (sum to 1)

Step 4: Weighted sum of Values:
  Output = softmax(Q × K^T / √d_k) × V
```

**Multi-Head Attention:** Run self-attention multiple times in parallel (different "heads"), then concatenate results. Each head can learn different types of relationships.

### The Transformer Architecture (2017, "Attention is All You Need")
```
                    OUTPUT PROBABILITIES
                           ↑
                    [Linear + Softmax]
                           ↑
               ┌─── Decoder Block × 6 ───┐
               │   Multi-Head Attention   │
               │   Cross-Attention (to    │
               │   encoder output)        │
               │   Feed Forward           │
               └─────────────────────────┘
                           ↑
               ┌─── Encoder Block × 6 ───┐
               │   Multi-Head Self-Attn  │
               │   Feed Forward          │
               │   Add & Norm            │
               └─────────────────────────┘
                           ↑
                  Input Embeddings +
                  Positional Encoding
                           ↑
                      INPUT TOKENS
```

**Key Components:**
- **Positional Encoding:** Since Transformer processes all words in parallel, we need to add position information (word order)
- **Multi-Head Attention:** Multiple attention heads capture different relationships
- **Feed Forward:** Simple dense network applied to each position independently
- **Add & Norm:** Residual connection + Layer Normalization for stable training

**Why Transformers are revolutionary:**
- **Parallelizable:** All words processed simultaneously (unlike RNNs)
- **Long-range attention:** Every word directly attends to every other word
- **Scalable:** Works amazingly well with more data and larger models

---

## 5.8 Introduction to BERT

### What is BERT?
**BERT = Bidirectional Encoder Representations from Transformers**
- Released by **Google AI (2018)**
- Uses only the **Encoder** part of the Transformer
- Pre-trained on massive text data (Wikipedia + BookCorpus)
- Fine-tuned for specific NLP tasks

### Why "Bidirectional"?
Earlier models (like GPT-1) processed text left-to-right only.
BERT reads text in **BOTH directions simultaneously** → much better understanding of context.

**Example:** "He [MASK] the bank after withdrawing money"
- Bidirectional: Uses both left ("He") and right ("after withdrawing money") context
- Correctly predicts [MASK] = "left"

### How BERT is Pre-trained:

#### Task 1: Masked Language Model (MLM)
- Randomly mask 15% of words in a sentence
- Train model to predict the masked words
- Forces model to understand bidirectional context

```
Input:  "The [MASK] sat on the mat."
Target: "cat"
```

#### Task 2: Next Sentence Prediction (NSP)
- Given 2 sentences, predict if sentence B follows sentence A in the original text
- Helps understand sentence relationships

```
Input:  [CLS] "The cat sat." [SEP] "It was tired." [SEP]
Label:  IsNext = True

Input:  [CLS] "The cat sat." [SEP] "Python is a language." [SEP]
Label:  IsNext = False
```

### BERT Input Representation:
```
[CLS] token + sentence + [SEP] token
Token Embedding + Segment Embedding + Positional Embedding
```

### Fine-tuning BERT for Downstream Tasks:
After pre-training, add a small task-specific layer and fine-tune on labeled data:

| Task | Fine-tuning Approach |
|---|---|
| Sentiment Classification | Use [CLS] token representation |
| Question Answering | Predict start/end position of answer |
| Named Entity Recognition | Classify each token |
| Text Similarity | Compare [CLS] embeddings |

### BERT vs GPT:

| Feature | BERT | GPT |
|---|---|---|
| Architecture | Encoder only | Decoder only |
| Direction | Bidirectional | Left-to-right |
| Pre-training | MLM + NSP | Language Modeling |
| Best for | Understanding (classification, NER, QA) | Generation (text, code) |
| Examples | BERT-base, RoBERTa, ALBERT | GPT-2, GPT-3, GPT-4 |

---

## 5.9 Explainability Techniques for Deep Learning

### Why do we need Explainability?
Deep learning models are often called **"black boxes"** — they give answers but can't easily explain WHY.

**Problems with black boxes:**
- A medical AI diagnoses cancer → Doctor needs to know WHY to trust it
- A loan AI rejects an application → Regulations may require explanation
- A self-driving car makes a bad decision → We need to understand the cause

**Explainability = making the model's decisions transparent and understandable**

---

### 5.9.1 SHAP (SHapley Additive exPlanations)

**Based on:** Game theory (Shapley values from cooperative game theory)

**Core Idea:** For each prediction, calculate how much each feature **contributed** to that prediction.

**Analogy:**
> Imagine a team of workers completed a project. SHAP calculates how much credit each worker deserves for the final result, based on how the output changes when each worker is included or excluded.

**How it works:**
- For a prediction, SHAP computes the **marginal contribution** of each feature across all possible combinations
- Positive SHAP value → feature pushed prediction higher
- Negative SHAP value → feature pushed prediction lower

**Example:** Loan approval prediction
```
Base (average) prediction: 0.5 (50% chance of approval)
Feature Contributions:
  + Income: High (+0.2) → increases approval chance
  + Credit Score: 750 (+0.15) → increases chance
  - Debt: High (-0.1) → decreases chance
  - Age: 22 (-0.05) → slight decrease
Final Prediction: 0.5 + 0.2 + 0.15 - 0.1 - 0.05 = 0.7 (70% approved)
```

**SHAP Plot Types:**
- **Bar Plot:** Overall feature importance
- **Beeswarm Plot:** Distribution of SHAP values for each feature
- **Waterfall Plot:** Explanation for a single prediction
- **Force Plot:** Interactive visualization of individual prediction

```python
import shap
explainer = shap.DeepExplainer(model, background_data)
shap_values = explainer.shap_values(test_data)
shap.summary_plot(shap_values, test_data)
```

---

### 5.9.2 LIME (Local Interpretable Model-Agnostic Explanations)

**Core Idea:** Explain a single prediction by training a **simple, interpretable model** (like linear regression) around that specific data point.

**"Local":** Explains one prediction at a time (not the whole model globally)
**"Interpretable":** Uses a simple model (linear) that humans can understand
**"Model-Agnostic":** Works with ANY model (CNN, RNN, XGBoost, etc.)

**How LIME works:**
1. Take the input you want to explain (e.g., one image)
2. Create many **perturbed versions** (slightly modified copies)
3. Run all through the complex model to get predictions
4. Train a **simple linear model** on these perturbed samples
5. The linear model's weights explain the prediction locally

**Example: Image Classification**
- Original image: "Cat" (95% confidence)
- LIME shows which **superpixels** (regions) contributed to the "Cat" prediction
- Result: Ears, eyes, and fur pattern regions highlighted → model uses these features to identify cats

**Example: Text Classification (Spam Detection)**
```
Email: "CONGRATULATIONS! You WON a FREE iPhone!"
LIME highlights: "CONGRATULATIONS" (high spam signal), "FREE" (high spam signal), "WON" (medium spam signal)
```

```python
import lime
from lime import lime_image

explainer = lime_image.LimeImageExplainer()
explanation = explainer.explain_instance(image, model.predict, num_samples=1000)
image_segments, mask = explanation.get_image_and_mask(label=1)
```

### SHAP vs LIME:

| Feature | SHAP | LIME |
|---|---|---|
| Basis | Game Theory (Shapley values) | Local linear approximation |
| Scope | Global + Local | Primarily Local |
| Consistency | Guaranteed consistent | May vary |
| Speed | Can be slow for large models | Faster for images/text |
| Best for | Tabular data | Images, text |

---

## Unit V Summary

| Topic | Key Takeaway |
|---|---|
| Autoencoder | Compress & reconstruct; learns latent representations; good for anomaly detection |
| VAE | Adds probability distribution to latent space; enables meaningful generation |
| GAN | Generator vs Discriminator competition; creates realistic fake data |
| GAN Challenges | Mode collapse, non-convergence, training instability |
| Boltzmann Machine | Energy-based probabilistic model; visible + hidden units |
| RBM | Restricted BM: no within-layer connections; used in recommendations |
| Deep Belief Network | Stacked RBMs; greedy pre-training; historically important |
| Self-Attention | Each word attends to all others; captures context |
| Transformer | Parallel processing, multi-head attention, positional encoding |
| BERT | Bidirectional encoder; MLM + NSP pre-training; fine-tune for NLP tasks |
| SHAP | Game theory-based; feature contribution values; globally consistent |
| LIME | Local linear approximation; model-agnostic; works for images/text |

---
*End of Unit V*
