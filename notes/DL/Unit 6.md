# AD32231: Deep Learning
## Unit VI: Reinforcement Learning
### Course Outcome 6 (CO6): Apply RL algorithms to solve decision-making problems, implement Q-learning and Deep Q-Networks.

---

## 6.1 Introduction to Deep Reinforcement Learning

### What is Reinforcement Learning (RL)?
Reinforcement Learning is a type of machine learning where an **agent** learns to make decisions by **interacting with an environment** to maximize cumulative **reward**.

Unlike:
- **Supervised Learning:** You have labeled examples (correct answers provided)
- **Unsupervised Learning:** Find patterns in unlabeled data

In RL:
- No labeled data provided
- Agent learns from **trial and error**
- Gets **rewards** for good actions and **penalties** for bad ones

**The Core Analogy:**
> Training a dog: 🐕
> - Dog (Agent) performs tricks (Actions)
> - If trick is done right, you give a treat (Positive Reward +)
> - If it does something wrong, you say "No!" (Negative Reward -)
> - Over time, the dog learns which actions lead to treats

### Real-World RL Applications:
- **Game Playing:** AlphaGo (beat world champion at Go), AlphaZero, OpenAI Five (Dota2)
- **Robotics:** Teaching robots to walk, grasp objects
- **Autonomous Driving:** Self-driving car decision-making
- **Recommendation Systems:** YouTube, Netflix recommendations
- **Finance:** Algorithmic trading
- **Healthcare:** Personalized treatment recommendations
- **NLP:** Fine-tuning LLMs with human feedback (RLHF — used in ChatGPT!)

---

## 6.2 Basic Framework of Reinforcement Learning

### Core Components:

```
         ACTION (a)
Agent ────────────────→ Environment
  ↑                           │
  │    STATE (s)               │
  │←──────────────────────────│
  │    REWARD (r)              │
  │←──────────────────────────│
```

#### 1. Agent
- The **learner** and decision-maker
- Example: The game-playing AI, the robot arm, the trading algorithm

#### 2. Environment
- The world the agent interacts with
- Example: The game board, the physical world, the stock market

#### 3. State (s)
- The current situation/observation of the environment
- Example: Position of pieces on the chess board, current stock prices, robot joint angles

#### 4. Action (a)
- What the agent can do
- Example: Move left/right in a game, buy/sell/hold a stock, rotate a joint

#### 5. Reward (r)
- A scalar signal indicating how good the last action was
- **Positive reward (+):** Good action (e.g., scoring a goal)
- **Negative reward (-):** Bad action (e.g., falling off a cliff)
- **Zero reward:** Neutral action

#### 6. Policy (π)
- The agent's **strategy** — maps states to actions
- `π(s) → a` (given state s, what action a should I take?)
- What we're ultimately trying to learn!

**Types of Policies:**
- **Deterministic:** Given state s, always take action a
- **Stochastic:** Given state s, take action a with probability π(a|s)

#### 7. Value Function (V)
- `V(s)` = Expected total future reward from state s, following policy π
- Helps the agent evaluate how "good" a state is for long-term reward

#### 8. Q-Function (Action-Value Function) — Q(s, a)
- `Q(s, a)` = Expected total future reward from taking action a in state s
- Unlike V(s), tells us which specific action is best in each state

---

### The RL Loop:
```
Time t=0: Agent observes state s0
Time t=1: Agent chooses action a0 based on policy π
          Environment returns: reward r1 and new state s1
Time t=2: Agent chooses action a1 based on s1
          Environment returns: r2 and s2
...
Goal: Maximize total cumulative reward R = r1 + r2 + r3 + ...
```

### Discounted Cumulative Reward:
Future rewards are worth less than immediate rewards (like money now vs later).
```
R = r1 + γ×r2 + γ²×r3 + γ³×r4 + ...
```
- **γ (gamma)** = discount factor, 0 ≤ γ < 1
- γ close to 0: Agent is short-sighted (only cares about immediate reward)
- γ close to 1: Agent is far-sighted (cares about long-term reward)

---

## 6.3 Markov Decision Process (MDP)

### What is an MDP?
A **Markov Decision Process** is the mathematical framework for modeling RL problems.

