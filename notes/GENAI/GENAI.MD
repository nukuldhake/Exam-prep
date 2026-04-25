# **AD32233: Generative AI – Comprehensive Course Material**

## **Unit I: Introduction to Generative AI**
**Course Objective:** Understand the fundamental concepts, evolution, and ethical considerations of Generative AI.
**Course Outcome 1:** Explain the principles and applications of Generative AI in various domains.

### **Detailed Theoretical Preparation Notes**

**1. Evolution of AI: Traditional AI vs. Generative AI**
*   **Traditional AI (Discriminative):** Focuses on analyzing data to make predictions or classifications. It learns boundaries between classes (e.g., classifying an image as a cat or a dog). Models include SVMs, Decision Trees, and standard CNNs. It answers "What is this?"
*   **Generative AI (Generative):** Focuses on understanding the underlying distribution of data to generate new, synthetic data instances that resemble the original data. It answers "What comes next?" or "Can you create something like this?"
*   **Evolution:** Rule-based systems $\rightarrow$ Machine Learning $\rightarrow$ Deep Learning (Discriminative) $\rightarrow$ Deep Generative Models.

**2. Foundations of Generative Models**
*   **Probabilistic Models:** These models assume data is generated from an underlying probability distribution. The goal is to estimate this distribution $P(X)$ (unsupervised) or $P(X|Y)$ (conditional). Examples: Hidden Markov Models, Gaussian Mixture Models.
*   **Representation Learning:** Instead of relying on manual feature engineering, generative models learn latent representations (hidden features) of the data. This "latent space" captures the essence of the data, allowing the model to decode it back into realistic outputs.

**3. Overview of Deep Generative Models**
*   **VAEs (Variational Autoencoders):** Encode data into a probabilistic latent space and decode it. Good for smooth, continuous generation and feature interpolation.
*   **GANs (Generative Adversarial Networks):** Two networks (Generator and Discriminator) compete. The generator tries to fool the discriminator. Excellent for high-fidelity, sharp image generation.
*   **Transformers:** Rely on self-attention mechanisms to process sequential data. The foundation for modern Large Language Models (LLMs) and increasingly for image/video generation.

**4. Applications of Generative AI**
*   **Text:** Chatbots, code generation (GitHub Copilot), summarization, translation.
*   **Image:** Art generation, deepfakes, medical image synthesis, graphic design.
*   **Audio:** Text-to-speech, music composition, voice cloning.
*   **Code:** Automated bug fixing, code refactoring, script generation.
*   **Synthetic Data:** Generating data to train other models where real data is scarce or privacy-restricted (e.g., financial/healthcare records).

**5. Ethical and Societal Impacts of Generative AI**
*   **Bias & Fairness:** Models can inherit and amplify biases present in training data (e.g., gender/racial biases in generated images or text).
*   **Misinformation & Deepfakes:** Erosion of truth, fake news generation, political manipulation.
*   **Copyright & Intellectual Property:** Who owns AI-generated art? Issues of using copyrighted data for training without consent.
*   **Job Displacement:** Automation of creative, coding, and copywriting roles.

**6. Introduction to RAG (Retrieval-Augmented Generation)**
*   **Concept:** A framework that improves LLM responses by retrieving factual, external data before generating an answer. It mitigates "hallucinations."
*   **Workflow:** User Query $\rightarrow$ Query Embedding $\rightarrow$ Search Vector Database $\rightarrow$ Retrieve Relevant Context $\rightarrow$ Pass Context + Query to LLM $\rightarrow$ Generate Response.

**7. Overview of Vector Databases**
*   **Purpose:** Store and efficiently query high-dimensional vector embeddings (mathematical representations of text/images).
*   **ChromaDB:** Open-source, developer-friendly, runs locally, great for prototyping RAG.
*   **Pinecone:** Fully managed, cloud-native, highly scalable vector database for production.
*   **PostgreSQL Vector (pgvector):** Extension for PostgreSQL enabling vector similarity search within traditional relational databases.

---

### **Possible Questions for Course Outcome 1**
**Remembering:**
1. Define Generative AI. How does it differ from Traditional (Discriminative) AI?
2. List the three main deep generative model architectures.
3. Name three applications of Generative AI across different modalities.
4. What is the primary purpose of a Vector Database?
5. State the full form of RAG and define its purpose.

