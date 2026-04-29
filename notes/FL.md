# AD32234C: Federated Learning — Comprehensive Course Notes

---

## UNIT I: Introduction to Federated Learning (6 Hrs)

---

### 1.1 Overview and Definition

**Federated Learning (FL)** is a machine learning paradigm where a model is trained across multiple decentralized devices or servers holding local data samples, **without exchanging the raw data**. Instead of centralizing data, the learning algorithm travels to the data.

**Formal Definition:**
Federated Learning is a distributed machine learning approach that enables training a shared global model across multiple participants (clients/devices/organizations) while keeping all training data localized on each participant's device. Only model updates (gradients or parameters) are communicated to a central server (or peers), preserving data privacy and reducing communication overhead.

**Key Principle:** "Bring the code to the data, not the data to the code."

#### Mathematical Formulation

The global objective in Federated Learning is:

$$\min_{w} F(w) = \sum_{k=1}^{K} \frac{n_k}{n} F_k(w)$$

Where:
- $K$ = number of clients
- $n_k$ = number of data samples on client $k$
- $n = \sum_{k=1}^{K} n_k$ = total number of samples
- $F_k(w) = \frac{1}{n_k} \sum_{i \in \mathcal{D}_k} \ell(w; x_i, y_i)$ = local objective function of client $k$
- $\ell$ = loss function
- $w$ = model parameters

---

### 1.2 History of Federated Learning

| Year | Milestone |
|------|-----------|
| **2015** | Google conceptualizes Federated Learning |
| **2016** | McMahan et al. publish the seminal paper "Communication-Efficient Learning of Deep Networks from Decentralized Data" introducing **FedAvg** |
| **2017** | Google deploys FL in Gboard (Android keyboard) for next-word prediction |
| **2018** | Apple adopts FL for Siri improvements; research on privacy (differential privacy + FL) intensifies |
| **2019** | Federated Learning frameworks emerge (TensorFlow Federated, PySyft); cross-silo FL gains traction in healthcare and finance |
| **2020–2021** | FL applied to COVID-19 research; emergence of vertical FL, split learning; standardization efforts (IEEE, OpenFL) |
| **2022–Present** | Integration with Large Language Models, Digital Twins, Edge AI; frameworks like FLOWER, FLUTE, FLSim mature |

---

### 1.3 Applications of Federated Learning

1. **Mobile Keyboard Prediction** (Google Gboard): Next-word prediction without collecting user typing data
2. **Healthcare**: Training diagnostic models across hospitals without sharing patient records (HIPAA compliance)
3. **Finance**: Collaborative fraud detection across banks without exposing transaction data
4. **Autonomous Vehicles**: Sharing driving model improvements across vehicles without centralizing sensor data
5. **IoT/Edge Computing**: Smart home devices learning collectively
6. **Telecommunications**: Network optimization across carriers
7. **Retail**: Recommendation systems across stores without sharing purchase history
8. **Natural Language Processing**: Voice assistants (Google Assistant, Alexa)

---

### 1.4 Terms and Concepts in Federated Learning

| Term | Definition |
|------|-----------|
| **Client/Participant** | A device or organization that holds local data and participates in training |
| **Global Model** | The shared model maintained by the server, aggregated from client updates |
| **Local Model** | The model trained on a client's local data |
| **Communication Round** | One cycle of: server sends model → clients train locally → clients send updates → server aggregates |
| **Aggregation** | The process of combining model updates from multiple clients (e.g., FedAvg) |
| **Non-IID Data** | Non-Independent and Identically Distributed data — data across clients is heterogeneous |
| **IID Data** | Data that is uniformly and independently distributed across clients |
| **Model Update** | The change in model parameters (gradients or weights) sent from client to server |
| **Stragglers** | Slow clients that delay the training process |
| **Data Silo** | Isolated data repositories within organizations |
| **Privacy Budget (ε)** | Parameter in differential privacy controlling the privacy-accuracy tradeoff |

---

### 1.5 Federated Learning Architecture

#### Standard Architecture Components:

```
┌─────────────────────────────────────┐
│           CENTRAL SERVER            │
│  ┌─────────────────────────────┐    │
│  │   Global Model Aggregator   │    │
│  │   (FedAvg / FedSGD / etc.)  │    │
│  └─────────────────────────────┘    │
└──────────┬──────────┬───────────────┘
           │          │          │
     ┌─────▼──┐ ┌─────▼──┐ ┌────▼───┐
     │Client 1│ │Client 2│ │Client K│
     │Local   │ │Local   │ │Local   │
     │Data D₁ │ │Data D₂ │ │Data Dₖ │
     │Local   │ │Local   │ │Local   │
     │Model   │ │Model   │ │Model   │
     └────────┘ └────────┘ └────────┘
```

#### Detailed Workflow:

1. **Initialization**: Server initializes global model $w_0$
2. **Distribution**: Server sends current global model to selected clients
3. **Local Training**: Each client trains the model on its local data for several epochs
4. **Upload**: Clients send model updates (not data) back to the server
5. **Aggregation**: Server aggregates updates to form a new global model
6. **Iteration**: Steps 2–5 repeat until convergence

---

### 1.6 Different Types of Federated Learning

#### 1.6.1 Based on Data Partitioning

**a) Horizontal Federated Learning (HFL) — Sample-based FL**

- Clients share the **same feature space** but have **different samples**
- Example: Two regional banks with the same types of data columns but different customers

```
Client A:  [Feature1, Feature2, Feature3] → Samples 1-1000
Client B:  [Feature1, Feature2, Feature3] → Samples 1001-2000
```

$$\mathcal{X}_A = \mathcal{X}_B, \quad \mathcal{Y}_A = \mathcal{Y}_B, \quad \mathcal{I}_A \neq \mathcal{I}_B$$

Where $\mathcal{X}$ = feature space, $\mathcal{Y}$ = label space, $\mathcal{I}$ = sample ID space.

**b) Vertical Federated Learning (VFL) — Feature-based FL**

- Clients share the **same samples** but have **different features**
- Example: A bank and an e-commerce company in the same city have overlapping users but different data attributes

```
Client A:  [Feature1, Feature2]     → User set {u1, u2, ..., u500}
Client B:  [Feature3, Feature4]     → User set {u1, u2, ..., u500}
```

$$\mathcal{X}_A \neq \mathcal{X}_B, \quad \mathcal{Y}_A \neq \mathcal{Y}_B, \quad \mathcal{I}_A = \mathcal{I}_B$$

**c) Federated Transfer Learning (FTL)**

- Clients have **different feature spaces** AND **different sample spaces** with minimal overlap
- Uses transfer learning techniques to bridge the gap

$$\mathcal{X}_A \neq \mathcal{X}_B, \quad \mathcal{I}_A \neq \mathcal{I}_B$$

#### Comparison Table:

| Aspect | Horizontal FL | Vertical FL | Federated Transfer Learning |
|--------|:------------:|:-----------:|:---------------------------:|
| Feature Space | Same | Different | Different |
| Sample Space | Different | Same (overlapping) | Different |
| Typical Use Case | Multiple hospitals | Bank + E-commerce | Cross-domain |
| Aggregation | FedAvg | Secure aggregation + entity alignment | Domain adaptation |
| Communication | Model parameters | Intermediate representations | Transformed features |

#### 1.6.2 Based on Scale

**a) Cross-Device FL**
- Massive number of clients (millions): mobile phones, IoT devices
- Each client has very limited data
- Clients are unreliable (may drop off)
- Example: Google Gboard

**b) Cross-Silo FL**
- Small number of clients (2–100): organizations, hospitals, banks
- Each client has substantial data
- Clients are reliable and always available
- Example: Multi-hospital medical research

| Property | Cross-Device | Cross-Silo |
|----------|:----------:|:---------:|
| Number of Clients | 10⁶ – 10¹⁰ | 2 – 100 |
| Data per Client | Small | Large |
| Client Availability | Intermittent | Always |
| Client Identity | Anonymous | Known |
| Communication | Slow, unreliable | Fast, reliable |
| Example | Smartphones | Hospitals |

---

### 1.7 Cross-Device Federated Learning Setting

**Characteristics:**
- **Client Selection**: In each round, only a small fraction of available clients are selected
- **Stateless Clients**: Clients cannot maintain state across rounds (may never be selected again)
- **Asynchronous Communication**: Clients have varying computation and communication speeds
- **Data Heterogeneity**: Data across devices is highly non-IID
- **System Heterogeneity**: Devices have different computational capabilities

**Typical Protocol:**
1. Server selects a subset $S_t$ of clients (e.g., a few hundred out of millions)
2. Selected clients download current model
3. Each client performs local SGD for $E$ local epochs with batch size $B$
4. Clients upload compressed model updates
5. Server aggregates and updates global model

---

### 1.8 A Typical Federated Training Process

```
Algorithm: Federated Averaging (FedAvg) — High-Level
─────────────────────────────────────────────────────
Server:
  Initialize w₀
  For each round t = 1, 2, ..., T:
    Select subset Sₜ of K clients
    Send wₜ to all clients in Sₜ
    For each client k ∈ Sₜ (in parallel):
      wₜ₊₁ᵏ ← ClientUpdate(k, wₜ)
    Aggregate: wₜ₊₁ ← Σₖ (nₖ/n) · wₜ₊₁ᵏ

ClientUpdate(k, w):
  B ← split local data into batches
  For each local epoch e = 1, ..., E:
    For each batch b ∈ B:
      w ← w − η · ∇ℓ(w; b)
  Return w
```

**Detailed Steps:**

| Step | Action | Location |
|------|--------|----------|
| 1 | Initialize global model parameters | Server |
| 2 | Broadcast global model to selected clients | Server → Clients |
| 3 | Perform local training (multiple epochs/batches) | Clients |
| 4 | Compute model update (Δw = w_local − w_global) | Clients |
| 5 | Upload model updates to server | Clients → Server |
| 6 | Aggregate updates (weighted average) | Server |
| 7 | Update global model | Server |
| 8 | Repeat steps 2–7 until convergence | — |

---

### 1.9 Criteria for a Reliable Federated Learning System