**Formally defined as a tuple: (S, A, P, R, γ)**
- **S:** Set of all possible states
- **A:** Set of all possible actions
- **P:** Transition probability P(s' | s, a) — probability of reaching state s' from state s by taking action a
- **R:** Reward function R(s, a, s') — reward received
- **γ:** Discount factor

### The Markov Property:
**"The future depends only on the present state, not the past history."**

```
P(s(t+1) | s(t), s(t-1), ..., s(0)) = P(s(t+1) | s(t))
```

**Analogy:**
> Chess: To determine the best next move, you only need to look at the **current board state** — not the entire history of how pieces moved to get there.

### MDP Example: Simple Grid World
```
Grid:
[ S ][ . ][ . ]
[ . ][ X ][ . ]    S=Start, G=Goal, X=Wall, H=Hole (penalty)
[ . ][ H ][ G ]

States: 9 grid positions
Actions: {Up, Down, Left, Right}
Rewards: Reach G = +10, Fall in H = -10, Each step = -0.1
Goal: Find the best path from S to G
```

### Solving MDPs:

#### Bellman Equation (for Value Function):
```
V(s) = max_a [ R(s,a) + γ × Σ P(s'|s,a) × V(s') ]
```
The value of a state = best action's immediate reward + discounted value of next states.

#### Bellman Equation (for Q-Function):
```
Q(s, a) = R(s, a) + γ × Σ P(s'|s,a) × max_a' Q(s', a')
```

---

## 6.4 Challenges of Reinforcement Learning

### 1. Exploration vs. Exploitation Dilemma
**Exploitation:** Use current knowledge to take the best-known action (short-term gain)
**Exploration:** Try new actions to discover potentially better options (long-term gain)

**Problem:** Too much exploitation → stuck in local optimum. Too much exploration → no learning.

**Analogy:**
> You have a favorite restaurant (exploit). Should you keep going there or try new restaurants (explore) that might be better?

**Solution — ε-Greedy Strategy:**
```
With probability ε (e.g., 0.1): Take a RANDOM action (explore)
With probability 1-ε (e.g., 0.9): Take the BEST known action (exploit)
```
Often, ε starts high and decreases over time (explore more initially, exploit more later).

### 2. Credit Assignment Problem
When a reward is received, which of the many past actions deserves the credit?

**Example:** A robot falls after 100 steps. Which step(s) caused it? Step 99? Step 50? All of them?

### 3. Sparse Rewards
Some tasks have very infrequent rewards, making learning slow.
**Example:** A robot playing chess might only receive a reward at the very end (win/loss), with nothing in between.

### 4. Sample Inefficiency
RL needs many interactions to learn → expensive in real world (robots, medical applications).

### 5. Non-Stationarity
The environment or optimal strategy might change over time.

### 6. Curse of Dimensionality
Large state/action spaces make it impossible to visit every state (need function approximation → DQN!)

---

## 6.5 Q-Learning

### What is Q-Learning?
**Q-Learning** is a **model-free** RL algorithm that learns the Q-function (action-value function) directly from experience.

"Model-free" means we don't need to know the transition probabilities P(s'|s,a) — we just learn from experience!

### The Q-Table:
For simple problems, we store Q-values in a **table**:
- Rows = states
- Columns = actions
- Each cell = Q(s, a)

**Example Q-table (simplified Tic-Tac-Toe):**
```
State       | Left | Right | Up  | Down
------------|------|-------|-----|------
State 1     | 0.5  | 0.3   | 0.8 | 0.1
State 2     | 0.2  | 0.9   | 0.1 | 0.4
...
```

### Q-Learning Update Rule:
```
Q(s, a) ← Q(s, a) + α × [r + γ × max Q(s', a') - Q(s, a)]
```

Let's break this down:
- `Q(s, a)` = Current Q-value estimate
- `r` = Reward received
- `γ × max Q(s', a')` = Discounted best future Q-value
- `r + γ × max Q(s', a')` = Target Q-value (what we want Q to be)
- `r + γ × max Q(s', a') - Q(s, a)` = TD Error (Temporal Difference Error)
- `α` = Learning rate (how fast we update)

**Analogy:**
> Like updating your review of a restaurant:
> Current opinion (Q): "It's a 6/10"
> After visiting: The food was great (r=+2), and you expect future visits to be good too (γ × max Q = +2)
> New target: 6/10 → closer to 8/10
> Updated opinion: "It's a 7/10" (moved partially toward target based on α)

### Q-Learning Algorithm:
```python
Initialize Q-table with zeros (or small random values)
For each episode:
    Reset environment, get initial state s
    While not done:
        Choose action a (ε-greedy)
        Take action a, observe reward r and new state s'
        Update Q-table:
            Q(s,a) ← Q(s,a) + α × [r + γ × max_a'(Q(s',a')) - Q(s,a)]
        s ← s'
```

### Convergence:
Q-Learning is proven to converge to the optimal Q-function **if:**
1. All state-action pairs are visited infinitely often (enough exploration)
2. Learning rate satisfies certain conditions (decreasing over time)

---

## 6.6 Deep Q-Networks (DQN)

### The Problem with Q-Tables:
Q-tables work for small state spaces, but:
- **Atari game:** Screen is 84×84 pixels × 4 frames = **28,224 dimensions**
- **Possible states:** Astronomically large → Q-table is impossible!

**Solution: Replace the Q-table with a Deep Neural Network**

### What is DQN?
**DQN (Deep Q-Network)** was introduced by **DeepMind (2015)** and achieved superhuman performance on 49 Atari games using just raw pixel inputs!

Instead of a table, we use a neural network to **approximate** Q(s, a):
```
State s (pixels) → [CNN + FC] → Q-values for each action
```

**Input:** Game screen (image)
**Output:** Q-value for each possible action (e.g., Q(s, Left), Q(s, Right), Q(s, Jump))

**Architecture (Atari DQN):**
```
84×84×4 frames → CONV → CONV → CONV → FC → Q-values for each action
```

### Key Innovations in DQN:

#### 1. Experience Replay
**Problem:** In standard RL, experiences are correlated (consecutive states are similar). Training on correlated data makes the network unstable.

**Solution:** Store experiences `(s, a, r, s')` in a **Replay Buffer** (memory bank). During training, sample **random mini-batches** from this buffer.

**Benefits:**
- Breaks correlation between consecutive experiences
- Each experience can be used for multiple updates (data efficiency)
- More stable training

```
Replay Buffer: [(s1,a1,r1,s1'), (s2,a2,r2,s2'), ..., (s10000, a10000, r10000, s10000')]
Mini-batch: Randomly sample 32 experiences from buffer
Train on these 32 random experiences
```

#### 2. Target Network
**Problem:** In standard DQN, the target `r + γ × max Q(s', a')` keeps changing (because we're updating the same network used to compute targets). This causes instability.

**Solution:** Use TWO networks:
- **Online Network:** Updated every step
- **Target Network:** A copy of the online network, updated **less frequently** (every N steps)

```
Loss = [r + γ × max Q_target(s', a') - Q_online(s, a)]²
```
The target is computed using the slow-updating **target network** → more stable targets.

### DQN Training Loop:
```python
Initialize online_network and target_network (same weights)
Initialize replay_buffer

For each episode:
    State s ← environment.reset()
    While not done:
        Action a ← ε-greedy(online_network(s))
        s', r, done ← environment.step(a)
        Store (s, a, r, s', done) in replay_buffer
        
        If replay_buffer is large enough:
            Sample mini-batch from replay_buffer
            Compute targets: y = r + γ × max(target_network(s'))
            Train online_network to minimize (y - online_network(s, a))²
        
        Every C steps: target_network ← online_network weights
        
        s ← s'
```

### DQN Improvements:

| Improvement | What it fixes |
|---|---|
| **Double DQN** | Reduces overestimation of Q-values |
| **Dueling DQN** | Separates state value and action advantage |
| **Prioritized Experience Replay** | Sample important experiences more often |
| **Rainbow DQN** | Combines all improvements |

---

## 6.7 Case Study: Simple Reinforcement Learning for Tic-Tac-Toe

### Game Overview:
- **Board:** 3×3 grid
- **Players:** X and O (agent vs. human or another agent)
- **Goal:** Get 3 in a row (horizontally, vertically, or diagonally)
- **Reward:** Win=+1, Lose=-1, Draw=0, Each move=0

### Defining the RL Components:

#### State Space:
- Each cell can be: empty (0), X (1), or O (-1)
- Total states: 3^9 = 19,683 (but only ~5,478 valid board states)
- Small enough for a Q-table!

#### Action Space:
- 9 possible moves (one per cell)
- Invalid moves (occupied cells) must be masked

#### Reward Structure:
```
Win:  +1.0
Loss: -1.0
Draw:  0.5 (or 0)
Invalid move: -0.5 (or just skip invalid moves)
Each step: 0 (sparse reward)
```

#### Policy:
- Start with ε=1.0 (fully random, pure exploration)
- Gradually decrease ε to 0.1 (mostly exploit learned Q-values)

### Q-Table Approach for Tic-Tac-Toe:

```python
# State representation: tuple of 9 values (0, 1, -1)
# Action: index 0-8 (which cell to play)

Q_table = {}  # dictionary: state → Q-values for each action

def get_Q_values(state):
    if state not in Q_table:
        Q_table[state] = np.zeros(9)  # Initialize to 0
    return Q_table[state]

def choose_action(state, epsilon=0.1):
    board = np.array(state)
    valid_moves = np.where(board == 0)[0]  # Empty cells only
    
    if random.random() < epsilon:
        return random.choice(valid_moves)  # Explore: random valid move
    else:
        Q_values = get_Q_values(state)
        # Only consider valid moves
        valid_Q = [(Q_values[a], a) for a in valid_moves]
        return max(valid_Q)[1]  # Exploit: best valid move

def update_Q(state, action, reward, next_state, done, alpha=0.5, gamma=0.9):
    current_Q = get_Q_values(state)[action]
    if done:
        target = reward
    else:
        next_Q = get_Q_values(next_state)
        target = reward + gamma * np.max(next_Q)
    
    get_Q_values(state)[action] += alpha * (target - current_Q)
```

### Training Process:
```
Train agent by playing against itself (self-play) or a random opponent:

Episode 1: Agent makes mostly random moves → loses/draws
Episode 100: Agent starts learning basic patterns → wins more
Episode 1000: Agent learns blocking, winning strategies
Episode 10000: Agent plays near-optimally!
```

### Key Observations During Training:
1. Initially: Agent places marks randomly → frequent losses
2. After some training: Agent learns to take winning moves when available
3. More training: Agent learns to block opponent's winning moves
4. Advanced: Agent learns opening strategies and fork creation

### Game Flow Example:
```
Board State (agent=X, opponent=O):
[ X ][ O ][ . ]
[ . ][ X ][ . ]
[ . ][ . ][ . ]

Agent's Q-values for empty cells:
Position 2 (top-right):  0.2
Position 3 (mid-left):   0.1
Position 5 (mid-right):  0.3
Position 6 (bot-left):   0.8  ← highest! (blocking O + setting up diagonal win)
Position 7 (bot-center): 0.4
Position 8 (bot-right):  0.9  ← highest! (creates two ways to win!)

Agent plays position 8 (bottom-right) → diagonal X-X-X → WIN!
Reward: +1.0 → Q-values updated
```

### Results After Training:
| Training Games | Win Rate vs Random Opponent |
|---|---|
| 100 | ~35% |
| 1,000 | ~65% |
| 10,000 | ~85% |
| 100,000 | ~95%+ |

---

## Unit VI Summary

| Topic | Key Takeaway |
|---|---|
| RL Framework | Agent takes actions in environment, gets rewards, learns optimal policy |
| MDP | Mathematical framework: (S, A, P, R, γ); Markov property: future depends only on present |
| Policy (π) | Strategy mapping states to actions; what we want to learn |
| Q-function | Q(s,a) = expected future reward of action a in state s |
| Exploration vs Exploitation | ε-greedy: explore randomly with probability ε, else exploit best action |
| Challenges | Credit assignment, sparse rewards, sample inefficiency, huge state spaces |
| Q-Learning | Update Q-values using Bellman equation; learn from experience |
| DQN | Neural network replaces Q-table for large state spaces (images, etc.) |
| Experience Replay | Random sampling from buffer breaks correlations, stabilizes training |
| Target Network | Separate slow-updating network for stable training targets |
| Tic-Tac-Toe | Q-table RL; state=board, action=cell, reward=win/lose/draw; self-play training |

---

## Full Course Quick Reference

| Unit | Core Theme | Key Algorithms/Models |
|---|---|---|
| I | Neural Network Basics | Perceptron, MLP, Backpropagation, Activation Functions |
| II | Training & Optimization | Gradient Descent, Adam, Dropout, Batch Normalization |
| III | Image Processing | CNN, AlexNet, VGG, ResNet, YOLO, Transfer Learning |
| IV | Sequential Data | RNN, LSTM, GRU, Bidirectional RNN, Seq2Seq |
| V | Generation & Explanation | VAE, GAN, BERT, Transformer, SHAP, LIME |
| VI | Decision Making | MDP, Q-Learning, DQN, Tic-Tac-Toe RL |

---
*End of Unit VI — End of AD32231: Deep Learning Notes*
