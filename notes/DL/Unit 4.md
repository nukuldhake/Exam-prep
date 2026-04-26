# AD32231: Deep Learning
## Unit IV: Recurrent Networks
### Course Outcome 4 (CO4): Develop deep recurrent models for time-series and NLP, analyze long-term dependency challenges, and optimize recurrent models.

---

## 4.1 Why Recurrent Neural Networks?

### The Problem with Standard ANN/CNN for Sequential Data
Regular neural networks (ANN, CNN) treat each input **independently** — they have no concept of order or sequence.

But many real-world problems involve **sequential data** where context matters:
- **Text:** "The bank is on the river bank" — the word "bank" has different meanings based on context
- **Speech:** Audio sounds must be understood in sequence
- **Time Series:** Today's stock price depends on yesterday's price
- **Video:** Frame 10 depends on frames 1-9

**Analogy:**
> Reading a story, you remember what happened in earlier chapters when you reach a later chapter. A regular ANN is like someone who forgets each sentence immediately after reading it.

### Solution: Recurrent Neural Networks (RNNs)
RNNs have **memory** — they pass information from one time step to the next via a **hidden state**.

---

## 4.2 Recurrent Neural Networks (RNN)

### Architecture:
```
x(t-1) → [RNN Cell] → h(t-1)
x(t)   → [RNN Cell] → h(t)   → output(t)
x(t+1) → [RNN Cell] → h(t+1)
```

At each time step `t`:
- **Input:** x(t) (current input, e.g., current word)
- **Hidden state:** h(t) (memory from the past)
- **Output:** y(t) (prediction at this step)

**Formulas:**
```
h(t) = tanh(W_h × h(t-1) + W_x × x(t) + b_h)
y(t) = W_y × h(t) + b_y
```

The **same weights** (W_h, W_x) are used at every time step → parameter sharing!

### RNN Unfolded (visualized over time):
```
x1 → [Cell] → h1 → [Cell] → h2 → [Cell] → h3 → output
        ↑             ↑              ↑
       h0=0
```

### Types of RNN by Input-Output:
```
One-to-One:   x → y         (not really RNN; like image classification)
One-to-Many:  x → y1,y2,y3  (image captioning: image → text)
Many-to-One:  x1,x2,x3 → y  (sentiment analysis: text → positive/negative)
Many-to-Many: x1,x2 → y1,y2 (machine translation, NER)
```

### Problem: Short Memory
Standard RNNs struggle to remember information from **far back** in the sequence.

Example: "I grew up in France... [200 words later] ...I speak fluent French."
- The word "French" depends on "France" from 200 words ago
- Standard RNN: by the time it reaches "French," it has mostly forgotten "France"

---

## 4.3 Bidirectional RNNs

### What is it?
A **Bidirectional RNN** processes the sequence in **both directions** simultaneously:
- **Forward RNN:** Reads from left to right (past context)
- **Backward RNN:** Reads from right to left (future context)
- Both hidden states are combined for each time step

```
Forward:   x1 → x2 → x3 → x4
Backward:  x4 → x3 → x2 → x1
                 ↓
          Combined output at each step
```

### Why Bidirectional?
Some tasks need **both past AND future context**:

**Example (Named Entity Recognition):**
"I visited **Apple** store yesterday."
- Knowing "store" comes AFTER "Apple" helps confirm "Apple" is an organization (not the fruit)
- Forward-only RNN doesn't know "store" is coming

### Applications:
- **Speech Recognition:** Audio context before AND after helps decode current sound
- **Machine Translation:** Understanding full sentence before translating
- **Text Classification:** Understanding full document
- Named Entity Recognition, POS Tagging

**Note:** Cannot be used when future input is unavailable (e.g., real-time prediction, streaming)

---

## 4.4 Encoder-Decoder (Sequence-to-Sequence) Architecture

### What is it?
The **Seq2Seq** model consists of:
1. **Encoder:** Reads the entire input sequence and compresses it into a **context vector** (fixed-size summary)
2. **Decoder:** Takes the context vector and generates the output sequence step by step