**Understanding:**
6. Explain the concept of "Representation Learning" in the context of generative models.
7. How do probabilistic models form the foundation of generative AI?
8. Describe the societal impacts of Generative AI regarding misinformation and copyright.
9. Explain the workflow of Retrieval-Augmented Generation (RAG).
10. Compare ChromaDB, Pinecone, and PostgreSQL Vector for vector storage.

**Applying:**
11. Propose a RAG architecture for a legal document chatbot. Why is it better than a standalone LLM?
12. How would you use generative AI for synthetic data generation in a privacy-sensitive domain like healthcare?

**Analyzing:**
13. Analyze the ethical implications of using LLMs trained on public internet data for commercial art generation.
14. Why has Generative AI surged in popularity recently compared to traditional probabilistic models?

**Evaluating:**
15. Evaluate the pros and cons of using an open-source vector DB (ChromaDB) vs. a managed service (Pinecone) for an enterprise application.
16. "Generative AI will do more harm than good to society." Debate this statement with examples.

---

## **Unit II: Variational Autoencoders (VAEs)**
**Course Objective:** Learn the working principles of VAEs and their applications in generative modeling.
**Course Outcome 2:** Implement Variational Autoencoders (VAEs) and understand their role in generative modeling.

### **Detailed Theoretical Preparation Notes**

