# BLOCKCHAIN TECHNOLOGY - COMPLETE PREPARATION NOTES

---

# UNIT I: INTRODUCTION TO BLOCKCHAIN

## 1. Types of Networks

### Central Network
- **What it is:** One main computer (server) controls everything
- **How it works:** All other computers connect to this one central computer
- **Example:** A traditional bank where the bank's main server holds all your account data
- **Problem:** If the central server fails, everything stops. If it gets hacked, all data is stolen.

### Distributed Network
- **What it is:** Data is spread across multiple computers, but one organization still controls them
- **How it works:** Multiple servers share the workload, but they all belong to one company
- **Example:** A company with servers in Mumbai, Delhi, and Bangalore - all controlled by the same company
- **Better than central:** If one server fails, others can take over

### Decentralized Network
- **What it is:** No single point of control - everyone is equal
- **How it works:** All computers in the network have equal power and no one controls the others
- **Example:** Blockchain network - no bank, no government controls it
- **Best for trust:** No single entity can manipulate the system

---

## 2. Introduction to Blockchain

### What is a Block?
Think of a block as a **page in a digital notebook** that stores information:
- List of transactions (who sent money to whom)
- Timestamp (when the block was created)
- A unique code called "hash" (like a fingerprint)
- The hash of the previous block (this connects blocks together)

### What is Chaining?
- Each block contains the hash (fingerprint) of the previous block
- This creates a chain: Block 1 → Block 2 → Block 3 → ...
- If someone tries to change data in Block 2, its hash changes, breaking the chain
- This makes blockchain **tamper-proof**

**Simple Example:**
```
Block 1: Hash = ABC123
Block 2: Contains "ABC123" + New Data → Hash = DEF456
Block 3: Contains "DEF456" + New Data → Hash = GHI789
```
If someone changes Block 1, its hash changes from ABC123 to XYZ999. Now Block 2 doesn't match anymore, and the whole chain breaks!

### Characteristics of Blockchain
1. **Decentralized:** No single authority controls it
2. **Transparent:** Everyone can see all transactions
3. **Immutable:** Once data is added, it cannot be changed
4. **Secure:** Uses cryptography to protect data
5. **Distributed:** Copies exist on many computers worldwide

### Opportunities (Where Blockchain Can Be Used)
- Banking and finance (fast, cheap money transfers)
- Supply chain (tracking products from factory to store)
- Healthcare (secure patient records)
- Voting (tamper-proof elections)
- Real estate (property records)
- Education (verified certificates)

---

## 3. History and Evolution of Blockchain

### Blockchain 1.0 - Digital Currency (2008-2013)
- **What:** Bitcoin - the first cryptocurrency
- **Created by:** Satoshi Nakamoto (anonymous person/group)
- **Purpose:** Digital money without banks
- **Features:** Only money transfers, no other programs
- **Example:** Sending Bitcoin to a friend

### Blockchain 2.0 - Smart Contracts (2014-2017)
- **What:** Ethereum - blockchain that can run programs
- **Created by:** Vitalik Buterin
- **Purpose:** Beyond money - programmable blockchain
- **Features:** Smart contracts (self-executing agreements)
- **Example:** Automatic insurance payout when flight is delayed

### Blockchain 3.0 - Real World Applications (2018-Present)
- **What:** Blockchain for everyday use cases
- **Purpose:** Solve real problems in various industries
- **Features:** Faster, cheaper, more scalable
- **Examples:** Supply chain tracking, healthcare records, government services, IoT

---

## 4. Types of Blockchain

### Public Blockchain
- **Who can join:** Anyone
- **Who can read:** Everyone
- **Who can write:** Anyone (following rules)
- **Control:** Fully decentralized
- **Speed:** Slow (many computers must agree)
- **Example:** Bitcoin, Ethereum
- **Like:** A public park - anyone can enter

### Private Blockchain
- **Who can join:** Only invited members
- **Who can read:** Only authorized people
- **Who can write:** Only authorized people
- **Control:** One organization controls
- **Speed:** Fast (fewer computers)
- **Example:** Internal company records
- **Like:** A private club - only members allowed

### Consortium Blockchain
- **Who can join:** Selected organizations
- **Who can read:** Members or public (depends)
- **Who can write:** Only member organizations
- **Control:** Shared by a group of organizations
- **Speed:** Medium
- **Example:** Banking consortium where 5 banks share data
- **Like:** A gated community - only selected families

### Hybrid Blockchain
- **What:** Mix of public and private
- **How:** Some data is public, some is private
- **Example:** A company publishes transaction proofs publicly but keeps details private
- **Like:** A house with open garden (public) but locked rooms (private)

---

## 5. Ledger and Peer-to-Peer Network

### Distributed Ledger
- **Simple definition:** A shared database that everyone in the network has a copy of
- **Traditional ledger:** Bank keeps one record of all transactions
- **Distributed ledger:** Everyone in the network keeps the same record
- **Benefit:** No single point of failure, very hard to cheat

### Peer-to-Peer (P2P) Network
- **What:** Computers connect directly to each other without a central server
- **How:** Each computer (peer) can both send and receive data
- **Example:** Bitcoin network - your computer connects to other users' computers directly
- **Benefit:** No middleman needed

---

## 6. Types of Blockchain Nodes

A **node** is simply a computer connected to the blockchain network.

### Full Node
- **What:** Stores complete copy of the blockchain
- **Does:** Validates all transactions and blocks
- **Needs:** Lots of storage space
- **Example:** A computer storing entire Bitcoin history (400+ GB)

### Miner Node
- **What:** Special node that creates new blocks
- **Does:** Solves complex math puzzles to add blocks (mining)
- **Gets:** Rewarded with cryptocurrency
- **Example:** Bitcoin miners using powerful computers

### Archive Node
- **What:** Stores EVERYTHING including historical states
- **Does:** Keeps complete history of all account balances at every point in time
- **Needs:** Massive storage
- **Used by:** Exchanges, analytics companies

### Validator Node
- **What:** Checks if transactions are valid
- **Does:** Votes on whether to accept new blocks
- **Found in:** Proof of Stake systems
- **Example:** Ethereum 2.0 validators

### Pruned Node
- **What:** Stores only recent blockchain data
- **Does:** Deletes old data to save space but keeps validation ability
- **Needs:** Less storage than full node
- **Good for:** People with limited hard drive space

### Authority Node
- **What:** Special node with power to create blocks
- **Found in:** Permissioned blockchains
- **Controlled by:** Trusted organizations
- **Example:** Government node in a public service blockchain

### Light Node (SPV Node)
- **What:** Stores only block headers (summaries), not full blocks
- **Does:** Relies on full nodes for detailed data
- **Needs:** Very little storage
- **Used by:** Mobile wallets, lightweight apps

### Super Node
- **What:** High-performance node with extra capabilities
- **Does:** Handles more traffic, stores more data, connects networks
- **Found in:** Some specific blockchain architectures

---

## CASE STUDY: Blockchain in Supply Chain - IBM and Maersk (TradeLens)

### The Problem
- Shipping involves many parties: factories, ports, customs, trucking companies
- Each has their own paperwork and systems
- Documents get lost, delayed, or faked
- Tracking a container is difficult

### The Solution: TradeLens
- **Built by:** IBM and Maersk (shipping company)
- **What:** Blockchain platform for global shipping
- **How it works:**
  - All parties share the same data on blockchain
  - Every event (loading, unloading, customs) is recorded
  - Documents are digital and tamper-proof
  - Real-time tracking of containers