1. **Privacy**: Raw data never leaves the client; model updates should be protected (differential privacy, secure aggregation)
2. **Communication Efficiency**: Minimize communication rounds and payload size
3. **Robustness**: Handle client failures, stragglers, and adversarial participants
4. **Scalability**: Support from tens to millions of clients
5. **Accuracy**: Achieve model quality comparable to centralized training
6. **Fairness**: Model should perform well for all participants, not just those with more data
7. **Heterogeneity Handling**: Support non-IID data distributions and diverse hardware
8. **Auditability**: Track contributions and detect malicious behavior
9. **Fault Tolerance**: Continue training despite client dropouts
10. **Incentive Mechanism**: Motivate clients to participate honestly

---

### 1.10 Federated Learning vs Centralized Learning

| Aspect | Centralized Learning | Federated Learning |
|--------|:-------------------:|:------------------:|
| **Data Location** | Centralized data warehouse | Distributed across clients |
| **Data Movement** | Data moves to computation | Computation moves to data |
| **Privacy** | High risk of data breach | Data stays local — better privacy |
| **Communication Cost** | One-time data transfer | Multiple rounds of model exchange |
| **Data Heterogeneity** | Typically IID (shuffled) | Often non-IID |
| **Computation** | Centralized (GPU cluster) | Distributed (heterogeneous devices) |
| **Scalability** | Limited by storage | Limited by communication |
| **Regulatory Compliance** | Difficult (GDPR, HIPAA) | Easier compliance |
| **Model Performance** | Generally higher | May be lower due to non-IID |
| **Fault Tolerance** | Single point of failure | More resilient |
| **Training Speed** | Faster (local computation) | Slower (communication bottleneck) |
| **Data Ownership** | Central entity owns all | Each participant owns their data |

---

### 1.11 Security & Privacy in FL (Introduction)

#### Privacy Threats:
- **Model Inversion Attacks**: Reconstructing training data from model parameters
- **Gradient Leakage**: Inferring private data from shared gradients
- **Membership Inference**: Determining if a sample was used in training

#### Privacy Preservation Techniques:
1. **Differential Privacy (DP)**: Adding calibrated noise to gradients
2. **Secure Multi-Party Computation (SMPC)**: Cryptographic protocols for secure aggregation
3. **Homomorphic Encryption (HE)**: Computing on encrypted model updates
4. **Secure Aggregation**: Ensuring the server only sees aggregated updates, not individual ones

#### Security Threats:
- **Byzantine Attacks**: Malicious clients sending corrupted updates
- **Data Poisoning**: Clients with manipulated local data
- **Model Poisoning**: Directly manipulating model updates
- **Free-Riding**: Clients that benefit without contributing

---

### 1.12 Case Study: FL for Google Assistant 'Hey Google' / Alexa

#### Background:
Google uses Federated Learning to improve its voice assistant services, particularly:
- **Hotword Detection**: Improving "Hey Google" activation accuracy
- **Speech Recognition**: Enhancing automatic speech recognition (ASR) models
- **Query Suggestions**: Personalizing responses

#### Implementation Details:

1. **Problem**: Millions of users interact with Google Assistant daily. Their voice data is highly personal and sensitive.

2. **FL Approach**:
   - Each device trains a local model on the user's voice interactions
   - Only model updates (not audio recordings) are sent to Google servers
   - Server aggregates updates using Secure Aggregation
   - Updated global model is pushed back to devices

3. **Technical Specifics**:
   - Used **FedAvg** with thousands of Android devices per round
   - Applied **differential privacy** (ε-DP) for formal privacy guarantees
   - Model updates are **compressed** to reduce communication (quantization, sketching)
   - Training happens only when devices are:
     - Charging
     - Connected to Wi-Fi
     - Idle (unmetered network)

4. **Results**:
   - Improved "Hey Google" detection accuracy by ~20% relative
   - Reduced false activation rates
   - No raw audio data ever left user devices

5. **Privacy Guarantees**:
   - Secure Aggregation ensures server sees only the aggregate
   - Differential Privacy adds noise to individual updates
   - Minimum participation threshold before accepting a round

#### Architecture Diagram:

```
┌──────────────────────────┐
│     Google FL Server     │
│  ┌────────────────────┐  │
│  │  Secure Aggregator │  │
│  │  + DP Noise Adder  │  │
│  └─────────┬──────────┘  │
└────────────┼─────────────┘
    ┌────────┼────────┐
    │        │        │
┌───▼──┐ ┌──▼───┐ ┌──▼───┐
│Phone1│ │Phone2│ │PhoneN│
│"Hey  │ │"Hey  │ │"Hey  │
│Google"│ │Google"│ │Google"│
│data  │ │data  │ │data  │
└──────┘ └──────┘ └──────┘
```

---

## UNIT II: Federated Learning Systems — Architecture Alternatives (6 Hrs)

---

### 2.1 System Architecture of Federated Learning

A Federated Learning system comprises several key components:

#### Core Components:

1. **Communication Layer**
   - Handles message passing between server and clients
   - Protocols: gRPC, HTTP/2, WebSocket, MQTT (for IoT)
   - Must handle unreliable connections, NAT traversal, and asynchronous communication

2. **Computation Layer**
   - Local training engine (PyTorch, TensorFlow)
   - Model serialization and deserialization
   - Resource management on heterogeneous devices

3. **Aggregation Layer**
   - Implements aggregation algorithms (FedAvg, FedProx, etc.)
   - May include secure aggregation protocols
   - Handles weighted vs. unweighted averaging

4. **Privacy Layer**
   - Differential privacy mechanisms
   - Secure computation protocols
   - Encryption/decryption of model updates

5. **Orchestration Layer**
   - Client selection and scheduling
   - Round management
   - Model versioning and deployment

6. **Storage Layer**
   - Model checkpointing
   - Logging and monitoring
   - Metadata management

#### System Architecture Diagram:

```
┌─────────────────────────────────────────────────────┐
│                    FL SERVER                         │
│  ┌──────────┐ ┌──────────┐ ┌──────────────────────┐│
│  │Orchestr- │ │Aggregat- │ │  Privacy Engine      ││
│  │ation     │ │ion Engine│ │  (DP, Secure Agg)    ││
│  │Engine    │ │(FedAvg)  │ │                      ││
│  └──────────┘ └──────────┘ └──────────────────────┘│
│  ┌──────────────────────────────────────────────┐  │
│  │        Communication Manager (gRPC)          │  │
│  └──────────────────────────────────────────────┘  │
└───────────────────────┬─────────────────────────────┘
                        │ (Model Updates / Global Model)
        ┌───────────────┼───────────────┐
        │               │               │
┌───────▼──────┐ ┌──────▼───────┐ ┌─────▼────────┐
│   CLIENT 1   │ │   CLIENT 2   │ │   CLIENT K   │
│┌────────────┐│ │┌────────────┐│ │┌────────────┐│
││Local Data  ││ ││Local Data  ││ ││Local Data  ││
│├────────────┤│ │├────────────┤│ │├────────────┤│
││Training    ││ ││Training    ││ ││Training    ││
││Engine      ││ ││Engine      ││ ││Engine      ││
│├────────────┤│ │├────────────┤│ │├────────────┤│
││Privacy     ││ ││Privacy     ││ ││Privacy     ││
││Module      ││ ││Module      ││ ││Module      ││
│└────────────┘│ │└────────────┘│ │└────────────┘│
└──────────────┘ └──────────────┘ └──────────────┘
```

---

### 2.2 Architecture Alternatives

#### 2.2.1 Centralized Architecture (Client-Server / Star Topology)

**Description:**
A single central server coordinates the entire training process. All clients communicate exclusively with this server.

```
         ┌──────────┐
         │  Server  │
         └────┬─────┘
       ┌──────┼──────┐
       │      │      │
    ┌──▼─┐ ┌─▼──┐ ┌─▼──┐
    │ C1 │ │ C2 │ │ C3 │
    └────┘ └────┘ └────┘
```

**Advantages:**
- Simple to implement and manage
- Easy to enforce consistency
- Straightforward aggregation
- Clear trust model

**Disadvantages:**
- Single point of failure
- Communication bottleneck at server
- Server must be trusted
- Scalability limited by server capacity

**Use Cases:** Cross-device FL (Google Gboard), most standard FL deployments

---

#### 2.2.2 Hierarchical Architecture (Multi-Level Aggregation)

**Description:**
Multiple levels of aggregation servers organized in a tree structure. Edge servers perform intermediate aggregation before sending to the cloud server.

```
              ┌────────────┐
              │Cloud Server│
              └──────┬─────┘
            ┌────────┼────────┐
      ┌─────▼────┐      ┌────▼─────┐
      │Edge Srv 1│      │Edge Srv 2│
      └────┬─────┘      └────┬─────┘
     ┌─────┼─────┐      ┌────┼─────┐
   ┌─▼─┐ ┌▼──┐ ┌▼─┐  ┌─▼─┐ ┌▼──┐ ┌▼─┐
   │C1 │ │C2 │ │C3│  │C4 │ │C5 │ │C6│
   └───┘ └───┘ └──┘  └───┘ └───┘ └──┘
```

**Aggregation Process:**
1. Clients send updates to nearest edge server
2. Edge servers perform local aggregation:
   $$w_{edge_j} = \frac{1}{|S_j|} \sum_{k \in S_j} w_k$$
3. Edge servers send aggregated updates to cloud server
4. Cloud server performs global aggregation:
   $$w_{global} = \sum_{j=1}^{M} \frac{n_j}{n} w_{edge_j}$$

**Advantages:**
- Reduced communication load on central server
- Lower latency for clients (closer edge servers)
- Better scalability
- Can leverage geographic locality for Non-IID data

**Disadvantages:**
- More complex orchestration
- Potential for stale updates
- Multiple trust levels needed
- Edge servers add infrastructure cost

**Use Cases:** IoT networks, mobile network operators, geographically distributed systems

---

#### 2.2.3 Decentralized Architecture (Peer-to-Peer / Fully Distributed)

**Description:**
No central server. Clients communicate directly with their neighbors in a peer-to-peer network. Each client maintains its own model and exchanges updates with peers.

```
    ┌───┐     ┌───┐
    │C1 │─────│C2 │
    └─┬─┘     └─┬─┘
      │    ╲    │
      │     ╲   │
    ┌─▼─┐   ┌──▼┐
    │C4 │───│C3 │
    └───┘   └───┘
```