```
Input:  "How are you?"
         ↓ ↓ ↓
      [Encoder RNN] → Context Vector (c)
                            ↓
                      [Decoder RNN] → "Comment" → "allez" → "vous?"
```

### Applications:
- **Machine Translation:** English → French
- **Text Summarization:** Long article → short summary
- **Chatbots:** User message → bot response
- **Speech-to-Text:** Audio → text

### Problem: Context Vector Bottleneck
When input is long (hundreds of words), compressing everything into ONE fixed-size vector loses information!

**Solution:** Attention Mechanism (we'll see in Unit V with Transformers)

---

## 4.5 Deep Recurrent Networks

### What are they?
Stack **multiple RNN layers** on top of each other. The output (hidden state) of one RNN layer becomes the input to the next layer.

```
Layer 3: [RNN] → [RNN] → [RNN] → output
           ↑        ↑       ↑
Layer 2: [RNN] → [RNN] → [RNN]
           ↑        ↑       ↑
Layer 1: [RNN] → [RNN] → [RNN]
           ↑        ↑       ↑
         x(1)    x(2)    x(3)
```

**Why deep?** Each layer learns increasingly abstract representations:
- Layer 1: Individual characters/words
- Layer 2: Phrases, local patterns
- Layer 3: Sentence-level semantics

**Used in:** Advanced NLP models, speech recognition (Deep Speech)

---

## 4.6 Recursive Neural Networks

**NOT to be confused with Recurrent Networks!**

A **Recursive Neural Network** applies the same function **recursively over a tree structure** (not a sequence).

```
      [Root]
      /    \
  [Node]  [Node]
  /   \      \
[L1] [L2]  [L3]
```

Used for:
- **Parsing sentence structure** (syntax trees)
- **Scene understanding** (hierarchical object relationships)
- **Sentiment analysis** on phrase-level (positive/negative for each phrase)

**Example:** "Not bad at all" → Tree structure captures that "Not" negates "bad"

---

## 4.7 Echo State Networks (ESN)

**Echo State Networks** are a type of RNN where:
- The internal connections (hidden-to-hidden weights) are **fixed/random** and NOT trained
- Only the **output weights** are trained (much simpler and faster!)

The recurrent part acts as a "reservoir" that creates complex dynamics from simple inputs.

**Key features:**
- Very fast to train (linear regression on output weights)
- Good for time-series prediction
- Used in: speech recognition, robotics control, financial forecasting

**Analogy:**
> Like throwing a stone into a pond (input) and predicting the ripple patterns (output). You study the ripples (reservoir states) to make predictions.

---

## 4.8 Leaky Units and Strategies for Multiple Time Scales

### The Problem:
Real-world data often has **multiple time scales** — some patterns change quickly, others slowly:
- Stock market: short-term fluctuations (seconds) vs long-term trends (years)
- Language: word-level (milliseconds) vs topic-level (minutes)

### Leaky Units:
- A hidden unit that **slowly accumulates** information over time
- Uses a moving average of past states

```
h(t) = α × h(t-1) + (1-α) × new_value
```
- When α is close to 1: **slow update** (long-term memory)
- When α is close to 0: **fast update** (short-term memory)

### Other Strategies:
1. **Skipped Connections:** Add connections that skip multiple time steps (d=2, d=3, etc.)
2. **Multiple Time Scales:** Have different groups of units that update at different rates
3. **Hierarchical RNNs:** Multiple levels, each operating at a different time scale

---

## 4.9 Long Short-Term Memory (LSTM) ⭐ Most Important

### The Problem with Vanilla RNN:
**Vanishing Gradient Problem:** During backpropagation through time (BPTT), gradients shrink exponentially → RNN forgets events far back in the sequence.

### The Solution: LSTM
LSTMs were introduced by **Hochreiter & Schmidhuber (1997)** to solve the long-term dependency problem.

**Key Idea:** LSTMs have a special **cell state (C)** — a conveyor belt that runs through the sequence, allowing information to flow unchanged.

### LSTM has 3 Gates:
Gates are mechanisms that control **what information to keep or discard**.

#### 1. Forget Gate (f)
- Decides what information from the **old cell state** to throw away
- Output: values between 0 (forget completely) and 1 (keep completely)
```
f(t) = sigmoid(W_f × [h(t-1), x(t)] + b_f)
New Cell State = old_cell_state × f(t)
```
**Example:** In translating a sentence, when you start a new sentence, forget the gender of the previous subject noun.

#### 2. Input Gate (i) + Candidate Values (C̃)
- Decides what **new information** to store in the cell state
```
i(t) = sigmoid(W_i × [h(t-1), x(t)] + b_i)
C̃(t) = tanh(W_C × [h(t-1), x(t)] + b_C)
New info = i(t) × C̃(t)
```
**Example:** When a new subject is introduced, store their gender as it may be needed for pronoun agreement later.

#### 3. Output Gate (o)
- Decides what to output based on the cell state
```
o(t) = sigmoid(W_o × [h(t-1), x(t)] + b_o)
h(t) = o(t) × tanh(C(t))
```

### LSTM Cell Diagram:
```
              Cell State C(t-1) ─────────── × ─────────── + ───────── C(t)
                                            ↑             ↑
                                         f (forget)    i × C̃ (input)
                                            ↑             ↑
h(t-1) ─┬─ [Forget Gate f] ────────────────┘             │
x(t) ───┤─ [Input Gate i] ──────────────────────────────→ + ─→ C̃
         ├─ [Candidate C̃] ─────────────────────────────→/
         └─ [Output Gate o] ────────── × tanh(C(t)) → h(t)
```

### Why LSTM Works:
- Cell state provides a **direct path** for gradients to flow (no vanishing!)
- Gates learn what information is relevant to keep

### GRU (Gated Recurrent Unit) — Simpler Alternative
- Introduced by Cho et al. (2014)
- Combines forget and input gates into a single **update gate**
- Fewer parameters than LSTM → faster training
- Often performs similarly to LSTM

**GRU Gates:**
- **Reset Gate:** How much past info to forget
- **Update Gate:** How much past info to keep vs new info

**When to use what:**
- LSTM: More complex tasks, longer sequences
- GRU: Faster training needed, shorter sequences, less data

---

## 4.10 Optimization for Long-Term Dependencies

### Challenges:
1. **Vanishing gradient:** Gradients shrink → early parts of sequence not learned
2. **Exploding gradient:** Gradients grow → unstable training
3. **Long sequences:** Computationally expensive

### Solutions:

#### 1. Gradient Clipping
- Cap the gradient at a maximum value before weight update
- Prevents exploding gradient
```python
optimizer = tf.keras.optimizers.Adam(clipvalue=1.0)  # Clips gradient to [-1, 1]
```

#### 2. LSTM / GRU
- Designed specifically to solve vanishing gradient through gating mechanisms

#### 3. Truncated BPTT (Backpropagation Through Time)
- Instead of backpropagating through the entire sequence, backpropagate only through the last K steps
- Trade-off: May miss very long-term dependencies

#### 4. Attention Mechanism
- Instead of relying solely on hidden state, allow the model to "look back" at all previous states
- Precursor to Transformer architecture (Unit V)

#### 5. Skip Connections
- Like ResNet, add skip connections across time steps to allow gradient to flow more easily

---

## Unit IV Summary

| Topic | Key Takeaway |
|---|---|
| RNN | Sequential processing with memory (hidden state); same weights at each step |
| Bidirectional RNN | Processes sequence in both directions; needs full sequence upfront |
| Seq2Seq | Encoder compresses input; Decoder generates output; used in translation |
| Deep RNN | Multiple stacked RNN layers; learns hierarchical features |
| Recursive NN | Tree structure processing; for syntax trees and hierarchical data |
| Echo State | Fixed random reservoir; only output weights trained; fast |
| Leaky Units | Slowly accumulate info; model multiple time scales |
| LSTM | 3 gates (forget, input, output) + cell state; solves long-term dependency |
| GRU | Simplified LSTM; 2 gates; faster, often equally good |
| Gradient Clipping | Prevent exploding gradients by capping maximum gradient value |
| Truncated BPTT | Backpropagate through limited timesteps for efficiency |

---
*End of Unit IV*