**1. Introduction to Autoencoders: Structure and Functioning**
*   **Concept:** An unsupervised neural network used for learning efficient data encodings.
*   **Structure:** Consists of an **Encoder** (maps input $X$ to a latent vector $z$) and a **Decoder** (reconstructs $X'$ from $z$).
*   **Functioning:** Trained to minimize the reconstruction loss ($|X - X'|^2$). Traditionally used for dimensionality reduction or denoising, not generation (because the latent space is irregular).

**2. Variational Autoencoder (VAE): Bayesian Inference & KL Divergence**
*   **Bayesian Inference:** Instead of mapping an input to a single fixed vector (deterministic), a VAE maps it to a *distribution* (typically Gaussian). It assumes the data is generated from some latent variable $z$ with a prior $P(z)$.
*   **KL Divergence (Kullback-Leibler Divergence):** A measure of how one probability distribution differs from a second, expected probability distribution. In VAEs, it forces the learned latent distribution $q(z|X)$ to be close to the prior $P(z)$ (usually a standard normal distribution $\mathcal{N}(0, 1)$). This ensures the latent space is continuous and smooth.

**3. VAE Training: Reparameterization Trick & Loss Function**
*   **Reparameterization Trick:** To train a neural network via backpropagation, all operations must be differentiable. Sampling $z$ directly from $q(z|X)$ is non-differentiable. The trick rewrites the random variable: $z = \mu + \sigma \odot \epsilon$, where $\epsilon \sim \mathcal{N}(0, 1)$. Now, the network learns $\mu$ and $\sigma$, and the randomness comes from an external input $\epsilon$.
*   **Loss Function (ELBO - Evidence Lower Bound):** The VAE loss consists of two parts:
    1.  **Reconstruction Loss:** How well does $X'$ match $X$? (e.g., Binary Cross-Entropy or MSE).
    2.  **KL Divergence Loss:** How close is the learned distribution $q(z|X)$ to $\mathcal{N}(0, 1)$?
    *   *Total Loss = Reconstruction Loss + KL Divergence Loss.*

**4. Applications of VAEs**
*   **Image Generation:** Generating faces, digits, or interpolating between faces (e.g., morphing one face into another).
*   **Text Generation:** Generating syntactic structures or semantic embeddings.
*   **Anomaly Detection:** High reconstruction loss indicates an anomaly.
*   **Drug Discovery:** Generating novel molecular structures (e.g., latent space exploration).

**5. Case Study: Implementing VAEs using PyTorch/TensorFlow**
*   *Key Steps:* Define Encoder (Dense/Conv layers outputting $\mu$ and $\sigma$), apply reparameterization, define Decoder (Dense/ConvTranspose layers), calculate combined loss, optimize using Adam.

**6. Accuracy Measures for Generative Models**
*   **ELBO (Evidence Lower Bound):** The theoretical objective function. Maximizing ELBO is equivalent to minimizing the KL divergence between the true posterior and approximate posterior.
*   **Reconstruction Error:** Pixel-wise MSE or BCE. Good for autoencoders, but doesn't measure "realism" well.
*   *(Note: FID (Fréchet Inception Distance) and IS (Inception Score) are modern metrics, though not explicitly listed, they are often discussed alongside VAE/GAN accuracy).*

---

### **Possible Questions for Course Outcome 2**
**Remembering:**
1. Draw the basic architecture of an Autoencoder.
2. What is KL Divergence?
3. State the two components of the VAE loss function.
4. What is the purpose of the reparameterization trick?

**Understanding:**
5. Why is a standard Autoencoder not suitable for generating new data, and how does a VAE solve this?
6. Explain the role of Bayesian Inference in Variational Autoencoders.
7. Mathematically explain the reparameterization trick. Why is it necessary for backpropagation?
8. How does ELBO relate to the training objective of a VAE?

**Applying:**
9. Write a pseudocode/Python snippet to implement the reparameterization trick.
10. How would you use a VAE for anomaly detection in a manufacturing setup?

**Analyzing:**
11. Compare the latent space of a standard Autoencoder versus a Variational Autoencoder.
12. Why might a VAE generate blurrier images compared to a GAN?

**Evaluating:**
13. Evaluate the suitability of Reconstruction Error vs. ELBO as accuracy measures for a VAE trained on facial generation.
14. Given a scenario where a VAE is generating blurry images, what hyperparameters or architectural changes would you adjust and why?

---

## **Unit III: Generative Adversarial Networks (GANs)**
**Course Objective:** Gain insights into GAN architectures, training challenges, and applications.
**Course Outcome 3:** Develop and train Generative Adversarial Networks (GANs) for realistic data generation.

### **Detailed Theoretical Preparation Notes**

**1. Introduction to GANs: Generator and Discriminator Networks**
*   **Concept:** A zero-sum game between two neural networks.
*   **Generator ($G$):** Takes random noise $z$ (from a prior distribution) and generates fake data. Its goal is to fool the discriminator.
*   **Discriminator ($D$):** Takes data (either real from the dataset or fake from $G$) and outputs a probability of it being real. Its goal is to correctly identify fakes.

**2. Training GANs: Minimax Game & Loss Functions**
*   **Minimax Game:** $\min_G \max_D V(D, G) = \mathbb{E}_{x \sim p_{data}}[\log D(x)] + \mathbb{E}_{z \sim p_z}[\log(1 - D(G(z)))]$
*   **Training Process:**
    1. Train $D$ to distinguish real from fake (maximize loss).
    2. Train $G$ to generate data that $D$ classifies as real (minimize loss).
*   **Loss Functions:** Standard GAN uses Binary Cross-Entropy (BCE) Loss. Variants use Wasserstein loss (WGAN) to improve stability.

**3. Types of GANs**
*   **DCGAN (Deep Convolutional GAN):** Uses Convolutional layers instead of Dense layers. Introduced architectural guidelines (e.g., using BatchNorm, avoiding fully connected layers, using ReLU/LeakyReLU) to stabilize training.
*   **CycleGAN:** Used for *unpaired* image-to-image translation (e.g., turning a horse into a zebra without paired examples). Uses cycle-consistency loss (Image A $\rightarrow$ B $\rightarrow$ A' should equal A).
*   **StyleGAN:** Introduced by Nvidia. Uses a mapping network to transform latent code into an intermediate latent space (style). Controls image generation at different resolutions (coarse features like face shape vs. fine features like hair color). Produces photorealistic high-res faces.

**4. Challenges in GANs**
*   **Mode Collapse:** The generator finds only a few modes (types of outputs) that fool the discriminator and continuously outputs them, ignoring the diversity of the real dataset. (e.g., generating only "1s" when trained on MNIST).
*   **Training Instability:** The delicate balance between $G$ and $D$. If $D$ gets too good, gradients vanish for $G$. If $G$ gets too good, $D$ is useless.
*   **Vanishing Gradients / Non-convergence.**

**5. Hands-on Implementation of GANs**
*   *Key steps:* Define $G$ (transposed convolutions) and $D$ (strided convolutions), alternate training loops, track losses visually to ensure equilibrium.

**6. Teacher-Student Model Architecture for GANs in Industry**
*   **Concept:** Knowledge Distillation. A large, complex "Teacher" GAN generates a massive dataset of synthetic images. A smaller, faster "Student" model is trained on this synthetic data.
*   **Application (Healthcare - Anomaly Detection):** Train a Teacher GAN on healthy tissue scans. Use it to generate synthetic healthy data. Train a lightweight student model to recognize healthy tissue. Any deviation detected by the student in real patient scans is flagged as an anomaly.

---

### **Possible Questions for Course Outcome 3**
**Remembering:**
1. Define the roles of the Generator and Discriminator in a GAN.
2. What is Mode Collapse?
3. Name three variants of GANs and their primary use cases.

**Understanding:**
4. Explain the Minimax game theory applied to GAN training.
5. How does a DCGAN differ from a standard Vanilla GAN architecturally?
6. Explain the concept of "Cycle Consistency Loss" in CycleGAN.
7. Describe the Teacher-Student model architecture in the context of GANs.

**Applying:**
8. Write the PyTorch/TensorFlow pseudocode for the discriminator training loop in a GAN.
9. How would you apply CycleGAN to convert daytime street images to nighttime street images for autonomous driving training?

**Analyzing:**
10. Analyze why Mode Collapse occurs and propose two methods to mitigate it.
11. Compare the image quality and training stability of a VAE versus a GAN.
12. Why is StyleGAN capable of generating higher-resolution, more realistic images than DCGAN?

**Evaluating:**
13. Evaluate the ethical implications and technical benefits of using Teacher-Student GAN architectures for anomaly detection in healthcare.
14. If a GAN's discriminator loss drops to zero very early in training, what does this indicate, and how would you fix the architecture?

---

## **Unit IV: Transformer-based Generative Models**
**Course Objective:** Explore the role of transformers in text generation and large language models (LLMs).
**Course Outcome 4:** Utilize transformer-based models for text generation and NLP applications.

### **Detailed Theoretical Preparation Notes**

**1. Introduction to Transformers: Self-Attention Mechanism**
*   **Concept:** A neural network architecture introduced in "Attention is All You Need" (2017) that processes data in parallel, replacing sequential models like RNNs/LSTMs.
*   **Self-Attention:** Allows the model to weigh the importance of different words in a sequence when processing a specific word. Calculates Query (Q), Key (K), and Value (V) vectors.
    *   *Attention(Q, K, V) = softmax(QK^T / sqrt(d_k)) V*
*   **Multi-Head Attention:** Runs multiple attention mechanisms in parallel to capture different relationships (e.g., grammar, semantics).

**2. Evolution of Language Models**
*   **BERT (Bidirectional Encoder Representations from Transformers):** Encoder-only. Excellent for understanding text (classification, NER, sentiment). Masked Language Modeling (MLM).
*   **GPT (Generative Pre-trained Transformer):** Decoder-only. Autoregressive (predicts the next word). Excellent for text generation.
*   **T5 (Text-to-Text Transfer Transformer):** Encoder-Decoder. Frames all NLP tasks as text-to-text (e.g., "translate English to French: Hello" $\rightarrow$ "Bonjour").

**3. Large Language Models (LLMs)**
*   **GPT-3/4:** Massive parameter models. GPT-4 is multimodal (accepts images/text). Exhibits few-shot/zero-shot learning.
*   **Gemini:** Google's multimodal model (natively handles text, images, audio, video).
*   **LLaMA:** Meta's open-weight models designed to be highly efficient (smaller parameter counts but trained on more tokens).

**4. Fine-tuning and Prompt Engineering**
*   **Prompt Engineering Techniques:**
    *   *Zero-shot:* No examples given.
    *   *Few-shot:* Providing examples in the prompt.
    *   *Chain-of-Thought (CoT):* Prompting the model to "think step-by-step."
    *   *System Prompting:* Defining the persona/rules of the AI.
*   **Fine-Tuning Methods:**
    *   *Transfer Learning:* Taking a pre-trained model and updating all weights on a specific dataset.
    *   *LoRA (Low-Rank Adaptation):* Freezes pre-trained weights and injects small, trainable rank-decomposition matrices. Highly efficient.
    *   *QLoRA:* Quantized LoRA. Further reduces memory by loading the frozen model in 4-bit precision, while training the LoRA adapters in higher precision.

**5. Creating and Using Embeddings**
*   **Concept:** Dense vector representations of text that capture semantic meaning.
*   **Usage:** Used in search, RAG, clustering, and as the input layer for Transformers.

**6. Hands-on Experimentation with Open-Source LLMs**
*   Utilizing Hugging Face `transformers` library: loading tokenizers, loading models (`AutoModelForCausalLM`), generating text using `pipeline` or `model.generate()`.

---

### **Possible Questions for Course Outcome 4**
**Remembering:**
1. State the mathematical formula for Scaled Dot-Product Attention.
2. What is the difference between BERT and GPT architectures?
3. Define LoRA and QLoRA.

**Understanding:**
4. Explain the role of Query, Key, and Value matrices in the self-attention mechanism.
5. How does the T5 model unify different NLP tasks?
6. Differentiate between few-shot prompting and chain-of-thought prompting.
7. Explain how QLoRA reduces memory requirements during fine-tuning.

**Applying:**
8. Write Python code using the Hugging Face library to load a GPT-2 model and generate text from a prompt.
9. Design a prompt strategy to get an LLM to solve a complex math problem accurately.
10. How would you use embeddings to build a semantic search engine?

**Analyzing:**
11. Compare Encoder-only (BERT) vs. Decoder-only (GPT) models regarding their suitability for generation vs. classification.
12. Analyze the trade-offs between full fine-tuning, LoRA, and QLoRA in terms of compute power vs. accuracy.

**Evaluating:**
13. Evaluate the effectiveness of Chain-of-Thought prompting vs. standard few-shot prompting on logical reasoning tasks.
14. If you have limited GPU memory (8GB VRAM), evaluate which LLM fine-tuning strategy you must use and justify your choice.

---

## **Unit V: Multimodal Generative Models**
**Course Objective:** Analyze AI techniques for generating images, videos, and cross-domain media.
**Course Outcome 5:** Work with multimodal generative models to create AI-generated images, videos, and speech.

### **Detailed Theoretical Preparation Notes**

**1. Introduction to Multimodal Learning**
*   **Concept:** AI systems that can process, understand, and generate data across multiple modalities (text, image, audio, video) simultaneously. Aligns different data types into a shared latent space.

**2. Image Generation: Diffusion Models**
*   **Concept:** Generate data by reversing a gradual noising process.
    1.  *Forward Process:* Add Gaussian noise to an image step-by-step until it is pure noise.
    2.  *Reverse Process:* Train a neural network (usually a U-Net) to predict and subtract the noise at each step, eventually revealing a new image.
*   **DALL·E:** Uses a two-stage approach (generates a prior/image embedding from text, then a decoder generates the image). DALL·E 2/3 heavily utilize diffusion for the decoder.
*   **Stable Diffusion (Latent Diffusion):** Performs the diffusion process in a lower-dimensional "latent space" rather than pixel space, making it highly efficient and runnable on consumer GPUs.
*   **MidJourney:** A proprietary model known for highly stylized, artistic, and aesthetically pleasing image generation.

**3. Text-to-Video and Speech Generation Models**
*   **Text-to-Video (Sora, Runway Gen-2):** Extends latent diffusion to the temporal dimension. Challenges include maintaining spatial-temporal consistency (objects disappearing between frames).
*   **Text-to-Speech (TTS):** Models like Tacotron 2 (sequence-to-sequence with attention) or modern diffusion-based TTS. Converts text to mel-spectrograms, then to audio waveforms via vocoders.

**4. Cross-Domain Generative AI Applications**
*   **Image-to-Text:** Image captioning (e.g., BLIP).
*   **Text-to-Music:** MusicLM, Suno.
*   **Audio-to-Image:** Generating visual art based on sound/speech input.

**5. Ethical Concerns in AI-Generated Media**
*   **Deepfakes:** Non-consensual use of likeness, political misinformation.
*   **Copyright Infringement:** Scraping artists' work without compensation to train models like Stable Diffusion.
*   **Authentication:** The need for watermarking (e.g., Content Credentials) to identify AI content.

**6. Agentic AI**
*   **A2A (Agent-to-Agent Communication):** Multiple AI agents interacting, negotiating, and collaborating to solve complex tasks (e.g., an "Engineer Agent" writing code and a "QA Agent" testing it).
*   **MCP (Model Context Protocol):** An open standard introduced by Anthropic to provide a standardized way for AI models to connect to external data sources and tools securely.
*   **ACP (Agent Communication Protocol):** Frameworks/protocols enabling agents to share state, messages, and goals (e.g., AutoGen, LangGraph).

---

### **Possible Questions for Course Outcome 5**
**Remembering:**
1. What are the two main steps in a Diffusion Model?
2. Name three popular text-to-image diffusion models.
3. What does A2A stand for in the context of Agentic AI?
4. What is the purpose of MCP (Model Context Protocol)?

**Understanding:**
5. Explain how Latent Diffusion Models (like Stable Diffusion) differ from standard Diffusion Models to save computational cost.
6. Describe the primary challenges in generating video from text compared to generating static images.
7. How does Tacotron 2 convert text to speech?
8. Explain the concept of Cross-Domain Generative AI.

**Applying:**
9. How would you implement a workflow where an AI agent creates an image, another agent critiques it, and a third agent refines the prompt? (Using A2A concepts).
10. Suggest a method to add a watermark to AI-generated audio.

**Analyzing:**
11. Compare the artistic outputs and target use cases of MidJourney vs. Stable Diffusion.
12. Analyze the ethical concerns surrounding open-source diffusion models like Stable Diffusion compared to closed APIs like DALL·E.

**Evaluating:**
13. Evaluate the impact of Agentic AI (A2A, MCP) on enterprise automation. What are the security risks?
14. "Deepfake technology should be banned entirely." Evaluate this statement considering both societal harm and technological innovation.

---

## **Unit VI: Industry Applications and Future Trends in Generative AI**
**Course Objective:** *Implicitly mapped to CO6 - Analyze AI techniques / Evaluate ethical considerations, security risks, and emerging trends.*
**Course Outcome 6:** Evaluate ethical considerations, security risks, and emerging trends in Generative AI.

### **Detailed Theoretical Preparation Notes**

**1. Generative AI in Healthcare, Finance, and Education**
*   **Healthcare:** Drug discovery (generating molecular structures), synthetic patient data for trials, medical image enhancement.
*   **Finance:** Synthetic financial data for stress testing without violating privacy, algorithmic trading signal generation, automated report generation.
*   **Education:** Personalized tutoring bots, automated curriculum generation, grading feedback.

**2. AI for Creativity: Music, Art, and Game Design**
*   **Music:** Generating melodies, stems, or full tracks (e.g., Suno, Udio). Assisting composers with writer's block.
*   **Art:** Concept art generation, texture generation for 3D models.
*   **Game Design:** Procedural content generation (creating levels, NPCs, dialogue trees), dynamic storytelling.

**3. Explainability and Interpretability of Generative AI Models**
*   **The Black Box Problem:** LLMs and Diffusion models are massive; it is hard to know *why* they generated a specific output.
*   **Techniques:** Probing latent spaces, attention visualization (seeing which words an LLM focused on), mechanistic interpretability (understanding individual neurons/circuits).
*   **Importance:** Crucial for high-stakes domains (medicine, law) to ensure trust and compliance.

**4. Challenges, Security, and Adversarial Attacks on Generative Models**
*   **Adversarial Prompts (Prompt Injection):** Tricking an LLM into bypassing its safety guardrails (e.g., "Ignore previous instructions...").
*   **Data Poisoning:** Maliciously altering training data to make the model output incorrect or biased information.
*   **Model Extraction/Stealing:** Replicating a proprietary model by querying it extensively and training a smaller model on the query-response pairs.
*   **Hallucinations:** Models confidently generating factually incorrect information.

**5. Future Trends: AGI, AI Regulation, and Responsible AI**
*   **AGI (Artificial General Intelligence):** The theoretical point where AI can perform any intellectual task a human can. Debate over timelines and safety (Alignment problem).
*   **AI Regulation:** Laws emerging globally (e.g., EU AI Act, US Executive Orders). Focus on transparency, copyright, and risk-tier classification.
*   **Responsible AI:** Principles of fairness, accountability, robustness, and transparency (FART/AORT). Implementing guardrails, RLHF (Reinforcement Learning from Human Feedback), and red-teaming.

---

### **Possible Questions for Course Outcome 6**
**Remembering:**
1. Define "Prompt Injection" in the context of LLM security.
2. What is AGI?
3. List three applications of GenAI in Finance.
4. What is the "Black Box" problem in AI?

**Understanding:**
5. Explain how Generative AI aids in Drug Discovery in Healthcare.
6. Describe the concept of "Data Poisoning" and its effect on generative models.
7. How does Reinforcement Learning from Human Feedback (RLHF) contribute to Responsible AI?
8. Explain the importance of mechanistic interpretability in LLMs.

**Applying:**
9. How would you design a security protocol to prevent prompt injection attacks in a customer-facing chatbot?
10. Suggest ways a game development studio can use GenAI to speed up level design.

**Analyzing:**
11. Analyze the difference between hallucinations in LLMs and mode collapse in GANs.
12. Compare the regulatory approaches of the EU AI Act (risk-based) vs. a hands-off approach. What are the pros and cons of each?

**Evaluating:**
13. Evaluate the ethical dilemma of using Generative AI to write academic papers. Propose a framework for responsible use.
14. "The pursuit of AGI poses an existential threat to humanity." Critically evaluate this statement based on current AI trends, security risks, and alignment research.
15. Assess the impact of Generative AI on job displacement in the creative industries (Music/Art). What mitigation strategies should society adopt?