**Gossip Protocol for Decentralized FL:**
```
For each client k at round t:
  1. Select random neighbor j
  2. Exchange models: wₖ, wⱼ
  3. Average: wₖ ← (wₖ + wⱼ) / 2
  4. Perform local SGD
```

**Mathematical Framework:**
Using a mixing matrix $W$ where $W_{ij} > 0$ if clients $i$ and $j$ are neighbors:

$$w_i^{t+1} = \sum_{j \in \mathcal{N}(i)} W_{ij} \cdot w_j^t - \eta \nabla F_i(w_i^t)$$

The mixing matrix must be doubly stochastic: $\sum_j W_{ij} = 1$ and $\sum_i W_{ij} = 1$.

**Advantages:**
- No single point of failure
- No need for trusted server
- Better privacy (no central aggregator)
- Naturally scalable

**Disadvantages:**
- Slower convergence (gossip protocols)
- Difficult to ensure model consistency
- Complex topology management
- Vulnerable to network partitioning

**Use Cases:** Blockchain-based FL, military/defense, highly privacy-sensitive applications

---

#### 2.2.4 Regional Architecture

**Description:**
Clients are grouped into regions based on geographic location, data similarity, or organizational boundaries. Each region has its own aggregation server, and regional models may or may not be synchronized globally.

```
┌──────────────────┐     ┌──────────────────┐
│    Region A      │     │    Region B      │
│  ┌──────────┐    │     │  ┌──────────┐    │
│  │Regional  │    │◄───►│  │Regional  │    │
│  │Server A  │    │     │  │Server B  │    │
│  └────┬─────┘    │     │  └────┬─────┘    │
│  ┌────┼────┐     │     │  ┌────┼────┐     │
│  │C1  │C2  │C3   │     │  │C4  │C5  │C6   │
│  └────┴────┘     │     │  └────┴────┘     │
└──────────────────┘     └──────────────────┘
```

**Advantages:**
- Addresses data heterogeneity by grouping similar clients
- Regulatory compliance (data sovereignty — data stays within geographic borders)
- Reduced cross-region communication

**Disadvantages:**
- May lead to divergent regional models
- Complex inter-region synchronization
- Requires careful region definition

---

### 2.3 Horizontal FL and Vertical FL — Detailed Architecture

#### 2.3.1 Horizontal Federated Learning Architecture

```
┌──────────────────────────────────────┐
│           Aggregation Server          │
│  Receives: model updates from all    │
│  Computes: weighted average          │
│  Sends: updated global model         │
└──────────────┬───────────────────────┘
          ┌────┼────┐
     ┌────▼──┐│┌───▼───┐
     │Client1│││Client2 │
     │       │││        │
     │Same   │││Same    │
     │Features│││Features│
     │Diff   │││Diff    │
     │Samples│││Samples │
     └───────┘│└────────┘
          ┌───▼───┐
          │Client3│
          │Same   │
          │Features│
          │Diff   │
          │Samples│
          └───────┘
```

**Workflow:**
1. Server distributes global model
2. Each client trains on its local samples (same feature space)
3. Clients send model parameter updates
4. Server aggregates via FedAvg

#### 2.3.2 Vertical Federated Learning Architecture

```
┌──────────────────────────────────────┐
│         Coordination Server          │
│  - Entity Alignment (PSI)            │
│  - Gradient Aggregation              │
│  - Encrypted Computation             │
└──────────────┬───────────────────────┘
          ┌────┼────┐
     ┌────▼──┐ ┌───▼───┐
     │Party A│ │Party B │
     │       │ │        │
     │Features│ │Features│
     │{f1,f2}│ │{f3,f4} │
     │       │ │+ Labels│
     │Same   │ │Same    │
     │Users  │ │Users   │
     └───────┘ └────────┘
```

**Workflow:**
1. **Entity Alignment**: Use Private Set Intersection (PSI) to find common users without revealing user identities
2. **Encrypted Model Training**:
   - Party A computes intermediate results using its features
   - Party B computes intermediate results using its features
   - Encrypted gradients are exchanged via the server
3. **Model Update**: Each party updates its own model component

**Key Difference:** In VFL, the model is split across parties (each party holds part of the model corresponding to their features), while in HFL, each party holds a complete copy of the model.

---

### 2.4 Comparison: Centralized vs. Hierarchical vs. Regional vs. Decentralized

| Feature | Centralized | Hierarchical | Regional | Decentralized |
|---------|:-----------:|:------------:|:--------:|:-------------:|
| Server Requirement | Single central | Multiple levels | Per-region | None |
| Scalability | Limited | Good | Good | Excellent |
| Fault Tolerance | Low | Medium | Medium | High |
| Communication Cost | High (bottleneck) | Distributed | Moderate | Varies |
| Convergence Speed | Fast | Medium | Medium | Slow |
| Privacy | Medium | Medium | Medium-High | High |
| Complexity | Low | Medium | Medium | High |
| Trust Model | Trust server | Trust hierarchy | Trust regional | Trust peers |
| Consistency | Strong | Eventual | Eventual | Weak |
| Latency | Variable | Lower (edge) | Lower (regional) | Depends on topology |

---

### 2.5 Case Study: Decentralized Federated Forest

#### Background:
The Decentralized Federated Forest is a variation of Federated Learning that applies Random Forest algorithms in a decentralized, privacy-preserving manner.

#### Architecture:
Instead of a neural network trained with gradient descent, this approach:
1. Each client builds local decision trees on their data
2. Trees are shared (in encrypted form) with peers
3. Ensemble prediction combines all trees without centralizing data

#### Key Innovation:
- **No central server**: Peer-to-peer tree exchange
- **Privacy preservation**: Secure computation protocols for tree evaluation
- **Heterogeneous data support**: Each tree captures local patterns

#### Process:
```
Step 1: Each client builds local Random Forest
Step 2: Clients exchange encrypted tree structures
Step 3: Each client creates an ensemble of all received trees
Step 4: Prediction uses majority voting across all trees
Step 5: Performance feedback is shared in a privacy-preserving manner
```

#### Advantages:
- Works well with tabular data (common in finance, healthcare)
- More interpretable than neural network-based FL
- No gradient leakage risk (no gradients shared)
- Robust to non-IID data (each tree learns local patterns)

#### Applications:
- **Credit Scoring**: Multiple banks build trees on their customer data
- **Medical Diagnosis**: Hospitals share decision trees without sharing patient data
- **Fraud Detection**: Financial institutions collaborate on detection rules

---

## UNIT III: Optimization Techniques (6 Hrs)

---

### 3.1 Federated Learning with Non-IID Data

#### 3.1.1 Understanding Non-IID Data

In real-world FL, data across clients is rarely IID. The non-IID nature manifests in several ways:

**Types of Non-IID-ness:**

1. **Feature Distribution Skew** ($P(x)$ varies): Same labels but different feature distributions
   - Example: Different hospitals have different imaging equipment
   
2. **Label Distribution Skew** ($P(y)$ varies): Different clients have different label proportions
   - Example: A user in Japan and a user in Brazil have different typing patterns
   
3. **Concept Shift** ($P(y|x)$ varies): Same features map to different labels
   - Example: "football" means different sports in US vs. UK
   
4. **Quantity Skew**: Clients have vastly different amounts of data
   - Example: Power users vs. casual users
   
5. **Temporal Skew**: Data distributions change over time differently on each client

#### Impact of Non-IID on FL:

| Effect | Description |
|--------|-------------|
| **Weight Divergence** | Local models drift apart due to different data distributions |
| **Slow Convergence** | More communication rounds needed |
| **Accuracy Drop** | Global model may perform poorly on individual clients |
| **Client Drift** | Local optimization moves away from global optimum |
| **Instability** | Training may oscillate or diverge |

Mathematical impact: When data is non-IID, $\nabla F_k(w) \neq \nabla F(w)$, so local updates push the model in different directions.

---

#### 3.1.2 Heterogeneity

**Statistical Heterogeneity**: Different data distributions across clients.

**Systems Heterogeneity**: Different computational capabilities, network bandwidth, and availability.

**Model Heterogeneity**: Clients may need different model architectures (e.g., smaller models for mobile, larger for servers).

#### Strategies to Handle Heterogeneity:

1. **Data Sharing**: Share a small public dataset with all clients
2. **Data Augmentation**: Generate synthetic data to balance distributions
3. **Clustering**: Group clients with similar data distributions
4. **Personalization**: Allow local model customization
5. **Regularization**: Constrain local updates to stay close to global model

---

#### 3.1.3 Stratification

**Stratification** in FL refers to organizing or grouping clients based on data characteristics to improve training efficiency.

**Stratified Sampling**:
- In each round, select clients from different strata (groups) to ensure diversity
- Groups based on: data size, label distribution, device type, geographic region

**Benefits:**
- Reduces variance in aggregated updates
- Improves convergence speed
- More representative global model

**Algorithm:**
```
1. Profile each client's data distribution (meta-data only)
2. Cluster clients into strata S₁, S₂, ..., Sₘ
3. In each round, sample proportionally from each stratum
4. Aggregate with stratum-aware weighting
```

---

#### 3.1.4 Local Update Rules

**Local SGD / Local Update:**
Each client performs multiple steps of SGD before communicating:

$$w_k^{t, \tau+1} = w_k^{t, \tau} - \eta \nabla F_k(w_k^{t, \tau})$$

Where $\tau = 0, 1, ..., E-1$ represents local iterations and $E$ is the number of local epochs.

**Key Hyperparameters:**
- **Local Epochs ($E$)**: More epochs = less communication, but more client drift
- **Local Batch Size ($B$)**: Affects local gradient estimation quality
- **Learning Rate ($\eta$)**: Must be carefully tuned for FL settings

---

### 3.2 FedAvg (Federated Averaging)

The foundational algorithm in Federated Learning, proposed by McMahan et al. (2017).

#### Algorithm:

```
Algorithm: FedAvg
══════════════════════════════════════════════════
Server Executes:
  Initialize w₀
  For each round t = 0, 1, 2, ..., T-1:
    m ← max(C · K, 1)         // C = fraction of clients
    Sₜ ← random set of m clients
    For each client k ∈ Sₜ in parallel:
      wₖᵗ⁺¹ ← ClientUpdate(k, wₜ)
    wₜ₊₁ ← Σₖ (nₖ/Σⱼnⱼ) · wₖᵗ⁺¹

ClientUpdate(k, w):
  𝓑 ← split 𝓓ₖ into batches of size B
  For each local epoch i = 1, ..., E:
    For each batch b ∈ 𝓑:
      w ← w − η · ∇ℓ(w; b)
  Return w
══════════════════════════════════════════════════
```

#### Key Parameters:
- **C**: Client fraction (e.g., 0.1 means 10% of clients per round)
- **E**: Number of local epochs
- **B**: Local mini-batch size  
- **η**: Learning rate

#### Aggregation Formula:

$$w_{t+1} = \sum_{k \in S_t} \frac{n_k}{\sum_{j \in S_t} n_j} w_k^{t+1}$$

#### Properties of FedAvg:
| Property | Details |
|----------|---------|
| Communication | Reduced by factor of $E \cdot \lceil n_k/B \rceil$ compared to FedSGD |
| Convergence | Proven for convex functions; empirically works for non-convex (DNNs) |
| Non-IID Handling | Degrades with high non-IID-ness |
| Simplicity | Easy to implement and understand |

---

### 3.3 FedAvg Variations

#### 3.3.1 FedSGD (Federated Stochastic Gradient Descent)

Special case of FedAvg where $E = 1$ and $B = n_k$ (one gradient computation per round):

$$w_{t+1} = w_t - \eta \sum_{k} \frac{n_k}{n} \nabla F_k(w_t)$$

- More communication rounds needed
- Better convergence guarantees
- Less client drift

#### 3.3.2 FedProx (Federated Proximal)

Adds a proximal term to the local objective to limit client drift:

$$\min_{w} F_k(w) + \frac{\mu}{2} \|w - w_t\|^2$$

where $\mu$ is the proximal coefficient and $w_t$ is the current global model.

**Benefit:** Prevents local models from drifting too far from the global model, especially useful for non-IID data.

**Local Update:**
$$w \leftarrow w - \eta \left( \nabla F_k(w) + \mu (w - w_t) \right)$$

#### 3.3.3 SCAFFOLD (Stochastic Controlled Averaging for FL)

Uses control variates to correct for client drift:

Each client maintains a control variate $c_k$ that estimates the update direction:

$$w_k \leftarrow w_k - \eta \left( \nabla F_k(w_k) - c_k + c \right)$$

where $c = \frac{1}{K} \sum_k c_k$ is the global control variate.

**Benefit:** Removes the client-drift problem, achieving faster convergence.

#### 3.3.4 FedMA (Federated Matched Averaging)

- Matches neurons across client models before averaging
- Uses Bayesian nonparametric methods
- Better handles model heterogeneity

#### 3.3.5 FedNova (Federated Normalized Averaging)

Normalizes local updates by the number of local steps to address the bias introduced by different amounts of local computation:

$$w_{t+1} = w_t - \sum_k \frac{n_k}{n} \cdot \frac{\tau_{eff}}{\tau_k} \cdot \Delta_k$$

where $\tau_k$ is the number of local steps by client $k$ and $\tau_{eff}$ is a normalized effective step count.

#### Comparison of FedAvg Variations:

| Algorithm | Key Idea | Non-IID Handling | Communication | Computation |
|-----------|----------|:----------------:|:-------------:|:-----------:|
| FedSGD | Single gradient per round | Good | High | Low |
| FedAvg | Multiple local epochs | Moderate | Low | Moderate |
| FedProx | Proximal regularization | Good | Low | Moderate |
| SCAFFOLD | Control variates | Excellent | Moderate (extra vars) | Moderate |
| FedMA | Neuron matching | Good | Low | High |
| FedNova | Normalized averaging | Good | Low | Moderate |

---

### 3.4 Advanced Optimization Techniques

#### 3.4.1 Adaptive Learning Rate

Standard SGD uses a fixed learning rate, which may not work well in FL's heterogeneous setting.

**FedAdam / FedAdagrad / FedYogi (Reddi et al., 2020):**

Apply adaptive optimization at the **server level**:

$$\Delta_t = \sum_k \frac{n_k}{n} (w_k^{t+1} - w_t) \quad \text{(pseudo-gradient)}$$

**FedAdam Server Update:**
$$m_t = \beta_1 m_{t-1} + (1-\beta_1) \Delta_t$$
$$v_t = \beta_2 v_{t-1} + (1-\beta_2) \Delta_t^2$$
$$w_{t+1} = w_t + \eta \frac{m_t}{\sqrt{v_t} + \epsilon}$$

**FedAdagrad:**
$$v_t = v_{t-1} + \Delta_t^2$$
$$w_{t+1} = w_t + \eta \frac{\Delta_t}{\sqrt{v_t} + \epsilon}$$

**FedYogi** (avoids aggressive increase of $v_t$):
$$v_t = v_{t-1} + (1 - \beta_2) \cdot \text{sign}(\Delta_t^2 - v_{t-1}) \cdot \Delta_t^2$$

#### 3.4.2 Momentum

**Server-Side Momentum (FedAvgM):**

$$w_{t+1} = w_t + \beta \cdot v_{t-1} + (1-\beta) \cdot \Delta_t$$

where $v_{t-1}$ is the previous momentum term and $\beta$ is the momentum coefficient.

**Client-Side Momentum (SlowMo):**
Each client uses momentum in local SGD, and the server applies slow momentum to the aggregated update.

#### 3.4.3 Weight Decay (L2 Regularization)

Local objective becomes:
$$\min_w F_k(w) + \frac{\lambda}{2} \|w\|^2$$

In FL, weight decay can be applied:
- **Client-side**: Each client adds $\lambda w$ to its gradient
- **Server-side**: After aggregation, apply $w_{t+1} = (1-\lambda) w_{t+1}$

**Note:** The interaction between local weight decay and FedAvg aggregation is subtle. Decoupled weight decay (AdamW-style) is often preferred.

#### 3.4.4 Learning Rate Scheduling in FL

Common schedules:
- **Step decay**: Reduce LR at fixed round intervals
- **Cosine annealing**: Smooth cyclical reduction
- **Warmup**: Start with small LR and increase
- **Per-round decay**: $\eta_t = \eta_0 / (1 + \alpha t)$

---

### 3.5 Meta-Learning for FL

Meta-learning ("learning to learn") is naturally suited to FL where each client represents a "task."

#### 3.5.1 Model-Agnostic Meta-Learning (MAML) for FL — Per-FedAvg

**Goal:** Find a global model that can be quickly fine-tuned to each client's data.

$$\min_w \sum_k \frac{n_k}{n} F_k\left(w - \alpha \nabla F_k(w)\right)$$

- The global model $w$ is a good initialization
- Each client performs 1–few gradient steps to personalize
- Similar to MAML (Finn et al., 2017)

#### 3.5.2 Federated Meta-Learning Workflow:

```
1. Server sends global model w
2. Each client k:
   a. Splits local data into support set Sₖ and query set Qₖ
   b. Computes adapted model: w'ₖ = w - α∇Fₖ(w; Sₖ)
   c. Evaluates on query set: loss = Fₖ(w'ₖ; Qₖ)
   d. Sends gradients of query loss w.r.t. w
3. Server aggregates meta-gradients
4. Server updates: w ← w - β · aggregated_meta_gradient
```

#### 3.5.3 Model Selection and Hyperparameter Tuning

**Challenges in FL:**
- Cannot do standard cross-validation (data is distributed)
- Hyperparameters interact: local LR, global LR, local epochs, batch size, client fraction
- Each client may need different hyperparameters

**Approaches:**

1. **Federated Hyperparameter Optimization (FedHPO)**:
   - Use Bayesian optimization across rounds
   - Evaluate hyperparameters on a held-out validation set on each client

2. **Hyperparameter Transfer**:
   - Tune on a small proxy dataset centrally
   - Transfer hyperparameters to federated setting

3. **Adaptive Methods**:
   - Use adaptive optimizers (FedAdam) that are less sensitive to LR choices
   - Per-client learning rate adaptation

4. **Neural Architecture Search (NAS) for FL**:
   - FedNAS: Automatically search for optimal architecture in FL

---

### 3.6 Case Study: Advanced Optimization Techniques for Autonomous Vehicles

#### Problem:
Multiple autonomous vehicle manufacturers want to collaboratively train a perception model (e.g., object detection) without sharing their proprietary driving data.

#### Challenges:
1. **Non-IID Data**: Different geographic regions, weather conditions, driving styles
2. **System Heterogeneity**: Different onboard computing capabilities (NVIDIA Jetson vs. custom ASICs)
3. **Communication Constraints**: Intermittent connectivity; models are large (hundreds of MB)
4. **Safety-Critical**: Model must be reliable; cannot tolerate degradation

#### FL Optimization Approach:

1. **Base Algorithm**: FedProx with proximal term $\mu = 0.01$ to handle non-IID driving data

2. **Adaptive Server Optimization**: FedAdam at the server
   - $\beta_1 = 0.9$, $\beta_2 = 0.99$, $\eta_{server} = 0.01$
   - Handles varying magnitudes of client updates

3. **Gradient Compression**: Use Top-K sparsification
   - Only transmit top 1% of gradient values
   - Reduces communication by ~100×
   - Error feedback mechanism preserves convergence

4. **Knowledge Distillation**: Instead of averaging parameters:
   - Each client trains a local model
   - Soft labels (predictions on a shared unlabeled dataset) are aggregated
   - Global model is retrained on aggregated soft labels
   - Handles model heterogeneity

5. **Personalization**: FedBN (Federated Batch Normalization)
   - Keep batch normalization layers local
   - Average all other layers globally
   - Accounts for different sensor calibrations

#### Results:
| Metric | Centralized | FedAvg | Optimized FL |
|--------|:-----------:|:------:|:------------:|
| mAP (object detection) | 82.3% | 74.1% | 80.7% |
| Communication Rounds | — | 500 | 200 |
| Communication Cost | — | 100% | 15% |
| Convergence Time | Baseline | 3× slower | 1.5× slower |

---

## UNIT IV: ML's Transition to Federated Learning (6 Hrs)

---

### 4.1 Machine Learning Basics