### Benefits
- Reduced paperwork by 50%
- Faster customs clearance
- Better tracking of goods
- Less fraud
- Cost savings for all parties

### Why Blockchain?
- All parties trust the data (cannot be changed)
- No single company controls everything
- Transparent but secure

---

# UNIT II: CRYPTOGRAPHIC FOUNDATIONS AND CONSENSUS MECHANISMS

## 1. Cryptography Basics

### What is Cryptography?
- The science of keeping information secret and secure
- Converts readable data (plaintext) into scrambled data (ciphertext)
- Only authorized people can read it

### Encryption and Decryption
- **Encryption:** Converting normal text into secret code
  - Example: "HELLO" → "XKQQR" (using a simple code)
- **Decryption:** Converting secret code back to normal text
  - Example: "XKQQR" → "HELLO"
- **Key:** The secret password/code used to encrypt and decrypt

---

## 2. Symmetric vs Asymmetric Cryptography

### Symmetric Cryptography
- **What:** Same key is used for encryption AND decryption
- **How it works:**
  - Alice encrypts message with Key A
  - Bob decrypts message with same Key A
- **Example:** Like a door lock - same key locks and unlocks
- **Fast:** Yes, very fast
- **Problem:** How to share the key safely?
- **Used for:** Encrypting large amounts of data

### Asymmetric Cryptography (Public Key Cryptography)
- **What:** Two different but related keys
  - **Public Key:** Shared with everyone (like your email address)
  - **Private Key:** Kept secret (like your email password)
- **How it works:**
  - If you encrypt with Public Key → Only Private Key can decrypt
  - If you encrypt with Private Key → Anyone with Public Key can verify
- **Example:** Like a mailbox - anyone can drop mail in (public), only you have key to take mail out (private)
- **Slower:** But more secure for key exchange
- **Used for:** Digital signatures, secure communication

---

## 3. Public Key and Private Key

### Public Key
- Can be shared with anyone
- Used to receive funds (like account number)
- Used to verify signatures
- Derived from private key (one-way process)

### Private Key
- MUST be kept secret
- Used to sign transactions (prove you own something)
- Used to decrypt messages meant for you
- If lost → You lose access to your funds forever!
- If stolen → Thief can steal your funds

### Simple Example:
```
Your Private Key: A1B2C3D4 (KEEP SECRET!)
       ↓ (mathematical calculation)
Your Public Key: XYZ789 (Share with everyone)
       ↓
Your Address: 0x1234...abcd (Like bank account number)
```

---

## 4. Digital Signature

### What is it?
- A mathematical way to prove a message came from you and wasn't changed
- Like a handwritten signature but much more secure

### How it works:
1. You create a message (e.g., "Send 5 BTC to Bob")
2. You sign it with your PRIVATE key
3. Anyone can verify the signature using your PUBLIC key
4. If verification passes → message is really from you and unchanged

### Properties:
- **Authenticity:** Proves who sent the message
- **Integrity:** Proves message wasn't changed
- **Non-repudiation:** Sender cannot deny sending it

### Example:
```
Message: "Pay Alice 10 coins"
Your Private Key signs it → Creates Signature
Alice receives: Message + Signature
Alice uses Your Public Key to verify → Valid!
```

---

## 5. Hashing Functions

### What is Hashing?
- Takes any input (text, file, etc.) and produces a fixed-size output called "hash"
- Like a fingerprint for data

### Properties of Good Hash Function:
1. **Deterministic:** Same input always gives same hash
2. **Fast:** Easy to calculate
3. **One-way:** Cannot reverse (cannot find input from hash)
4. **Small change, big difference:** Changing one letter changes entire hash
5. **No collisions:** Two different inputs never give same hash

### Common Hash Functions:
- **SHA-256:** Used by Bitcoin (produces 256-bit hash)
- **Keccak-256:** Used by Ethereum

### Example:
```
Input: "Hello"
SHA-256 Hash: 185f8db32271fe25f561a6fc938b2e264306ec304eda518007d1764826381969

Input: "hello" (lowercase h)
SHA-256 Hash: 2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824
```
See how one letter change = completely different hash!

---

## 6. Merkle Tree

### What is it?
- A tree structure used to efficiently verify large amounts of data
- Named after Ralph Merkle

### How it works:
1. Take all transactions in a block
2. Hash each transaction
3. Pair up hashes and hash them together
4. Keep pairing until you get ONE hash (Merkle Root)

### Simple Example:
```
Transaction A → Hash A    Transaction B → Hash B
                    ↘         ↙
                  Hash AB
                    ↗         ↘
Transaction C → Hash C    Transaction D → Hash D
                    ↘         ↙
                  Hash CD
                    ↘         ↙
                  MERKLE ROOT
```

### Why useful?
- To verify one transaction, you don't need all data
- Only need a few hashes (called Merkle proof)
- Saves storage and bandwidth

### Used in:
- Bitcoin blocks
- Ethereum blocks
- Git version control

---

## 7. Blockchain Consensus Mechanisms

### What is Consensus?
- Agreement among all computers in the network about which transactions are valid
- Like a group deciding where to eat - everyone must agree

### Why needed?
- No central authority
- Some nodes might be dishonest
- Network must agree on the "truth"

---

### Proof of Work (PoW)
- **Used by:** Bitcoin, Litecoin
- **How it works:**
  - Miners compete to solve a difficult math puzzle
  - First to solve gets to add the next block
  - Winner gets rewarded with cryptocurrency
- **Puzzle:** Find a number that makes the block's hash start with certain zeros
- **Energy intensive:** Requires lots of electricity
- **Secure:** Very hard to attack (need 51% of computing power)

**Simple Example:**
```
Puzzle: Find a number that when added to "Blockchain" and hashed starts with "0000"
Try: Blockchain + 1 → Hash = abc... (no)
Try: Blockchain + 2 → Hash = def... (no)
Try: Blockchain + 15682 → Hash = 0000xyz... (YES!)
```

---

### Proof of Stake (PoS)
- **Used by:** Ethereum 2.0, Cardano
- **How it works:**
  - Validators lock up (stake) their coins
  - System randomly picks validator to create next block
  - More coins staked = higher chance of being picked
  - Bad behavior = lose staked coins (slashing)
- **Energy efficient:** No mining puzzles
- **Faster:** Blocks created quicker

**Simple Example:**
```
Alice stakes 100 coins
Bob stakes 50 coins
Charlie stakes 150 coins
Total: 300 coins

Alice's chance: 100/300 = 33%
Bob's chance: 50/300 = 17%
Charlie's chance: 150/300 = 50%
```

---

### Proof of Capacity (PoC)
- **Used by:** Burstcoin, Signum
- **How it works:**
  - Miners use hard drive space instead of computing power
  - Pre-compute and store possible solutions
  - More storage = better chances
- **Energy efficient:** Hard drives use less power than miners

---

### Proof of Authority (PoA)
- **Used by:** Private blockchains, testnets
- **How it works:**
  - Pre-approved validators create blocks
  - Validators are known, trusted entities
  - Reputation is at stake
- **Fast:** Few validators, quick agreement
- **Not decentralized:** Only trusted parties

**Example:** 5 banks run a blockchain, each bank is a validator

---

## 8. Byzantine Generals Problem

### The Problem
- Several generals surround a city
- They must attack together to win
- They communicate via messengers
- Some generals might be traitors
- How to reach agreement when some might lie?

### Byzantine Fault Tolerance (BFT)
- System can work correctly even if some nodes fail or act dishonest
- Needs 2/3 or more nodes to be honest
- **Formula:** System works if honest nodes > 2 × faulty nodes

