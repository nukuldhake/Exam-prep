
---

# ✅ NUMERICAL 1  
# ✅ Binary Cross Entropy (From Your Notes)

---

## ✅ Question:

Given the following actual and predicted outputs:

| Sample | Y (Actual) | Ŷ (Predicted) |
| ------ | ---------- | ------------- |
| S1     | 1          | 0.8           |
| S2     | 0          | 0.2           |
| S3     | 0          | 0.6           |
| S4     | 1          | 0.9           |

Compute the Binary Cross Entropy loss.

---

## ✅ Given:

\[
n = 4
\]

Formula:

\[
BCE = -\frac{1}{n} \sum_{i=1}^{n} [y_i \log(\hat{y}_i) + (1-y_i)\log(1-\hat{y}_i)]
\]

---

## ✅ Step 1: Apply Formula for Each Sample

---

### 🔹 S1:

\[
y=1, \hat{y}=0.8
\]

\[
= 1\log(0.8) + 0
\]

\[
= \log(0.8)
\]

\[
\log(0.8) ≈ -0.223
\]

---

### 🔹 S2:

\[
y=0, \hat{y}=0.2
\]

\[
= 0 + \log(1-0.2)
\]

\[
= \log(0.8)
\]

\[
= -0.223
\]

---

### 🔹 S3:

\[
y=0, \hat{y}=0.6
\]

\[
= \log(1-0.6)
\]

\[
= \log(0.4)
\]

\[
= -0.916
\]

---

### 🔹 S4:

\[
y=1, \hat{y}=0.9
\]

\[
= \log(0.9)
\]

\[
= -0.105
\]

---

## ✅ Step 2: Sum All Values

\[
-0.223 -0.223 -0.916 -0.105
\]

\[
= -1.467
\]

---

## ✅ Step 3: Divide by n and Apply Negative

\[
BCE = -\frac{-1.467}{4}
\]

\[
= 0.367
\]

---

## ✅ Final Answer:

\[
\boxed{BCE = 0.367}
\]

---

## ✅ Why We Did This?

Cross entropy measures how far predicted probabilities are from actual labels.

Smaller value = better prediction.

---

# ✅ NUMERICAL 2  
# ✅ Convolution Output Size

---

## ✅ Question:

Input size = 32×32  
Filter size = 5×5  
Stride = 1  
Padding = 0  

Find output feature map size.

---

## ✅ Formula:

\[
Output = \frac{(n - f + 2p)}{s} + 1
\]

Where:

- n = input size  
- f = filter size  
- p = padding  
- s = stride  

---

## ✅ Step 1: Substitute Values

\[
= \frac{(32 - 5 + 0)}{1} + 1
\]

\[
= 27 + 1
\]

\[
= 28
\]

---

## ✅ Final Answer:

\[
\boxed{28 \times 28}
\]

---

## ✅ Explanation:

Each time filter slides, it reduces dimension by (f-1) when padding=0.

---

# ✅ NUMERICAL 3  
# ✅ Parameter Calculation in CNN

---

## ✅ Question:

Filter size = 3×3  
Input channels = 3  
Number of filters = 64  

Find total parameters.

---

## ✅ Formula:

\[
Parameters = (f_h \times f_w \times n_c + 1) \times n_f
\]

---

## ✅ Step 1:

\[
(3 × 3 × 3 + 1) × 64
\]

\[
(27 + 1) × 64
\]

\[
28 × 64
\]

\[
= 1792
\]

---

## ✅ Final Answer:

\[
\boxed{1792 \text{ parameters}}
\]

---

## ✅ Explanation:

Each filter has:

27 weights + 1 bias = 28 parameters  
Total filters = 64  

---

# ✅ NUMERICAL 4  
# ✅ Perceptron Weight Update

---

## ✅ Question:

\[
x = [1,2]
\]

\[
w = [0.4,-0.6]
\]

\[
b=0.2,\quad η=0.1
\]

Target = 1  

Step function activation.

Find updated weights after one iteration.

---

## ✅ Step 1: Net Input

\[
z = 0.4(1) + (-0.6)(2) + 0.2
\]

\[
= 0.4 - 1.2 + 0.2
\]

\[
= -0.6
\]

---

## ✅ Step 2: Predicted Output

\[
z<0
\]

\[
\hat{y} = 0
\]

---

## ✅ Step 3: Error

\[
Error = 1 - 0 = 1
\]

---

## ✅ Step 4: Update Rule

\[
w_i^{new} = w_i + η (y - \hat{y}) x_i
\]

---

### Update w1:

\[
0.4 + 0.1(1)(1) = 0.5
\]

---

### Update w2:

\[
-0.6 + 0.1(1)(2)
\]

\[
= -0.6 + 0.2 = -0.4
\]

---

### Update bias:

\[
0.2 + 0.1(1) = 0.3
\]

---

## ✅ Final Answer:

\[
w = [0.5, -0.4], \quad b = 0.3
\]

---

# ✅ NUMERICAL 5  
# ✅ IoU Calculation

---

## ✅ Question:

TP = 70  
FP = 20  
FN = 10  

Find IoU.

---

## ✅ Formula:

\[
IoU = \frac{TP}{TP + FP + FN}
\]

---

## ✅ Step 1:

\[
= \frac{70}{70 + 20 + 10}
\]

\[
= \frac{70}{100}
\]

\[
= 0.7
\]

---

## ✅ Final Answer:

\[
\boxed{IoU = 0.7}
\]

---

# ✅ NUMERICAL 6  
# ✅ RNN Hidden State

---

## ✅ Question:

\[
h_t = \tanh(Wx_t + Uh_{t-1})
\]

Given:
\[
W=1,\quad U=0.5
\]
\[
x_1=2,\quad h_0=0
\]

Find h1.

---

## ✅ Step 1:

\[
h_1 = \tanh(1(2) + 0.5(0))
\]

\[
= \tanh(2)
\]

\[
\tanh(2) ≈ 0.964
\]

---

## ✅ Final Answer:

\[
\boxed{h_1 ≈ 0.964}
\]

---