#### 4.1.1 Types of Machine Learning

**Supervised Learning:**
- Labeled data: $(x_i, y_i)$ pairs
- Goal: Learn mapping $f: X \rightarrow Y$
- Examples: Classification, Regression
- Algorithms: Linear Regression, SVM, Neural Networks, Decision Trees

**Unsupervised Learning:**
- Unlabeled data: $x_i$ only
- Goal: Find hidden patterns/structure
- Examples: Clustering, Dimensionality Reduction
- Algorithms: K-Means, PCA, Autoencoders

**Reinforcement Learning:**
- Agent interacts with environment
- Goal: Maximize cumulative reward
- Examples: Game playing, robotics
- Algorithms: Q-Learning, Policy Gradient

#### 4.1.2 Machine Learning Pipeline (Traditional)

```
┌──────────┐    ┌─────────────┐    ┌───────────┐    ┌──────────┐    ┌────────┐
│ Data      │───►│ Data        │───►│ Feature   │───►│ Model    │───►│Deploy- │
│Collection │    │Preprocessing│    │Engineering│    │Training  │    │ment    │
└──────────┘    └─────────────┘    └───────────┘    └──────────┘    └────────┘
     │                                                    │
     │    ┌──────────────────────────────────────────┐    │
     └───►│        Centralized Data Storage           │◄───┘
          │        (Data Warehouse / Lake)             │
          └──────────────────────────────────────────┘
```

#### 4.1.3 Key ML Concepts

- **Loss Function**: $\ell(y, \hat{y})$ — measures prediction error
- **Optimization**: $w^* = \arg\min_w \frac{1}{N}\sum_{i=1}^{N} \ell(f(x_i; w), y_i)$
- **Gradient Descent**: $w_{t+1} = w_t - \eta \nabla_w L(w_t)$
- **SGD**: Use mini-batch instead of full dataset
- **Regularization**: L1, L2, Dropout to prevent overfitting
- **Cross-Validation**: K-fold for model selection
- **Bias-Variance Tradeoff**: Balancing underfitting and overfitting

---

### 4.2 Challenges in Machine Learning Workflows

#### 4.2.1 Data Privacy

| Challenge | Description |
|-----------|-------------|
| **Regulatory Compliance** | GDPR (Europe), HIPAA (Healthcare, US), CCPA (California), DPDP (India) |
| **Data Sensitivity** | Medical records, financial data, personal communications |
| **Cross-border Restrictions** | Data cannot be transferred across national boundaries |
| **User Consent** | Users may not consent to data collection |
| **Re-identification Risk** | Even "anonymized" data can be de-anonymized |

**Example:** A hospital cannot send patient X-rays to a cloud server for model training due to HIPAA regulations.

#### 4.2.2 Communication Efficiency

- **Large Models**: Modern DNNs have millions/billions of parameters
- **Bandwidth Limitations**: Mobile devices have limited upload bandwidth
- **Latency**: Real-time applications need fast model updates
- **Cost**: Data transfer costs, especially in mobile networks

**Numbers for perspective:**
- ResNet-50: ~98 MB of parameters
- BERT-base: ~440 MB
- GPT-2: ~1.5 GB
- Transmitting these models in each round is prohibitive

#### 4.2.3 Data Ownership and Storage

| Issue | Description |
|-------|-------------|
| **Siloed Data** | Organizations don't want to share proprietary data |
| **Data Sovereignty** | Legal requirements to keep data within borders |
| **Data Quality** | Distributed data may be noisy, incomplete, or biased |
| **Data Labeling** | Expensive to label data, especially in specialized domains |
| **Storage Costs** | Centralizing data from multiple sources is expensive |

#### 4.2.4 Other Challenges

- **Scalability**: Training on massive datasets requires significant infrastructure
- **Fairness & Bias**: Centralized models may reflect biases in collected data
- **Availability**: Data owners may not always be available
- **Intellectual Property**: Models trained on proprietary data contain embedded IP

---

### 4.3 Transition Towards Federated Learning

#### 4.3.1 Why the Transition?

Traditional ML's centralized approach fails when:
1. Data is **legally restricted** from being centralized (GDPR, HIPAA)
2. Data is **too large or costly** to transfer
3. Data is **generated at the edge** in real-time
4. **Multiple organizations** want to collaborate without sharing data
5. **Users demand privacy** for their personal data

#### 4.3.2 The Transition Pathway

```
Traditional ML ──► Distributed ML ──► Federated Learning
                                       ▲
                                       │
Data Parallelism ──► Model Parallelism ─┘
```

**Stage 1: Centralized ML**
- All data in one place
- Single machine or cluster training
- Full access to all data

**Stage 2: Distributed ML (Data Parallelism)**
- Data split across machines in a cluster
- All machines in same data center (same organization)
- IID data distribution (deliberate splitting)
- Still centralized data ownership

**Stage 3: Federated Learning**
- Data stays at source (different organizations/devices)
- Non-IID, heterogeneous data
- Communication over the internet (slow, unreliable)
- Privacy preservation is a primary goal
- No central entity controls all data

#### 4.3.3 Key Differences in the Transition

| Aspect | Distributed ML | Federated Learning |
|--------|:--------------:|:------------------:|
| **Data Distribution** | Controlled, IID | Uncontrolled, Non-IID |
| **Data Access** | All nodes access all data | Each node accesses only local data |
| **Network** | High-bandwidth data center | Low-bandwidth, unreliable internet |
| **Scale** | 10s–100s of nodes | 100s–millions of clients |
| **Failure Handling** | Rare failures | Frequent dropouts |
| **Primary Goal** | Speed up training | Enable training without data sharing |
| **Privacy** | Not a concern (same org) | Primary concern |
| **Data Ownership** | Single entity | Multiple entities |

---

### 4.4 Converting ML to FL — Step-by-Step

#### Step 1: Identify Data Sources
- Who holds the data? (devices, organizations)
- What privacy constraints exist?

#### Step 2: Define the Learning Objective
- Same as centralized ML: minimize a loss function
- But the objective is decomposed across clients:
  $$F(w) = \sum_k \frac{n_k}{n} F_k(w)$$

#### Step 3: Select FL Architecture
- Horizontal, Vertical, or Transfer FL?
- Centralized, Hierarchical, or Decentralized?

#### Step 4: Adapt the Training Algorithm
- Replace centralized SGD with local SGD + aggregation
- Handle non-IID data (FedProx, SCAFFOLD)
- Add privacy mechanisms (DP, Secure Aggregation)

#### Step 5: Address Communication Efficiency
- Model compression (quantization, pruning, sparsification)
- Reduce communication rounds (more local epochs)
- Asynchronous updates

#### Step 6: Implement Privacy & Security
- Differential Privacy
- Secure Aggregation
- Robustness against adversaries

#### Step 7: Deploy and Monitor
- Client selection and scheduling
- Model versioning
- Performance monitoring across clients

---

### 4.5 Comparison: Federated Learning vs. Machine Learning

| Dimension | Traditional ML | Federated Learning |
|-----------|:-------------:|:------------------:|
| **Data Location** | Centralized | Distributed, remains local |
| **Data Access** | Full access | No raw data access |
| **Training** | On central server | On distributed clients |
| **Model Updates** | Local computation | Communicated across network |
| **Privacy** | Risk of data breaches | Privacy by design |
| **Communication** | Minimal (data→server once) | High (multiple rounds) |
| **Data Distribution** | IID (controlled) | Often Non-IID |
| **Convergence** | Well-understood | Challenging (non-IID, partial participation) |
| **Scalability** | Limited by central compute | Limited by communication |
| **Regulatory** | May violate GDPR/HIPAA | Compliant by design |
| **Model Quality** | Generally higher | May be slightly lower |
| **Debugging** | Easy (access all data) | Hard (no data visibility) |
| **Fairness** | Monitor centrally | Hard to ensure across clients |
| **Computational Cost** | Borne by server | Distributed across clients |

---

### 4.6 Case Study: Federated Learning for Deep Learning Solutions

#### Problem:
A consortium of 5 medical imaging centers wants to train a deep learning model for detecting diabetic retinopathy from retinal fundus images.

#### Traditional ML Approach:
- Collect all ~50,000 images in one central server
- **Problem**: HIPAA/GDPR prevents sharing patient images
- **Problem**: Images contain identifiable patient information
- **Problem**: Hospitals don't trust the central entity

#### Federated Learning Solution:

**Model**: ResNet-18 for binary classification (diabetic retinopathy vs. normal)

**Setup**:
| Hospital | Samples | Demographics | Equipment |
|----------|---------|-------------|-----------|
| Hospital A | 12,000 | Asian population | Canon CR-2 |
| Hospital B | 8,000 | European population | Topcon NW400 |
| Hospital C | 15,000 | Mixed population | Zeiss Visucam |
| Hospital D | 5,000 | African population | Nikon NX-70 |
| Hospital E | 10,000 | Latin American | Canon CX-1 |

**FL Configuration:**
- Algorithm: FedAvg with FedProx ($\mu = 0.01$)
- Local epochs: $E = 5$
- Communication rounds: 100
- Client fraction: $C = 1.0$ (all hospitals participate each round)
- Local learning rate: $\eta = 0.01$ with cosine annealing
- Differential Privacy: ($\epsilon = 8, \delta = 10^{-5}$)

**Results:**

| Approach | AUC-ROC | Sensitivity | Specificity |
|----------|:-------:|:-----------:|:-----------:|
| Local (Hospital A only) | 0.87 | 0.82 | 0.85 |
| Local (Hospital C only) | 0.89 | 0.85 | 0.86 |
| Centralized (ideal) | 0.95 | 0.92 | 0.93 |
| FedAvg | 0.92 | 0.88 | 0.90 |
| FedAvg + FedProx | 0.93 | 0.90 | 0.91 |
| FedAvg + DP | 0.91 | 0.87 | 0.89 |

**Key Observations:**
1. FL achieves ~97% of centralized performance
2. FedProx improves upon FedAvg due to heterogeneous data (different cameras, populations)
3. Differential Privacy causes minor accuracy drop (~2%)
4. Every hospital benefits — especially Hospital D with smallest dataset