### Variants:
1. **Practical BFT (PBFT):** Used in permissioned blockchains
2. **Delegated BFT (dBFT):** Used by NEO
3. **Federated BFT:** Used by Stellar

---

## 9. Security on Blockchain

### Why Blockchain is Secure:
1. **Cryptography:** Digital signatures protect transactions
2. **Hashing:** Makes data tamper-evident
3. **Decentralization:** No single point of failure
4. **Consensus:** Network agrees on valid transactions
5. **Immutability:** Cannot change past records

---

## 10. Data Storage on Blockchain

### On-Chain Storage
- Data stored directly on blockchain
- Permanent and immutable
- Expensive (costs gas/fees)
- Example: Smart contract code, transaction records

### Off-Chain Storage
- Data stored outside blockchain
- Only hash/reference stored on-chain
- Cheaper and faster
- Example: Large files, images, documents

---

## 11. Transaction Life Cycle

### Steps in a Blockchain Transaction:
1. **Creation:** User creates transaction (send X coins to Y address)
2. **Signing:** User signs with private key
3. **Broadcasting:** Transaction sent to network
4. **Verification:** Nodes check if transaction is valid
5. **Pooling:** Valid transactions wait in "mempool"
6. **Block Creation:** Miner/validator picks transactions and creates block
7. **Consensus:** Network agrees on the block
8. **Confirmation:** Block added to chain
9. **Finalization:** After more blocks, transaction is irreversible

---

## CASE STUDY: Bitcoin's Use of Proof-of-Work and SHA-256

### How Bitcoin Uses These:
- **SHA-256:** Hashes all transactions and blocks
- **PoW:** Miners compete to find valid block hashes

### Mining Process:
1. Collect pending transactions
2. Create Merkle tree → get Merkle root
3. Add block header (previous hash, timestamp, nonce)
4. Hash everything with SHA-256
5. If hash doesn't start with enough zeros → change nonce and try again
6. Repeat until valid hash found
7. Broadcast block to network

### Difficulty Adjustment:
- Every 2016 blocks (~2 weeks), difficulty adjusts
- If blocks too fast → difficulty increases
- If blocks too slow → difficulty decreases
- Goal: One block every 10 minutes

---

# UNIT III: ETHEREUM BLOCKCHAIN

## 1. What is Ethereum?
- A blockchain platform that can run programs (smart contracts)
- Created by Vitalik Buterin in 2015
- Second largest cryptocurrency after Bitcoin
- Has its own cryptocurrency called Ether (ETH)

### Key Difference from Bitcoin:
- **Bitcoin:** Digital money only
- **Ethereum:** Programmable blockchain - can build apps on it

---

## 2. Ethereum Ecosystem

### Components:

#### Address
- Like a bank account number
- 42 characters starting with "0x"
- Example: `0x742d35Cc6634C0532925a3b844Bc9e7595f2bD18`
- Derived from public key

#### Accounts
Two types:
1. **Externally Owned Accounts (EOAs):**
   - Controlled by private key (real people)
   - Can send transactions
   - Have ETH balance
   - Example: Your personal wallet

2. **Contract Accounts:**
   - Controlled by code (smart contracts)
   - Cannot initiate transactions
   - Have ETH balance and code
   - Activated when someone sends transaction to it
   - Example: A voting contract, a token contract

#### Transaction
- Action that changes blockchain state
- Types:
  - Transfer ETH between accounts
  - Deploy a smart contract
  - Call a smart contract function
- Contains: From, To, Value, Gas, Data, Nonce, Signature

#### Messages
- Internal calls between smart contracts
- Not stored on blockchain directly
- Happen during transaction execution

#### Ether (ETH)
- Ethereum's native cryptocurrency
- Used to pay for transactions (gas fees)
- Smallest unit: Wei (1 ETH = 10¹⁸ Wei)
- Sub-units:
  - Wei = 1
  - Gwei = 1,000,000,000 Wei (commonly used for gas prices)
  - ETH = 1,000,000,000,000,000,000 Wei

---

## 3. Tool Stack

### Development Tools:
1. **Remix IDE:** Web-based smart contract editor
2. **MetaMask:** Browser wallet
3. **Truffle:** Development framework
4. **Ganache:** Personal blockchain for testing
5. **Hardhat:** Development environment
6. **Web3.js / Ethers.js:** JavaScript libraries to interact with Ethereum

---

## 4. Ethereum Virtual Machine (EVM)

### What is EVM?
- A virtual computer that runs smart contracts
- Every Ethereum node runs EVM
- Ensures all nodes get same result
- Isolated from main computer (sandboxed)

### How it works:
```
Smart Contract Code (Solidity)
         ↓
    Compiled to Bytecode
         ↓
    EVM executes bytecode
         ↓
    State changes on blockchain
```

### Gas
- Unit measuring computational work
- Every operation costs gas
- Prevents infinite loops and spam
- Users pay gas fees in ETH
- Gas Limit: Maximum gas user willing to pay
- Gas Price: Amount of ETH per unit of gas

---

## 5. Difference Between Bitcoin and Ethereum

| Feature | Bitcoin | Ethereum |
|---------|---------|----------|
| Purpose | Digital currency | Programmable platform |
| Creator | Satoshi Nakamoto | Vitalik Buterin |
| Year | 2009 | 2015 |
| Block Time | 10 minutes | 12 seconds |
| Consensus | PoW | PoS (was PoW) |
| Language | Script (limited) | Solidity (full programming) |
| Supply | 21 million | Unlimited (with burning) |
| Smart Contracts | No | Yes |
| Use Cases | Store of value, payments | DeFi, NFTs, dApps |

---

## 6. Ether: ETH and ETC

### ETH (Ethereum)
- Current Ethereum blockchain
- After the DAO hack, community decided to reverse transactions
- Most users moved to this chain
- Supported by Ethereum Foundation

### ETC (Ethereum Classic)
- Original Ethereum blockchain
- Some users believed "code is law" - no reversing transactions
- Kept the original chain
- Smaller community

---

## 7. Ethereum Wallets

### Types:
1. **Hot Wallets:** Connected to internet
   - MetaMask (browser extension)
   - Mobile wallets
   - Web wallets

2. **Cold Wallets:** Offline storage
   - Hardware wallets (Ledger, Trezor)
   - Paper wallets

### What wallets store:
- NOT coins (coins are on blockchain)
- Store your PRIVATE KEY
- Allow you to sign transactions

---

## 8. Ethereum Transaction Life Cycle

1. User creates transaction in wallet
2. Wallet signs transaction with private key
3. Transaction broadcast to network
4. Nodes validate transaction (signature, nonce, balance)
5. Valid transactions enter mempool
6. Validator picks transactions and creates block
7. Block proposed to network
8. Network validates block
9. Block added to chain
10. Transaction confirmed (more blocks = more secure)

---

## 9. Key Terms in Ethereum Transaction

### Nonce
- Number of transactions sent from your account
- Starts at 0, increases by 1 each time
- Prevents replay attacks
- Example: Your 5th transaction has nonce = 4

### Signature
- Mathematical proof that you authorized the transaction
- Created using your private key
- Can be verified by anyone with your public key

### To
- Recipient address
- Can be another account or contract address

### Value
- Amount of ETH being sent
- Measured in Wei

### Gas Price
- Amount of ETH you pay per unit of gas
- Higher gas price = faster processing
- Measured in Gwei