**Technical Challenges Addressed:**
- **Non-IID**: Different populations and camera types → FedProx
- **Communication**: Only model weights (~45MB) transmitted, not images (~2GB per hospital)
- **Privacy**: DP added; no patient images leave hospitals
- **Fairness**: Monitored per-hospital performance to ensure equitable improvement

---

## UNIT V: Privacy & Security (6 Hrs)

---

### 5.1 Protecting Against Data Leakage in FL

#### 5.1.1 The Privacy Paradox in FL

While FL keeps raw data local, the shared model updates can leak information:

**Threat Model:**
- **Honest-but-curious server**: Follows protocol but tries to infer information from received updates
- **Malicious clients**: Send corrupted updates or try to extract others' data
- **External adversary**: Intercepts communication between clients and server

#### 5.1.2 Types of Data Leakage

1. **Gradient Leakage / Deep Leakage from Gradients (DLG)**
   - Zhu et al. (2019) showed that shared gradients can be inverted to reconstruct training images
   - Attack: Given gradient $\nabla_w L(x, y; w)$, find $x^*, y^*$ such that:
     $$\min_{x^*, y^*} \|\nabla_w L(x^*, y^*; w) - \nabla_w L(x, y; w)\|^2$$
   - Particularly effective with small batch sizes

2. **Membership Inference Attack**
   - Determine whether a specific data point was in a client's training set
   - Uses the model's confidence/output distribution
   - Shadow model training approach (Shokri et al., 2017)

3. **Model Inversion Attack**
   - Reconstruct representative training data from the model
   - Given class label $y$, find $x^*$ that maximizes model confidence:
     $$x^* = \arg\max_x P(y | x; w)$$

4. **Attribute Inference Attack**
   - Infer sensitive attributes of training data
   - Even if not directly trained on sensitive attributes

5. **Property Inference Attack**
   - Infer properties of a client's training data that are not related to the main task
   - Example: Infer gender distribution of a hospital's patients from a disease prediction model

---

### 5.2 Private Parameter Aggregation for FL

#### 5.2.1 Secure Aggregation

**Goal:** The server should only learn the aggregate update $\sum_k w_k$, not individual updates $w_k$.

**Masking-based Secure Aggregation (Bonawitz et al., 2017):**

```
Protocol:
1. Key Agreement: Each pair of clients (i, j) agrees on a shared secret sᵢⱼ
2. Masking: Client k computes masked update:
   ŵₖ = wₖ + Σⱼ>ₖ PRG(sₖⱼ) - Σⱼ<ₖ PRG(sⱼₖ)
   where PRG is a pseudorandom generator
3. Aggregation: Server sums masked updates:
   Σₖ ŵₖ = Σₖ wₖ (masks cancel out!)
4. Dropout Handling: Use Shamir's secret sharing for robustness
```

**Properties:**
- Server sees only the sum, not individual contributions
- Tolerates client dropouts (up to a threshold)
- Communication overhead: $O(K^2)$ for key agreement, but can be optimized

#### 5.2.2 Differential Privacy (DP)

**Definition:** A randomized mechanism $\mathcal{M}$ satisfies $(\epsilon, \delta)$-differential privacy if for all datasets $D, D'$ differing by one record, and for all subsets $S$ of outputs:

$$P[\mathcal{M}(D) \in S] \leq e^\epsilon \cdot P[\mathcal{M}(D') \in S] + \delta$$

**Intuition:** The mechanism's output doesn't change much whether or not any single individual's data is included.

**DP in FL — Two Levels:**

**a) Client-Level DP (CDP / User-Level DP):**
- Protects entire client's contribution
- Noise added at client before sending update
- Stronger privacy guarantee

**b) Record-Level DP (Local DP / LDP):**
- Protects individual records within a client
- Each record is perturbed before training

**DP-FedAvg Algorithm:**
```
Algorithm: DP-FedAvg
═══════════════════════════════════
For each round t:
  Select clients Sₜ
  For each client k ∈ Sₜ:
    Δₖ = ClientUpdate(k, wₜ) - wₜ     // model update
    Δ̂ₖ = Δₖ / max(1, ||Δₖ||₂/C)       // clip to bound sensitivity
    Δ̃ₖ = Δ̂ₖ + 𝒩(0, σ²C²I)            // add Gaussian noise
  
  wₜ₊₁ = wₜ + (1/|Sₜ|) Σₖ Δ̃ₖ
═══════════════════════════════════
```

**Key Parameters:**
- **C**: Clipping bound (bounds the sensitivity)
- **σ**: Noise multiplier
- **ε**: Privacy budget (lower = more private)
- **δ**: Failure probability

**Privacy-Accuracy Tradeoff:**
| ε Value | Privacy Level | Model Accuracy Impact |
|---------|:------------:|:--------------------:|
| 0.1 | Very high privacy | Significant accuracy loss |
| 1.0 | High privacy | Moderate accuracy loss |
| 8.0 | Moderate privacy | Small accuracy loss |
| 100+ | Weak privacy | Negligible accuracy loss |

#### 5.2.3 Homomorphic Encryption (HE)

**Concept:** Perform computations on encrypted data without decrypting it.

$$\text{Enc}(a) \oplus \text{Enc}(b) = \text{Enc}(a + b)$$

**Types:**
- **Partially HE (PHE)**: Supports only addition (e.g., Paillier) or only multiplication
- **Somewhat HE (SHE)**: Supports limited operations
- **Fully HE (FHE)**: Supports arbitrary computation (e.g., CKKS, BFV)

**HE in FL:**
1. Clients encrypt their model updates: $\text{Enc}(w_k)$
2. Server aggregates in encrypted domain: $\sum_k \text{Enc}(w_k) = \text{Enc}(\sum_k w_k)$
3. Server sends encrypted aggregate back
4. Clients decrypt using shared key

**Trade-offs:**
| Aspect | Pro | Con |
|--------|-----|-----|
| Privacy | Strong cryptographic guarantees | |
| Computation | | 100-10000× slower |
| Communication | | Ciphertexts are larger |
| Flexibility | | Limited operations (esp. PHE) |

---

### 5.3 Data Leakage in FL — Detailed Analysis

#### 5.3.1 Deep Leakage from Gradients (DLG)

**Attack Algorithm:**

```
DLG Attack (Zhu et al., 2019):
═══════════════════════════════════
Given: gradient ∇w = ∇L(x_real, y_real; w)
Goal: Recover x_real, y_real

1. Initialize dummy data x', y' randomly
2. Repeat for T iterations:
   a. Compute dummy gradient: ∇w' = ∇L(x', y'; w)
   b. Compute distance: D = ||∇w' - ∇w||²
   c. Update dummy data: x' ← x' - α · ∂D/∂x'
                          y' ← y' - α · ∂D/∂y'
3. Return x', y' (recovered data)
═══════════════════════════════════
```

**Improved Variants:**
- **iDLG**: Analytically extracts label from gradient direction
- **InvertingGradients**: Uses cosine similarity instead of L2 distance, adds regularization
- **GradInversion**: Handles batches of data

#### 5.3.2 Defenses Against Data Leakage

| Defense | Mechanism | Effectiveness | Cost |
|---------|-----------|:------------:|:----:|
| **Differential Privacy** | Add noise to gradients | High | Accuracy loss |
| **Gradient Compression** | Sparsify gradients | Medium | Some accuracy loss |
| **Gradient Perturbation** | Add structured noise | Medium | Moderate accuracy loss |
| **Secure Aggregation** | Server sees only sum | High (vs. server) | Communication overhead |
| **Larger Batch Size** | Average over more samples | Medium | May affect convergence |
| **Gradient Clipping** | Bound gradient magnitude | Medium | Minimal |
| **InstaHide** | Mix data and add random sign flips | Medium | Moderate |

---

### 5.4 Dealing with Byzantine Threats to Neural Networks

#### 5.4.1 Byzantine Threat Model

A **Byzantine client** can send arbitrary or strategically crafted model updates to degrade the global model.

**Types of Byzantine Attacks:**

1. **Random Attack**: Send random model weights
   $$w_k^{byzantine} \sim \mathcal{N}(0, \sigma^2 I)$$

2. **Sign-Flipping Attack**: Negate the true gradient
   $$w_k^{byzantine} = w_t - \eta \cdot (-\nabla F_k(w_t)) = w_t + \eta \nabla F_k(w_t)$$

3. **Scaling Attack**: Send scaled-up legitimate updates
   $$w_k^{byzantine} = w_t + \gamma \cdot (w_k - w_t), \quad \gamma \gg 1$$

4. **Targeted Attack (Backdoor)**: Insert a hidden trigger
   - Model works normally on clean data
   - Misclassifies inputs with a specific pattern (e.g., a pixel patch)

5. **Sybil Attack**: Create multiple fake clients to amplify influence

6. **Free-Riding Attack**: Send zero or minimal updates while benefiting from the global model

#### 5.4.2 Byzantine-Resilient Aggregation Rules

**a) Median-Based Aggregation (Coordinate-Wise Median)**
$$w_{t+1}^{(j)} = \text{median}\{w_1^{(j)}, w_2^{(j)}, ..., w_K^{(j)}\}$$

For each parameter coordinate, take the median instead of the mean. Tolerates up to $f < K/2$ Byzantine clients.

**b) Trimmed Mean**
For each coordinate, remove the largest and smallest $f$ values, then average:
$$w_{t+1}^{(j)} = \frac{1}{K-2f} \sum_{k=f+1}^{K-f} w_{(k)}^{(j)}$$

where $w_{(k)}^{(j)}$ are the sorted values of the $j$-th coordinate.

**c) Krum (Blanchard et al., 2017)**
Select the update closest to its neighbors:
$$\text{Krum}(w_1, ..., w_K) = w_{k^*}$$
where $k^* = \arg\min_k \sum_{j \in \text{nearest}(k, K-f-2)} \|w_k - w_j\|^2$

**d) Bulyan**
Combines Krum selection with trimmed mean:
1. Use Krum to select $K - 2f$ updates
2. Apply trimmed mean on selected updates

**e) RFA (Robust Federated Averaging)**
Use geometric median instead of arithmetic mean:
$$w_{t+1} = \arg\min_w \sum_k \|w - w_k\|_2$$

This is the geometric median, which is more robust to outliers.

#### 5.4.3 Comparison of Byzantine-Resilient Methods