### Gas Limit
- Maximum gas you're willing to pay
- Prevents spending too much
- Unused gas is refunded

### Init
- Used when deploying a new contract
- Contains the contract's creation code

### Data
- Additional information for contract calls
- Contains function name and parameters

---

## 10. Smart Contracts

### What is a Smart Contract?
- Self-executing program on the blockchain
- "If this, then that" logic
- No middleman needed
- Cannot be changed once deployed

### Simple Example:
```
IF player A wins the bet
THEN send 10 ETH to player A
ELSE send 10 ETH to player B
```

### Properties:
- Automatic execution
- Trustless (don't need to trust the other party)
- Transparent (code is public)
- Immutable (cannot be changed)
- Cost-effective (no intermediaries)

---

## 11. Etherscan

### What is it?
- Block explorer for Ethereum
- Website to view blockchain data

### You can see:
- Account balances
- Transaction history
- Smart contract code
- Token transfers
- Gas prices
- Network statistics

### Website: https://etherscan.io

---

## CASE STUDY: Decentralized Finance (DeFi) on Ethereum - Uniswap

### What is DeFi?
- Financial services without banks
- Built on blockchain using smart contracts
- Lending, borrowing, trading, earning interest

### What is Uniswap?
- Decentralized exchange (DEX)
- Trade tokens without a middleman
- Uses Automated Market Maker (AMM) model

### How Uniswap Works:
1. **Liquidity Pools:** Users deposit pairs of tokens
2. **Automated Pricing:** Price determined by ratio of tokens in pool
3. **Trading:** Users trade against the pool, not other users
4. **Fees:** Traders pay 0.3% fee, distributed to liquidity providers

### Benefits:
- No account needed
- No KYC (identity verification)
- 24/7 trading
- Anyone can provide liquidity and earn fees
- Transparent and open-source

### Risks:
- Smart contract bugs
- Impermanent loss for liquidity providers
- High gas fees during busy times

---

# UNIT IV: SOLIDITY PROGRAMMING AND SMART CONTRACTS

## 1. Introduction to Solidity

### What is Solidity?
- Programming language for writing smart contracts
- Designed for Ethereum Virtual Machine (EVM)
- Similar to JavaScript in syntax
- Created by Gavin Wood

### Basic Structure:
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract MyContract {
    // Your code here
}
```

### Explanation:
- `SPDX-License-Identifier`: License for the code
- `pragma solidity`: Specifies compiler version
- `contract`: Keyword to define a smart contract

---

## 2. Basic Syntax

### Comments:
```solidity
// Single line comment

/* 
   Multi-line 
   comment 
*/
```

### State Variables:
- Variables stored permanently on blockchain
- Declared inside contract
- Expensive to store!

```solidity
contract Example {
    uint public myNumber = 10;
    string public myName = "Hello";
    bool public isActive = true;
}
```

---

## 3. Data Types and Variables

### Value Types (stored directly):

#### uint (Unsigned Integer)
- Whole numbers, no decimals, no negatives
- Variants: uint8, uint16, uint32, uint256
- Default: uint256

```solidity
uint age = 25;
uint8 smallNumber = 100;
uint256 bigNumber = 999999999;
```

#### int (Signed Integer)
- Can be negative
- Variants: int8, int16, int256

```solidity
int temperature = -10;
int balance = -500;
```

#### bool
- True or false

```solidity
bool isComplete = true;
bool hasAccess = false;
```

#### address
- Ethereum address (20 bytes)

```solidity
address public owner = 0x742d35Cc6634C0532925a3b844Bc9e7595f2bD18;
```

#### address payable
- Address that can receive ETH

```solidity
address payable public receiver = payable(0x742d35...);
```

#### bytes and string
```solidity
string public greeting = "Hello World";
bytes32 public data = "Fixed size";
```

### Reference Types:

#### Arrays
```solidity
uint[] public numbers;  // Dynamic array
uint[5] public fixedNumbers;  // Fixed array
string[] public names;
```

#### Structs (Custom data types)
```solidity
struct Student {
    string name;
    uint age;
    address studentId;
}

Student public student1;
```

#### Mappings (Key-value pairs)
```solidity
mapping(address => uint) public balances;
mapping(string => uint) public prices;
mapping(address => Student) public students;
```

---

## 4. Variables Scope

### State Variables
- Declared inside contract, outside functions
- Stored on blockchain permanently
- Most expensive

### Local Variables
- Declared inside functions
- Exist only during function execution
- Not stored on blockchain
- Cheap

### Global Variables
- Provided by Ethereum
- Always available

```solidity
// Common global variables:
msg.sender      // Address that called the function
msg.value       // Amount of ETH sent with the call
block.timestamp // Current block timestamp
block.number    // Current block number
```

---

## 5. Functions

### Basic Syntax:
```solidity
function functionName(parameters) visibility stateMutability returns(returnType) {
    // Code here
}
```

### Visibility:
- `public`: Anyone can call (inside and outside)
- `private`: Only inside this contract
- `internal`: Inside this contract and child contracts
- `external`: Only from outside

### State Mutability:
- `pure`: Doesn't read or write state
- `view`: Reads state but doesn't write
- `payable`: Can receive ETH
- (none): Can read and write state

### Examples:

```solidity
// Read-only function
function getBalance() public view returns(uint) {
    return balance;
}

// Function that changes state
function setBalance(uint newBalance) public {
    balance = newBalance;
}

// Function that receives ETH
function deposit() public payable {
    // msg.value contains the ETH sent
}

// Pure function (no state access)
function add(uint a, uint b) public pure returns(uint) {
    return a + b;
}
```

---

## 6. Modifiers

### What are Modifiers?
- Code that runs before a function
- Used for conditions and checks
- Like a security guard

### Example:
```solidity
address public owner;

modifier onlyOwner() {
    require(msg.sender == owner, "Not the owner!");
    _;  // Function code runs here
}

function deleteContract() public onlyOwner {
    // Only owner can call this
    selfdestruct(payable(owner));
}
```

### Common Modifiers:
```solidity
// Check if enough ETH sent
modifier costs(uint amount) {
    require(msg.value >= amount, "Not enough ETH");
    _;
}

// Check if number is positive
modifier positive(uint number) {
    require(number > 0, "Must be positive");
    _;
}
```

---

## 7. Conditional Statements and Loops

### If-Else:
```solidity
function checkAge(uint age) public pure returns(string memory) {
    if (age >= 18) {
        return "Adult";
    } else if (age >= 13) {
        return "Teenager";
    } else {
        return "Child";
    }
}
```

### Ternary Operator:
```solidity
string memory status = (age >= 18) ? "Adult" : "Minor";
```

### For Loop:
```solidity
function sumArray(uint[] memory numbers) public pure returns(uint) {
    uint total = 0;
    for (uint i = 0; i < numbers.length; i++) {
        total += numbers[i];
    }
    return total;
}
```

### While Loop:
```solidity
function countDown(uint start) public pure returns(uint) {
    uint count = 0;
    while (start > 0) {
        start--;
        count++;
    }
    return count;
}
```

### Find Even Numbers Example:
```solidity
function findEvenNumbers(uint[] memory numbers) public pure returns(uint[] memory) {
    uint count = 0;
    // First pass: count even numbers
    for (uint i = 0; i < numbers.length; i++) {
        if (numbers[i] % 2 == 0) {
            count++;
        }
    }
    
    // Create result array
    uint[] memory evens = new uint[](count);
    uint index = 0;
    
    // Second pass: store even numbers
    for (uint i = 0; i < numbers.length; i++) {
        if (numbers[i] % 2 == 0) {
            evens[index] = numbers[i];
            index++;
        }
    }
    
    return evens;
}
```

---

## 8. Smart Contract Structure

### Basic Contract:
```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleStorage {
    // State variable
    uint private storedData;
    
    // Event
    event DataChanged(uint newValue, address changedBy);
    
    // Function to set data
    function set(uint newValue) public {
        storedData = newValue;
        emit DataChanged(newValue, msg.sender);
    }
    
    // Function to get data
    function get() public view returns(uint) {
        return storedData;
    }
}
```

---

## 9. Contract Lifecycle

### Deploy
- Contract is uploaded to blockchain
- Done by sending a transaction with contract bytecode
- Gets its own address
- Constructor runs once during deployment

```solidity
contract MyContract {
    address public owner;
    
    // Constructor runs once during deployment
    constructor() {
        owner = msg.sender;
    }
}
```

### Call
- Users interact with contract functions
- Two types of calls:
  - **Read (view/pure):** Free, doesn't change state
  - **Write:** Costs gas, changes state

### Destroy
- Contract can be deleted using `selfdestruct()`
- Sends remaining ETH to specified address
- Contract code remains on blockchain but becomes inactive

```solidity
function destroy() public onlyOwner {
    selfdestruct(payable(owner));
}
```

---

## 10. Tools

### Remix IDE
- Web-based development environment
- Website: https://remix.ethereum.org
- Features:
  - Write Solidity code
  - Compile contracts
  - Deploy to test networks
  - Debug transactions
  - No installation needed

### MetaMask
- Browser extension wallet
- Manages Ethereum accounts
- Connects to dApps
- Can switch between networks

### Ganache
- Personal blockchain for development
- Runs locally on your computer
- Comes with pre-funded test accounts
- Fast and free

### Truffle
- Development framework
- Features:
  - Compile contracts
  - Deploy contracts
  - Write tests
  - Manage networks

---

## CASE STUDY: Creating a Voting System using Solidity

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract Voting {
    // Data structures
    struct Candidate {
        string name;
        uint voteCount;
    }
    
    // State variables
    address public owner;
    mapping(address => bool) public hasVoted;
    Candidate[] public candidates;
    bool public votingActive;
    
    // Events
    event Voted(address voter, string candidateName);
    event CandidateAdded(string name);
    
    // Constructor
    constructor() {
        owner = msg.sender;
        votingActive = true;
    }
    
    // Add candidate (only owner)
    function addCandidate(string memory name) public {
        require(msg.sender == owner, "Only owner can add candidates");
        require(votingActive, "Voting is not active");
        candidates.push(Candidate(name, 0));
        emit CandidateAdded(name);
    }
    
    // Vote for candidate
    function vote(uint candidateIndex) public {
        require(votingActive, "Voting is not active");
        require(!hasVoted[msg.sender], "Already voted");
        require(candidateIndex < candidates.length, "Invalid candidate");
        
        hasVoted[msg.sender] = true;
        candidates[candidateIndex].voteCount++;
        emit Voted(msg.sender, candidates[candidateIndex].name);
    }
    
    // Get candidate details
    function getCandidate(uint index) public view returns(string memory, uint) {
        require(index < candidates.length, "Invalid candidate");
        return (candidates[index].name, candidates[index].voteCount);
    }
    
    // Get winner
    function getWinner() public view returns(string memory, uint) {
        require(candidates.length > 0, "No candidates");
        
        uint maxVotes = 0;
        uint winnerIndex = 0;
        
        for (uint i = 0; i < candidates.length; i++) {
            if (candidates[i].voteCount > maxVotes) {
                maxVotes = candidates[i].voteCount;
                winnerIndex = i;
            }
        }
        
        return (candidates[winnerIndex].name, maxVotes);
    }
    
    // End voting
    function endVoting() public {
        require(msg.sender == owner, "Only owner can end voting");
        votingActive = false;
    }
}
```

---

# UNIT V: HYPERLEDGER FABRIC

## 1. Introduction to Hyperledger Fabric

### What is Hyperledger?
- Open-source blockchain project by Linux Foundation
- Focus on enterprise solutions
- Multiple frameworks: Fabric, Sawtooth, Indy, etc.

### What is Hyperledger Fabric?
- Permissioned blockchain platform
- Designed for business use
- Modular architecture
- Supports smart contracts (called Chaincode)

### Key Features:
1. **Permissioned:** Only authorized members can join
2. **Modular:** Plug-and-play components
3. **Privacy:** Channels for private transactions
4. **Fast:** No mining, quick consensus
5. **Flexible:** Supports multiple programming languages

---

## 2. Permissioned vs Public Blockchain

| Feature | Public (Ethereum) | Permissioned (Fabric) |
|---------|-------------------|----------------------|
| Access | Anyone can join | Invitation only |
| Identity | Anonymous | Known identities |
| Consensus | PoW/PoS | Pluggable (Raft, Kafka) |
| Speed | Slow | Fast |
| Privacy | All data public | Private channels |
| Currency | Native cryptocurrency | Optional |
| Use Case | Public applications | Enterprise solutions |

---

## 3. Hyperledger Fabric vs Ethereum

| Feature | Fabric | Ethereum |
|---------|--------|----------|
| Type | Permissioned | Public |
| Consensus | Raft/Kafka | PoS |
| Smart Contracts | Chaincode (Go, Java, JS) | Solidity |
| Privacy | Channels | All public |
| Currency | Optional | Required (ETH) |
| Performance | High | Medium |
| Identity | Known | Pseudonymous |
| Governance | Consortium | Decentralized |

---

## 4. Hyperledger Fabric Architecture

### Components:

#### Peers
- Nodes that maintain the ledger
- Types:
  - **Endorsing Peer:** Executes chaincode, endorses transactions
  - **Committing Peer:** Validates and commits transactions
  - **Anchor Peer:** Connects different organizations
- Each organization runs its own peers

#### Orderers
- Orderer nodes arrange transactions into blocks
- No execution, only ordering
- Uses consensus (Raft)
- Creates blocks and sends to peers

#### Certificate Authorities (CA)
- Issues digital certificates
- Manages identities
- Based on PKI (Public Key Infrastructure)
- Fabric-CA is the implementation

#### Clients
- Applications that submit transactions
- User interface to the network
- SDK available in multiple languages

#### Membership Service Provider (MSP)
- Framework for managing identities
- Defines who is a member
- Issues certificates
- Controls access

---

## 5. Ledger in Fabric

### Two Parts:
1. **World State:**
   - Current values of all data
   - Like a database
   - Stored in CouchDB or LevelDB
   - Fast access to latest values

2. **Blockchain:**
   - Immutable history of all transactions
   - Chain of blocks
   - Complete audit trail

```
World State: Key-Value pairs (current values)
      ↑
Blockchain: Complete history (all changes)
```

---

## 6. Transactions and Endorsements

### Transaction Flow:
1. **Proposal:** Client sends transaction proposal to endorsing peers
2. **Execution:** Peers execute chaincode
3. **Endorsement:** Peers sign the result
4. **Submission:** Client sends endorsed transaction to orderer
5. **Ordering:** Orderer creates block
6. **Validation:** Peers validate transaction
7. **Commit:** Transaction written to ledger

### Endorsement Policy
- Rules defining who must endorse a transaction
- Example: "2 out of 3 organizations must endorse"
- Ensures trust without requiring everyone

---

## 7. Channels and Private Data Collections

### Channels
- Private sub-networks within Fabric
- Only channel members can see transactions
- Each channel has its own ledger
- Example: Bank A and Bank B have a channel for their transactions

### Private Data Collections
- Share data with specific organizations
- Data not on the main channel ledger
- Only hash is on blockchain
- Example: Sharing customer details only with partner organizations

---

## 8. Chaincode and Smart Contracts

### What is Chaincode?
- Fabric's term for smart contracts
- Business logic that runs on peers
- Can be written in:
  - Go (Golang)
  - Java
  - JavaScript/Node.js

### Basic Structure (JavaScript):
```javascript
const { Contract } = require('fabric-contract-api');

class MyContract extends Contract {
    async initLedger(ctx) {
        // Initialize data
    }
    
    async queryData(ctx, key) {
        // Read data
    }
    
    async createData(ctx, key, value) {
        // Write data
    }
}

module.exports = MyContract;
```

---

## 9. Lifecycle of Chaincode

### Step 1: Package
- Bundle chaincode code and metadata
- Create a .tar.gz file

### Step 2: Install
- Install on peers that will execute it
- Done by each organization

### Step 3: Approve
- Each organization approves the chaincode definition
- Includes: name, version, endorsement policy

### Step 4: Commit
- Commit the approved definition to the channel
- Requires enough organizations to approve

### Step 5: Invoke
- Call chaincode functions
- Read or write data

---

## 10. Endorsement Policies and Validation

### Endorsement Policies
Define who must approve transactions:

```
AND(Org1.Member, Org2.Member)
→ Both Org1 and Org2 must endorse

OR(Org1.Member, Org2.Member)
→ Either Org1 or Org2 must endorse

OutOf(2, Org1.Member, Org2.Member, Org3.Member)
→ Any 2 of the 3 organizations must endorse
```

### Validation
Before committing, peers check:
1. Correct endorsements
2. Valid signatures
3. Read-write set consistency
4. No double spending

---

## CASE STUDY: Hyperledger Fabric in Healthcare - MedRec

### The Problem
- Patient records scattered across hospitals
- No unified system
- Privacy concerns
- Difficult to share data between providers

### MedRec Solution
- Built on Hyperledger Fabric
- Manages patient health records
- Features:
  - Patients control their data
  - Providers request access
  - Immutable audit trail
  - Private channels for sensitive data

### How it Works:
1. Patient record created at hospital
2. Record stored with patient's permission
3. Other hospitals request access
4. Patient grants/denies permission
5. All access logged on blockchain

### Benefits:
- Patient ownership of data
- Secure sharing
- Complete audit trail
- Interoperability between systems

---

# UNIT VI: CHALLENGES, SECURITY, AND FUTURE TRENDS

## 1. Blockchain Limitations

### Scalability
- **Problem:** Blockchains process fewer transactions than traditional systems
- **Bitcoin:** ~7 transactions per second
- **Ethereum:** ~15-30 transactions per second
- **Visa:** ~24,000 transactions per second
- **Why:** Every node must process every transaction

### Solutions:
- Layer 2 solutions (Lightning Network, Rollups)
- Sharding (splitting network)
- Larger blocks
- Faster consensus

### Speed
- **Problem:** Block creation takes time
- Bitcoin: 10 minutes per block
- Ethereum: 12 seconds per block
- Confirmation needs multiple blocks
- **Result:** Not suitable for instant payments

### Cost
- **Problem:** Transaction fees can be high
- Ethereum gas fees: $5-$100+ during busy times
- Storage on blockchain is expensive
- **Why:** Limited block space, high demand

---

## 2. Security Issues

### 51% Attack
- **What:** Attacker controls more than 50% of network power
- **Can do:**
  - Reverse their own transactions (double spend)
  - Prevent new transactions
  - Stop other miners
- **Cannot do:**
  - Create new coins
  - Steal others' coins
  - Change old transactions
- **More likely in:** Small blockchains
- **Example:** Ethereum Classic suffered multiple 51% attacks

### Sybil Attack
- **What:** Attacker creates many fake identities
- **Goal:** Influence network decisions
- **Defense:** 
  - PoW (requires real computing power)
  - PoS (requires real money)
  - Known identities (permissioned)

### Replay Attack
- **What:** Valid transaction is repeated on another chain
- **When it happens:** After blockchain forks
- **Example:** After Ethereum fork, transactions could be replayed on ETC
- **Defense:** Chain ID in transactions, replay protection

### Other Attacks:
- **Phishing:** Tricking users to reveal private keys
- **Dusting:** Sending tiny amounts to track addresses
- **Routing attacks:** Intercepting network traffic

---

## 3. Privacy Enhancements

### ZK-SNARKs (Zero-Knowledge Succinct Non-Interactive Argument of Knowledge)
- **What:** Prove you know something without revealing what it is
- **Example:** Prove you're over 18 without showing your birthdate
- **Used by:** Zcash for private transactions
- **Benefits:** Complete privacy, small proof size

### Ring Signatures
- **What:** Mix your signature with others
- **Result:** Transaction appears to be from a group
- **Used by:** Monero for privacy
- **Benefits:** Cannot trace who actually signed

### Other Privacy Tools:
- **CoinJoin:** Combine multiple payments
- **Stealth Addresses:** One-time addresses
- **Confidential Transactions:** Hide amounts

---

## 4. Blockchain Interoperability

### What is it?
- Different blockchains communicating with each other
- Like the internet connects different networks

### Why needed?
- Many separate blockchains exist
- Users want to move assets between them
- Avoid being locked into one blockchain

### Solutions:
- **Bridges:** Connect two blockchains
- **Polkadot:** Connects multiple chains (parachains)
- **Cosmos:** Internet of blockchains
- **Atomic Swaps:** Direct exchange between chains

---

## 5. Regulations, Compliance, and Legal Frameworks

### Current Status:
- Varies by country
- Some embrace, some ban, some regulate

### Key Areas:
1. **KYC/AML:** Know Your Customer, Anti-Money Laundering
2. **Taxation:** How to tax crypto gains
3. **Securities:** When is a token a security?
4. **Consumer Protection:** Protecting users from fraud

### Regulatory Approaches:
- **USA:** SEC regulates some tokens as securities
- **EU:** MiCA (Markets in Crypto-Assets) regulation
- **India:** Taxation, cautious approach
- **El Salvador:** Bitcoin as legal tender

---

## 6. Future Trends

### Web3
- **What:** Decentralized internet
- **Vision:** Users own their data, not corporations
- **Components:** Blockchain, crypto, dApps
- **Goal:** Return power to users

### DAO (Decentralized Autonomous Organization)
- **What:** Organization run by smart contracts
- **No central leadership**
- **Decisions made by voting**
- **Members hold tokens**
- **Example:** MakerDAO manages DAI stablecoin

### CBDC (Central Bank Digital Currency)
- **What:** Digital version of national currency
- **Issued by:** Central banks
- **Examples:** Digital Yuan (China), Digital Euro (planned)
- **Benefits:** Faster payments, financial inclusion
- **Concerns:** Privacy, government control

### Quantum-Resistant Blockchain
- **Problem:** Future quantum computers could break current cryptography
- **Threat:** Could steal funds, forge signatures
- **Solution:** Quantum-resistant algorithms
- **Status:** Research ongoing, not urgent yet

---

## CASE STUDY: Security Breaches - The DAO Hack

### What was The DAO?
- Decentralized venture fund on Ethereum
- Raised $150 million in 2016
- Investors could vote on projects
- Smart contract controlled the funds

### The Hack:
- **Vulnerability:** Reentrancy bug in the code
- **What happened:**
  1. Attacker requested withdrawal
  2. Before balance was updated, called withdrawal again
  3. Repeated this many times
  4. Drained $60 million
- **How:** Recursive calls before state update

### The Aftermath:
- Ethereum community debated response
- Decision: Hard fork to reverse the hack
- Created two chains:
  - Ethereum (ETH) - with reversal
  - Ethereum Classic (ETC) - no reversal
- **Lesson:** Smart contract security is critical

### Prevention:
- Code audits
- Testing
- Bug bounties
- Withdrawal limits
- Emergency stop functions

---

# QUESTIONS BY COURSE OUTCOME

## COURSE OUTCOME 1: Recall the basic concepts, characteristics, types, and historical development of blockchain and its network models.

### Short Answer Questions (2-4 marks):
1. Define blockchain technology in simple terms.
2. What is the difference between central, distributed, and decentralized networks? Give one example of each.
3. List any four characteristics of blockchain technology.
4. What is a block in blockchain? What information does it contain?
5. Explain the concept of "chaining" in blockchain.
6. Differentiate between public and private blockchain.
7. What is consortium blockchain? Give one example.
8. Define distributed ledger. How is it different from traditional ledger?
9. What is a peer-to-peer network?
10. Name any four types of blockchain nodes.
11. What is the function of a full node?
12. What is a light node and why is it useful?
13. What is Blockchain 1.0? Give an example.
14. What is Blockchain 2.0? How is it different from Blockchain 1.0?
15. List three opportunities where blockchain can be used.
16. What is a hybrid blockchain?
17. What is the role of a miner node?
18. What is an archive node?
19. What is the difference between a validator node and a miner node?
20. Define immutable in the context of blockchain.

### Long Answer Questions (6-8 marks):
1. Explain the evolution of blockchain from 1.0 to 3.0 with examples.
2. Compare and contrast public, private, consortium, and hybrid blockchains with suitable examples.
3. Explain in detail the different types of blockchain nodes and their functions.
4. Describe the characteristics of blockchain and explain how they provide advantages over traditional systems.
5. What is a distributed ledger? Explain how peer-to-peer networks work in blockchain.
6. Explain the concept of block and chaining with a suitable example. Why does this make blockchain tamper-proof?
7. Discuss the various applications and opportunities of blockchain technology in different industries.
8. Explain the TradeLens case study. How did IBM and Maersk use blockchain in supply chain management?

---

## COURSE OUTCOME 2: Explain the role of encryption, hashing, and consensus mechanisms in ensuring blockchain integrity and security.

### Short Answer Questions (2-4 marks):
1. What is cryptography? Why is it important in blockchain?
2. Differentiate between symmetric and asymmetric cryptography.
3. What are public key and private key? How are they related?
4. What is a digital signature? List its properties.
5. What is hashing? List four properties of a good hash function.
6. What is SHA-256? Which blockchain uses it?
7. What is a Merkle tree? Why is it useful?
8. What is the Byzantine Generals Problem?
9. What is Byzantine Fault Tolerance (BFT)?
10. Explain Proof of Work (PoW) consensus mechanism.
11. Explain Proof of Stake (PoS) consensus mechanism.
12. What is Proof of Authority (PoA)? Where is it used?
13. What is Proof of Capacity (PoC)?
14. Compare PoW and PoS in terms of energy consumption.
15. What is the transaction life cycle in blockchain?
16. Why is blockchain considered secure?
17. What is the difference between on-chain and off-chain storage?
18. What is consensus and why is it needed in blockchain?
19. What is a nonce in the context of mining?
20. What is a Merkle root?

### Long Answer Questions (6-8 marks):
1. Explain symmetric and asymmetric cryptography with examples. How are they used in blockchain?
2. Explain digital signatures in detail. How do they ensure authenticity and integrity?
3. Explain hashing functions and Merkle tree with a diagram. How do they contribute to blockchain security?
4. Compare and contrast PoW, PoS, PoA, and PoC consensus mechanisms with their advantages and disadvantages.
5. Explain the Byzantine Generals Problem and how Byzantine Fault Tolerance solves it.
6. Describe the complete transaction life cycle in a blockchain from creation to confirmation.
7. Explain how Bitcoin uses Proof-of-Work and SHA-256 hashing. Describe the mining process.
8. Discuss the various security features of blockchain. How does cryptography ensure blockchain integrity?

---

## COURSE OUTCOME 3: Identify and describe key components of the Ethereum ecosystem and compare Ethereum with Bitcoin.

### Short Answer Questions (2-4 marks):
1. What is Ethereum? How is it different from Bitcoin?
2. What is an Ethereum address? Give an example format.
3. Differentiate between Externally Owned Accounts (EOA) and Contract Accounts.
4. What is Ether (ETH)? What is its smallest unit?
5. What is the Ethereum Virtual Machine (EVM)?
6. What is gas in Ethereum? Why is it needed?
7. What is the difference between gas price and gas limit?
8. List any four tools in the Ethereum ecosystem.
9. What is the difference between ETH and ETC?
10. What is Etherscan? What can you do with it?
11. What are the different types of Ethereum wallets?
12. What is a nonce in Ethereum transactions?
13. Explain the "Data" field in an Ethereum transaction.
14. What is the difference between Bitcoin and Ethereum in terms of block time?
15. What is the consensus mechanism used by Ethereum currently?
16. What is Wei? How many Wei are in 1 ETH?
17. What is a smart contract? Give one example.
18. What is Gwei and why is it commonly used?
19. List three differences between Bitcoin and Ethereum.
20. What is the supply limit of Bitcoin vs Ethereum?

### Long Answer Questions (6-8 marks):
1. Explain the Ethereum ecosystem in detail. Describe its key components with examples.
2. Compare and contrast Bitcoin and Ethereum across various parameters.
3. Explain Ethereum accounts, transactions, and the role of EVM in detail.
4. Describe the Ethereum transaction life cycle. Explain all key terms used in an Ethereum transaction.
5. Explain the concept of gas in Ethereum. How does gas price and gas limit affect transactions?
6. Discuss the Ethereum development tool stack. Explain the role of MetaMask, Ganache, and Truffle.
7. Explain the Uniswap case study. How does DeFi work on Ethereum?
8. What are smart contracts? Explain their properties and give examples of real-world use cases.

---

## COURSE OUTCOME 4: Use Solidity syntax to write and deploy simple smart contracts using Remix IDE.

### Short Answer Questions (2-4 marks):
1. What is Solidity? Which platform is it used for?
2. What is Remix IDE? List its features.
3. List five data types used in Solidity.
4. What is the difference between uint and int in Solidity?
5. What is a mapping in Solidity? Give an example.
6. What is a struct in Solidity? Why is it useful?
7. Explain the visibility specifiers in Solidity functions.
8. What is the difference between view and pure functions?
9. What are modifiers in Solidity? Give an example.
10. What is a payable function?
11. What is msg.sender and msg.value?
12. What is the contract lifecycle in Solidity?
13. What is the purpose of the constructor in Solidity?
14. What is selfdestruct()? When is it used?
15. Write the basic syntax of a Solidity function.
16. What are events in Solidity? Why are they used?
17. What is the difference between storage, memory, and calldata?
18. How do you write comments in Solidity?
19. What is the purpose of pragma solidity?
20. What tools are used alongside Solidity for development?

### Long Answer Questions (6-8 marks):
1. Explain the basic syntax and structure of Solidity with examples.
2. Explain all data types in Solidity with suitable examples. How are arrays, structs, and mappings used?
3. Explain functions in Solidity. Discuss visibility, state mutability, and modifiers with examples.
4. Write a Solidity contract that stores and manages student records with functions to add, view, and update records.
5. Write a Solidity contract to find even numbers from an array using loops and conditionals.
6. Explain the contract lifecycle in Solidity. Describe deployment, function calls, and destruction.
7. Explain how to use Remix IDE to write, compile, and deploy a smart contract.
8. Write a complete voting system smart contract in Solidity and explain each part.

### Practical Questions:
1. Write a Solidity contract with a function that uses a for loop to calculate the sum of numbers in an array.
2. Write a Solidity contract that uses if-else conditions to categorize a number as positive, negative, or zero.
3. Write a Solidity contract with a modifier that restricts function access to only the contract owner.
4. Create a Solidity contract that maintains a simple bank account with deposit, withdraw, and balance check functions.
5. Write a Solidity contract using structs to store employee information (name, id, salary).

---

## COURSE OUTCOME 5: Illustrate the architecture and components of Hyperledger Fabric with its permissioned blockchain features.

### Short Answer Questions (2-4 marks):
1. What is Hyperledger Fabric?
2. What is the difference between permissioned and public blockchain?
3. Compare Hyperledger Fabric and Ethereum.
4. What are peers in Hyperledger Fabric?
5. What is the role of orderers in Fabric?
6. What is Certificate Authority (CA) in Fabric?
7. What is MSP (Membership Service Provider)?
8. What is world state in Fabric ledger?
9. What is the difference between endorsing peer and committing peer?
10. What is a channel in Hyperledger Fabric?
11. What are private data collections?
12. What is chaincode?
13. List the programming languages supported for writing chaincode.
14. What is the lifecycle of chaincode in Fabric?
15. What is an endorsement policy?
16. What is the difference between Fabric and Bitcoin?
17. What is an anchor peer?
18. What is a client in Fabric architecture?
19. What databases can be used for world state in Fabric?
20. What is the transaction flow in Hyperledger Fabric?

### Long Answer Questions (6-8 marks):
1. Explain the architecture of Hyperledger Fabric with all its components in detail.
2. Compare permissioned and public blockchains. Why is Fabric considered better for enterprise use?
3. Explain the different components of Hyperledger Fabric: Peers, Orderers, CA, Clients, and MSP.
4. Explain the ledger structure in Fabric. How does world state differ from blockchain?
5. Describe the complete transaction flow in Hyperledger Fabric from proposal to commit.
6. Explain the chaincode lifecycle in Fabric. Describe each step from packaging to invocation.
7. What are channels and private data collections? How do they provide privacy in Fabric?
8. Explain the MedRec case study. How is Hyperledger Fabric used in healthcare record management?

---

## COURSE OUTCOME 6: Recognize common blockchain challenges, security threats, and describe emerging trends such as Web3 and quantum resistance.

### Short Answer Questions (2-4 marks):
1. What is the scalability problem in blockchain?
2. Why are blockchain transaction fees sometimes very high?
3. What is a 51% attack? What can an attacker do?
4. What is a Sybil attack? How can it be prevented?
5. What is a replay attack? When does it occur?
6. What are ZK-SNARKs? How do they enhance privacy?
7. What are ring signatures? Which cryptocurrency uses them?
8. What is blockchain interoperability? Why is it needed?
9. What is Web3? How is it different from Web2?
10. What is a DAO? How does it work?
11. What is CBDC? Give two examples.
12. What is quantum-resistant blockchain? Why is it needed?
13. What are the main limitations of blockchain technology?
14. List three security issues in blockchain.
15. What is the role of regulations in blockchain?
16. What is KYC/AML in the context of blockchain?
17. What is a bridge in blockchain interoperability?
18. What is Polkadot and how does it help interoperability?
19. What was the DAO hack? What vulnerability was exploited?
20. How can smart contract vulnerabilities be prevented?

### Long Answer Questions (6-8 marks):
1. Explain the scalability, speed, and cost limitations of blockchain. What are the possible solutions?
2. Explain 51% attack, Sybil attack, and replay attack in detail. How can they be prevented?
3. Explain privacy enhancement techniques in blockchain: ZK-SNARKs and ring signatures with examples.
4. What is blockchain interoperability? Explain different solutions for achieving it.
5. Discuss the regulatory challenges and legal frameworks for blockchain technology.
6. Explain emerging trends in blockchain: Web3, DAO, CBDC, and quantum-resistant blockchain.
7. Explain the DAO hack case study in detail. What was the vulnerability and how was it resolved?
8. Discuss the future of blockchain technology. What are the major challenges and opportunities ahead?

---

# QUICK REFERENCE TABLES

## Blockchain Types Summary

| Type | Access | Control | Speed | Example |
|------|--------|---------|-------|---------|
| Public | Anyone | Decentralized | Slow | Bitcoin, Ethereum |
| Private | Invited only | One org | Fast | Internal company |
| Consortium | Selected orgs | Group | Medium | Banking network |
| Hybrid | Mixed | Mixed | Mixed | Enterprise solutions |

## Consensus Mechanisms Summary

| Mechanism | Used By | Energy | Speed | Decentralization |
|-----------|---------|--------|-------|------------------|
| PoW | Bitcoin | High | Slow | High |
| PoS | Ethereum 2.0 | Low | Fast | High |
| PoA | Private chains | Very Low | Very Fast | Low |
| PoC | Burstcoin | Low | Medium | Medium |

## Node Types Summary

| Node | Storage | Function |
|------|---------|----------|
| Full Node | Complete blockchain | Validates everything |
| Light Node | Block headers only | Quick verification |
| Miner Node | Complete + mining tools | Creates blocks |
| Archive Node | Everything + history | Analytics, queries |
| Validator Node | Complete | Votes on blocks (PoS) |

## Key Formulas and Values

```
1 ETH = 1,000,000,000,000,000,000 Wei (10^18)
1 ETH = 1,000,000,000 Gwei (10^9)
1 Gwei = 1,000,000,000 Wei (10^9)

Bitcoin Block Time: ~10 minutes
Ethereum Block Time: ~12 seconds
Bitcoin Max Supply: 21 million
BFT Requirement: Honest nodes > 2/3 total

SHA-256 Output: 256 bits (64 hex characters)
Ethereum Address: 160 bits (40 hex characters + 0x prefix)
```

---

# TIPS FOR EXAMINATION

## For CIE (20 Marks):
- Focus on assignments and practical work
- Complete all 10 assignments thoroughly
- Practice writing Solidity code
- Understand case studies well

## For SCE (20 Marks):
- Focus on practical skills
- Be ready to write smart contracts
- Demonstrate understanding of tools (Remix, MetaMask)
- Show blockchain concepts practically

## For ESE (40 Marks):
- Study all 6 units thoroughly
- Practice writing long answers
- Use diagrams where possible
- Give examples for each concept
- Attempt questions from all units

## General Tips:
1. **Understand, don't memorize:** Blockchain concepts are logical
2. **Use diagrams:** Draw blockchain structures, network types, transaction flows
3. **Give examples:** Real-world examples score better
4. **Compare and contrast:** Tables are great for comparison questions
5. **Case studies:** Know at least the key points of each case study
6. **Practice Solidity:** Write at least 5 different smart contracts
7. **Current affairs:** Know recent blockchain developments

---

*End of Preparation Notes*
*All topics from syllabus covered with simple explanations and examples*