| Method | Byzantine Tolerance | Computational Cost | Accuracy Impact |
|--------|:------------------:|:------------------:|:---------------:|
| FedAvg (no defense) | 0 | O(K·d) | None |
| Coordinate Median | < K/2 | O(K·d·log K) | Moderate |
| Trimmed Mean | < K/4 | O(K·d·log K) | Low |
| Krum | < K/3 | O(K²·d) | Moderate |
| Bulyan | < K/4 | O(K²·d) | Low |
| RFA (Geometric Median) | < K/2 | O(K·d·T_iter) | Low |

---

### 5.5 Case Study: Federated Learning for Collaborative Financial Crimes Detection

#### Background:
Multiple banks want to collaboratively detect money laundering and fraud without sharing customer transaction data (due to banking secrecy laws and competition concerns).

#### Problem:
- Money laundering involves transaction chains across banks
- No single bank sees the full picture
- Regulatory requirements (BSA/AML) demand detection
- Sharing data violates privacy laws and competitive interests

#### FL-Based Solution:

**Architecture: Vertical Federated Learning + Secure Aggregation**

```
┌───────────────────────────────┐
│   Secure Aggregation Server   │
│   (Neutral Third Party)       │
└──────────────┬────────────────┘
          ┌────┼────┐
     ┌────▼──┐ ┌───▼───┐
     │Bank A │ │Bank B │
     │Trans. │ │Trans. │
     │Data   │ │Data   │
     │(feat.)│ │(feat.)│
     └───────┘ └───────┘
```

**Implementation Details:**

1. **Entity Alignment**: Use Private Set Intersection (PSI) to find common account holders
   - Banks encrypt customer IDs and find intersections
   - Neither bank learns about the other's unique customers

2. **Model**: Gradient Boosted Decision Trees (for interpretability, required by regulators)
   - Split learning: Each bank computes partial features for the tree
   - Secure aggregation combines partial computations

3. **Privacy Techniques:**
   - **Differential Privacy**: ε = 5 per round
   - **Secure Multi-Party Computation**: For computing split points in trees
   - **Homomorphic Encryption**: For gradient aggregation

4. **Security Against Byzantine Threats:**
   - Banks are known entities (cross-silo), so Sybil attacks are unlikely
   - Verification of update magnitudes (detect scaled attacks)
   - Audit trails for regulatory compliance

#### Results:
| Metric | Bank A Alone | Bank B Alone | Federated Model |
|--------|:-----------:|:-----------:|:---------------:|
| Precision | 0.72 | 0.68 | 0.89 |
| Recall | 0.65 | 0.61 | 0.84 |
| F1-Score | 0.68 | 0.64 | 0.86 |
| False Positive Rate | 8.2% | 9.1% | 3.5% |
| Detection of Cross-bank Laundering | 22% | 18% | 78% |

**Key Insight:** The federated model dramatically improves cross-bank money laundering detection (from ~20% to ~78%) because it can see patterns spanning multiple banks without either bank sharing raw transaction data.

---

## UNIT VI: Applications and Future Scope (6 Hrs)

---

### 6.1 Federated Learning for Healthcare

#### 6.1.1 Privacy-Preserving Diagnosis

**Problem:** Medical data (EHRs, imaging, genomics) is highly sensitive and regulated (HIPAA, GDPR).

**FL Solution:**
- Train diagnostic models across hospitals without centralizing patient data
- Each hospital keeps its data locally
- Only model updates are shared

**Applications:**

1. **Medical Imaging**: 
   - CT scan analysis for COVID-19 detection
   - Mammography for breast cancer screening
   - Retinal imaging for diabetic retinopathy
   - Brain MRI for tumor detection

2. **Electronic Health Records (EHR)**:
   - Disease prediction from patient records
   - Drug interaction prediction
   - Patient readmission prediction

3. **Genomics**:
   - Genome-wide association studies (GWAS)
   - Rare disease identification
   - Pharmacogenomics

#### 6.1.2 Treatment Planning

**Personalized Medicine via FL:**
- Train treatment response models across hospitals
- Account for diverse patient populations
- Maintain personalization through per-hospital fine-tuning

**Example: Federated Drug Discovery**
- Pharmaceutical companies train molecular property prediction models
- Each company contributes without revealing proprietary compound libraries
- Accelerates drug discovery pipeline

#### 6.1.3 Real-World Healthcare FL Projects

| Project | Participants | Application | Framework |
|---------|-------------|-------------|-----------|
| NVIDIA FLARE/Clara | 20+ hospitals globally | Brain tumor segmentation | NVIDIA Clara |
| HealthChain | European hospitals | Breast cancer treatment | Custom |
| MELLODDY | 10 pharma companies | Drug discovery | OWKIN |
| FedAI COVID-19 | Multiple institutions | COVID-19 diagnosis | FATE |

---

### 6.2 Federated Learning for Finance

#### 6.2.1 Fraud Detection

**Challenge:** Fraud patterns evolve; no single institution sees all fraud types.

**FL Approach:**
- Banks collaborate on fraud detection models
- Each bank trains on its transaction data
- Model captures diverse fraud patterns without data sharing

**Model Architecture:**
```
Transaction → Feature Extraction → Neural Network → Fraud/Not Fraud
   Data         (per bank)           (federated)       (prediction)
```

#### 6.2.2 Risk Assessment

**Credit Scoring:**
- Multiple financial institutions train a unified credit scoring model
- Vertical FL: Bank has income data, e-commerce platform has spending data
- Combined model is more accurate than either alone

**Anti-Money Laundering (AML):**
- As detailed in Unit V case study
- Transaction graph analysis across institutions

#### 6.2.3 Other Financial Applications

- **Algorithmic Trading**: Collaborative strategy learning without sharing proprietary strategies
- **Insurance Underwriting**: Multi-insurer risk models
- **Regulatory Compliance**: Shared compliance models across institutions

---

### 6.3 Federated Learning for IoT

#### 6.3.1 Edge Computing

**FL at the Edge:**
- IoT devices generate massive amounts of data
- Sending all data to cloud is impractical (bandwidth, latency, privacy)
- FL enables learning directly at the edge

**Architecture:**
```
Cloud Server (Global Aggregation)
      │
  ┌───┼───┐
  │       │
Edge 1  Edge 2  (Regional Aggregation)
  │      │
┌─┼─┐  ┌─┼─┐
│   │  │   │
D1  D2 D3  D4  (IoT Devices: sensors, cameras, etc.)
```

#### 6.3.2 Distributed Sensing

**Applications:**
1. **Smart Home**: Devices learn user preferences locally
2. **Smart City**: Traffic cameras, air quality sensors, noise monitors
3. **Industrial IoT**: Predictive maintenance across factory equipment
4. **Wearables**: Health monitoring (heart rate, activity recognition)
5. **Agriculture**: Crop monitoring, soil analysis across farms

**Challenges for IoT FL:**
| Challenge | Description | Solution |
|-----------|-------------|----------|
| Resource Constraints | Limited CPU, memory, battery | Model compression, quantization |
| Connectivity | Intermittent, low bandwidth | Asynchronous FL, compression |
| Heterogeneity | Diverse devices and data | FedProx, personalization |
| Scale | Billions of devices | Hierarchical aggregation |
| Security | Physical access to devices | Secure enclaves, attestation |

---

### 6.4 Automotive Industry

**Applications:**
1. **Autonomous Driving**: Perception models (object detection, lane detection)
2. **Predictive Maintenance**: Component failure prediction across vehicle fleets
3. **Traffic Prediction**: Learning from multiple vehicles' GPS data
4. **Driver Behavior Analysis**: Personalized driving assistance
5. **V2X Communication**: Vehicle-to-Everything learning

**Example: Federated Autonomous Driving**
```
┌─────────────────────────┐
│  Cloud Training Server  │
│  (Global Model)         │
└────────────┬────────────┘
        ┌────┼────┐
   ┌────▼──┐ ┌───▼───┐
   │Car 1  │ │Car 2  │ ... (millions of vehicles)
   │Camera │ │Camera │
   │LiDAR  │ │LiDAR  │
   │GPS    │ │GPS    │
   │IMU    │ │IMU    │
   └───────┘ └───────┘
```

---

### 6.5 Synchronous FL of Deep Neural Decision Forests

**Concept:** Combine Deep Neural Networks with Decision Forests in a federated setting.

**Deep Neural Decision Forest (DNDF):**
- Uses neural network features as input to a differentiable decision forest
- Routing decisions at each tree node are computed by the neural network
- Leaf nodes contain learned distributions

**Federated DNDF:**
1. Each client trains the neural network + decision forest locally
2. Synchronous aggregation: All clients finish before aggregation
3. Aggregate neural network parameters via FedAvg
4. Aggregate leaf distributions via weighted averaging
5. Tree structure is shared (same architecture)

**Benefits:**
- More interpretable than pure DNNs
- Handles mixed data types (tabular + image)
- Decision boundaries are more robust to non-IID data

---

### 6.6 Topology-Aware Federated Learning in Edge Computing

**Problem:** Standard FL ignores the network topology between devices and edge servers, leading to inefficient communication.

**Topology-Aware FL:**
1. **Topology Discovery**: Map the network graph of devices and edge servers
2. **Hierarchical Aggregation**: Aggregate based on network proximity
3. **Communication-Efficient Routing**: Send updates along shortest/fastest paths
4. **Load Balancing**: Distribute aggregation load based on network capacity

**Algorithm:**
```
1. Construct network topology graph G = (V, E)
   - V = devices ∪ edge servers ∪ cloud
   - E = communication links with bandwidth/latency
2. Partition devices into clusters based on network proximity
3. Each cluster has a designated aggregation node
4. Hierarchical aggregation: device → cluster head → cloud
5. Adapt round timing to slowest device in each cluster
```

**Benefits:**
- Reduced communication latency (up to 3×)
- Better utilization of network resources
- Handles heterogeneous network conditions

---

### 6.7 Microservice-Based Platform for Federated Learning

**Architecture:** Decompose the FL system into loosely coupled microservices.

```
┌─────────────────────────────────────────────────┐
│              FL Microservice Platform           │
│                                                 │
│  ┌──────────┐ ┌──────────┐ ┌────────────────┐   │
│  │Client    │ │Aggregat- │ │Model           │   │
│  │Selection │ │ion       │ │Registry        │   │
│  │Service   │ │Service   │ │Service         │   │
│  └──────────┘ └──────────┘ └────────────────┘   │
│                                                 │
│  ┌──────────┐ ┌──────────┐ ┌────────────────┐   │
│  │Privacy   │ │Monitoring│ │Communication   │   │
│  │Service   │ │Service   │ │Gateway         │   │
│  │(DP, SA)  │ │(Metrics) │ │(gRPC/REST)     │   │
│  └──────────┘ └──────────┘ └────────────────┘   │
│                                                 │
│  ┌──────────┐ ┌──────────┐ ┌────────────────┐   │
│  │Scheduling│ │Security  │ │Data            │   │
│  │Service   │ │Service   │ │Validation      │   │
│  │          │ │(Auth)    │ │Service         │   │
│  └──────────┘ └──────────┘ └────────────────┘   │
└─────────────────────────────────────────────────┘
```

**Microservices:**

1. **Client Selection Service**: Selects and schedules clients for each round
2. **Aggregation Service**: Implements FedAvg, FedProx, etc.
3. **Model Registry**: Stores model versions and checkpoints
4. **Privacy Service**: Manages DP, Secure Aggregation, encryption
5. **Monitoring Service**: Tracks metrics, convergence, anomalies
6. **Communication Gateway**: Handles client-server communication
7. **Scheduling Service**: Manages round timing, async/sync modes
8. **Security Service**: Authentication, authorization, access control
9. **Data Validation Service**: Validates model updates (Byzantine detection)

**Benefits:**
- Independent scaling of each component
- Easy to update individual services
- Technology-agnostic (each service can use different tech stack)
- Fault isolation
- Easier testing and debugging

---

### 6.8 Integrating Federated Learning with Digital Twins

#### What are Digital Twins?
A **Digital Twin** is a virtual replica of a physical system (machine, building, city) that is continuously updated with real-time data.

#### Integration Architecture:

```
Physical World          Digital World
┌────────────┐         ┌────────────────┐
│ Physical   │ sensor  │ Digital Twin   │
│ Device     │ data    │ (Virtual       │
│ (factory   │────────►│  Replica)      │
│  machine)  │         │                │
└────────────┘         └───────┬────────┘
                              │
                              │ simulation data
                              ▼
                       ┌──────────────┐
                       │ FL Training  │
                       │ (Local Model)│
                       └──────┬───────┘
                              │ model updates
                              ▼
                       ┌──────────────┐
                       │ FL Server    │
                       │ (Aggregation)│
                       └──────────────┘
```

**Use Cases:**

1. **Manufacturing**: Each factory has a digital twin of its production line; FL trains quality prediction models across factories

2. **Smart Cities**: Digital twins of traffic systems; FL enables collaborative traffic optimization without sharing city-specific data

3. **Healthcare**: Digital twins of patients; FL enables treatment optimization across hospital digital twin systems

4. **Energy**: Digital twins of power grids; FL enables predictive maintenance across utilities

**Benefits of Integration:**
- Digital twins provide simulation data to augment real data
- FL enables cross-organization learning without sharing digital twin data
- Simulation-based data augmentation reduces non-IID effects
- Real-time model updates from both physical and simulated data

---

### 6.9 Case Study: Federated Learning for Automotive Industry

#### Scenario:
Three autonomous vehicle companies (Company A, B, C) want to collaboratively improve their object detection models for safer self-driving.

#### Setup:

| Company | Fleet Size | Primary Region | Data Characteristics |
|---------|-----------|---------------|---------------------|
| A | 50,000 vehicles | USA (urban) | Highway, suburban driving |
| B | 30,000 vehicles | Europe (mixed) | City streets, rain, snow |
| C | 20,000 vehicles | Asia (dense urban) | Dense traffic, motorcycles |

#### FL Architecture: Hierarchical + Cross-Silo

```
                ┌──────────────┐
                │  Cloud       │
                │  Aggregator  │
                └──────┬───────┘
           ┌───────────┼───────────┐
     ┌─────▼────┐ ┌────▼─────┐ ┌──▼──────┐
     │Company A │ │Company B │ │Company C│
     │Server    │ │Server    │ │Server   │
     └────┬─────┘ └────┬─────┘ └────┬────┘
     ┌────┼────┐  ┌────┼────┐  ┌────┼────┐
     │Vehicles │  │Vehicles │  │Vehicles │
     └─────────┘  └─────────┘  └─────────┘
```

**Level 1**: Vehicles → Company Server (cross-device FL within each company)
**Level 2**: Company Servers → Cloud (cross-silo FL across companies)

#### Technical Implementation:

1. **Model**: YOLOv5 for object detection
2. **Optimization**: 
   - FedProx at Level 1 (non-IID across vehicles)
   - FedAdam at Level 2 (non-IID across companies)
3. **Communication**: 
   - Level 1: Over cellular network, gradient compression (Top-10%)
   - Level 2: Over dedicated inter-company network, full model exchange
4. **Privacy**:
   - Level 1: Local DP (ε = 10)
   - Level 2: Secure Aggregation + Company-level DP (ε = 5)
5. **Personalization**: 
   - FedBN: Keep batch normalization layers per-company
   - Fine-tuning: Each company fine-tunes final layers on own data

#### Results:

| Metric | Company A Alone | Company B Alone | Company C Alone | Federated Model |
|--------|:-------------:|:-------------:|:-------------:|:--------------:|
| mAP@0.5 | 0.78 | 0.75 | 0.72 | 0.85 |
| Pedestrian Detection | 0.82 | 0.79 | 0.85 | 0.91 |
| Rain Performance | 0.65 | 0.80 | 0.60 | 0.82 |
| Dense Traffic | 0.70 | 0.68 | 0.82 | 0.84 |
| Night Driving | 0.72 | 0.74 | 0.70 | 0.81 |

**Key Observations:**
1. FL model outperforms all individual models across all scenarios
2. Company B's rain data improves performance for Companies A and C
3. Company C's dense traffic data improves urban driving for all
4. Night driving (underrepresented in all datasets) improves through collective learning
5. No company shares its proprietary driving data

---

### 6.10 Future Directions in Federated Learning

#### 6.10.1 Current Research Trends

1. **Federated Learning with Foundation Models (LLMs)**
   - Fine-tuning GPT/LLaMA models in federated settings
   - Federated prompt tuning (LoRA, adapter-based FL)
   - Communication-efficient fine-tuning of billion-parameter models

2. **Personalized Federated Learning**
   - Per-client model adaptation
   - Multi-task FL, clustered FL
   - Mixture of global and local models

3. **Fairness in FL**
   - Ensuring equitable model performance across all clients
   - Addressing bias in non-IID settings
   - Client-level fairness constraints

4. **Federated Unlearning**
   - Removing a client's contribution from the model
   - Right to be forgotten (GDPR compliance)
   - Efficient retraining without the removed client's data

5. **Federated Continual Learning**
   - Handling evolving data distributions over time
   - Avoiding catastrophic forgetting in FL
   - Online FL with streaming data

6. **Incentive Mechanisms**
   - Motivating clients to participate and contribute quality data
   - Game-theoretic approaches (Shapley value for contribution assessment)
   - Blockchain-based reward systems

7. **FL for Generative AI**
   - Federated training of GANs, VAEs, Diffusion Models
   - Federated synthetic data generation
   - Privacy-preserving text generation

8. **Cross-Modal FL**
   - Clients have different data modalities (text, image, audio)
   - Multi-modal fusion in federated settings

#### 6.10.2 Open Challenges

| Challenge | Current State | Research Direction |
|-----------|:------------:|:------------------:|
| Communication Efficiency | Compression, fewer rounds | Novel protocols, one-shot FL |
| Non-IID Data | FedProx, SCAFFOLD | Theoretical understanding, adaptive methods |
| System Heterogeneity | Async FL, partial participation | Heterogeneous model architectures |
| Privacy | DP, Secure Aggregation | Formal guarantees with utility preservation |
| Scalability | Hierarchical FL | Billion-client systems |
| Debugging | Limited | Federated debugging tools |
| Benchmarking | LEAF, FedML | Standardized benchmarks |
| Regulation | Ad-hoc | Legal frameworks for FL |

---

## Summary Tables

### Key Algorithms Comparison

| Algorithm | Year | Key Innovation | Best For |
|-----------|:----:|---------------|----------|
| FedSGD | 2016 | Distributed SGD | Baseline, convex problems |
| FedAvg | 2017 | Multiple local epochs | General FL |
| FedProx | 2020 | Proximal regularization | Non-IID data |
| SCAFFOLD | 2020 | Control variates | Client drift reduction |
| FedNova | 2020 | Normalized averaging | Heterogeneous local computation |
| FedAdam | 2021 | Adaptive server optimizer | Large-scale FL |
| FedBN | 2021 | Local batch norm | Domain-shifted data |
| Per-FedAvg | 2020 | Meta-learning personalization | Personalized FL |

### FL Frameworks

| Framework | Developer | Key Features |
|-----------|-----------|-------------|
| TensorFlow Federated (TFF) | Google | Research, simulation |
| PySyft | OpenMined | Privacy-preserving ML |
| FLOWER | Adap | Framework-agnostic, cross-platform |
| FLUTE | Microsoft | Large-scale simulation |
| FLSim | Meta | Simulation, scalability |
| FedML | FedML Inc. | MLOps for FL |
| NVIDIA FLARE | NVIDIA | Healthcare, production |
| PaddleFL | Baidu | MPC support |
| FATE | WeBank | Enterprise FL, VFL |
| FedLab | SMU | Research benchmark |

### Privacy Techniques Comparison

| Technique | Privacy Guarantee | Performance Overhead | Accuracy Impact |
|-----------|:-----------------:|:-------------------:|:---------------:|
| Differential Privacy | Mathematical (ε-DP) | Low | Moderate |
| Secure Aggregation | Information-theoretic | Moderate | None |
| Homomorphic Encryption | Cryptographic | Very High | None |
| SMPC | Cryptographic | High | None |
| Gradient Compression | Heuristic | Low | Low |
| Knowledge Distillation | Heuristic | Moderate | Moderate |

---
