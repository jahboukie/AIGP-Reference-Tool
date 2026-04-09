# Glossary

*Last reviewed: April 2026*

Terms are grouped by domain. Within each domain, entries are alphabetical.

---

## Neural Network Fundamentals

**Activation Function**
A non-linear function applied to the output of each neuron. Introduces the non-linearity that allows neural networks to model complex patterns. Common activations: ReLU, sigmoid, tanh, GELU, SiLU/Swish.

**Backpropagation**
The algorithm used to compute gradients of the loss function with respect to each weight in the network. Applies the chain rule of calculus layer by layer from output to input, enabling gradient descent to update weights.

**Batch Size**
The number of training examples processed together in one forward/backward pass. Larger batches provide more stable gradient estimates but require more memory. Common practice: 32 to 4096 for language models.

**Epoch**
One complete pass through the entire training dataset. Language model training is often measured in tokens processed rather than epochs, since datasets may be seen fewer than once.

**Gradient Descent**
An optimisation algorithm that iteratively adjusts weights in the direction that reduces the loss function. Variants: stochastic gradient descent (SGD), Adam, AdamW.

**Hidden Layer**
Any layer in a neural network between the input and output layers. "Deep" learning uses multiple hidden layers.

**Hyperparameter**
A configuration value set before training begins and not learned from data. Examples: learning rate, batch size, number of layers, dropout rate.

**Loss Function**
A mathematical function that measures how far the model's predictions are from the desired output. Training minimises this function. Cross-entropy loss is standard for language models.

**Neuron (Node)**
The basic computational unit of a neural network. Computes a weighted sum of inputs, adds a bias, and applies an activation function.

**Overfitting**
When a model learns patterns specific to the training data that do not generalise to new data. Detected when training performance exceeds validation performance.

**Parameter**
A value learned during training. In neural networks: weights and biases. A model's parameter count is the total number of learnable values. GPT-3: 175 billion parameters.

**Regularisation**
Techniques to prevent overfitting: dropout, weight decay (L2 regularisation), early stopping, data augmentation.

**Tensor**
A multi-dimensional array of numbers — the fundamental data structure in deep learning. A scalar is a 0-dimensional tensor, a vector is 1D, a matrix is 2D.

**Weight**
A learnable parameter that determines the strength of connection between neurons. Weights are adjusted during training to minimise the loss function.

---

## Transformer Architecture

**Attention Mechanism**
A mechanism that allows each token in a sequence to attend to (calculate relevance scores for) every other token. Computes: Attention(Q,K,V) = softmax(QK^T / √d_k)V.

**Cross-Attention**
Attention where queries come from one sequence and keys/values come from another. Used in encoder-decoder models (e.g., machine translation).

**Decoder**
The component that generates output tokens autoregressively, one at a time. Uses masked self-attention (can only attend to previous tokens). GPT-family models use decoder-only architecture.

**Embedding**
A learned vector representation of a discrete token. Maps tokens from a vocabulary (e.g., 100,000 words/subwords) to dense vectors (e.g., 4096 dimensions).

**Encoder**
The component that processes an entire input sequence bidirectionally. BERT-family models use encoder-only architecture. Can attend to all tokens in both directions.

**Feed-Forward Network (FFN)**
A two-layer fully connected network applied to each position independently within a transformer block. Typically expands dimensionality (e.g., 4x), applies activation, then projects back down.

**Key (K)**
In attention, the key vector represents what information a token has available for other tokens to attend to. Computed from the token's representation via a learned linear projection.

**Layer Normalisation (LayerNorm)**
Normalises activations across the feature dimension (not the batch dimension). Stabilises training. Applied before (pre-norm) or after (post-norm) attention and FFN sub-layers.

**Multi-Head Attention (MHA)**
Running multiple attention operations in parallel, each with its own Q/K/V projections (a "head"). Allows the model to attend to different types of relationships simultaneously. GPT-3 uses 96 attention heads.

**Positional Encoding / Positional Embedding**
Information about token position in the sequence, since attention itself is position-agnostic. Approaches: sinusoidal (original transformer), learned absolute, RoPE (rotary), ALiBi.

**Query (Q)**
In attention, the query vector represents what information a token is looking for. Computed from the token's representation via a learned linear projection.

**Residual Connection (Skip Connection)**
Adding the input of a sub-layer directly to its output: output = sublayer(x) + x. Enables training of very deep networks by allowing gradients to flow unchanged through layers.

**Self-Attention**
Attention where queries, keys, and values all come from the same sequence. Each token computes relevance scores for every other token in the same input.

**Softmax**
A function that converts a vector of raw scores into a probability distribution (values between 0 and 1 that sum to 1). Used in attention score normalisation and output token prediction.

**Tokeniser / Tokenizer**
Converts raw text into a sequence of token IDs. Common algorithms: Byte Pair Encoding (BPE), WordPiece, SentencePiece, Unigram. Vocabulary sizes typically 32K–100K tokens.

**Transformer Block**
One complete layer of a transformer, containing: self-attention → residual connection → layer norm → FFN → residual connection → layer norm. A model stacks many blocks (GPT-3: 96 blocks).

**Value (V)**
In attention, the value vector represents the actual information a token contributes when attended to. Computed from the token's representation via a learned linear projection.

---

## Large Language Models

**Alignment**
The process of making a model's outputs consistent with human values, intentions, and preferences. Techniques: RLHF, DPO, Constitutional AI, RLAIF.

**Autoregressive Generation**
Generating text one token at a time, where each new token is conditioned on all previous tokens. The standard generation method for GPT-family models.

**Chain-of-Thought (CoT)**
A prompting technique where the model is encouraged to show intermediate reasoning steps before giving a final answer. Improves performance on complex reasoning tasks.

**Constitutional AI (CAI)**
An alignment technique (Anthropic, 2022) where the model is trained to follow a set of principles ("constitution") and critique/revise its own outputs against those principles.

**Context Window**
The maximum number of tokens a model can process in a single forward pass. Determines how much text the model can "see" at once. Examples: GPT-4 Turbo: 128K tokens, Claude 3: 200K tokens.

**Direct Preference Optimisation (DPO)**
An alignment technique that optimises the model directly from preference data without training a separate reward model. Simpler alternative to RLHF.

**Few-Shot Learning**
Providing a small number of examples in the prompt to guide model behavior, without updating model weights. Also called in-context learning.

**Fine-Tuning**
Continuing to train a pre-trained model on a smaller, task-specific dataset. Updates model weights. Distinguished from prompting (which does not update weights).

**Foundation Model**
A large model trained on broad data that can be adapted to a wide range of downstream tasks. The term encompasses large language models but also multimodal models and other architectures.

**Hallucination**
When a model generates text that is fluent and confident but factually incorrect, fabricated, or unsupported by its training data. A fundamental unsolved challenge.

**In-Context Learning (ICL)**
The ability of large language models to learn from examples provided in the prompt, without weight updates. Emerges as a capability at sufficient scale.

**Inference**
Using a trained model to generate predictions or outputs on new inputs. Distinguished from training (which updates model weights). Inference cost is typically much lower than training cost.

**Mixture of Experts (MoE)**
An architecture where the model has multiple specialised sub-networks ("experts") and a routing mechanism that selects which experts to activate for each input. Allows very large total parameter counts while keeping per-input compute manageable.

**Perplexity**
A metric measuring how well a language model predicts a sample of text. Lower perplexity = better prediction. Defined as 2^(cross-entropy loss). Used as a training metric, not a downstream task metric.

**Pre-Training**
The initial training phase where a model learns from a very large, general-purpose corpus using self-supervised objectives (e.g., next-token prediction). The most compute-intensive phase.

**Prompt Engineering**
Designing and optimising the text input (prompt) to elicit desired model behavior. Techniques: system prompts, few-shot examples, chain-of-thought, role-playing.

**Quantisation / Quantization**
Reducing model weight precision from higher bit-widths (e.g., FP32, FP16) to lower ones (INT8, INT4). Reduces memory and compute requirements at the cost of some accuracy.

**Reinforcement Learning from Human Feedback (RLHF)**
An alignment technique where: (1) humans rank model outputs by preference, (2) a reward model is trained on those rankings, (3) the language model is optimised to maximise the reward model's score using reinforcement learning (PPO).

**Retrieval-Augmented Generation (RAG)**
Combining a language model with an external knowledge retrieval system. The model's prompt is augmented with relevant documents retrieved from a knowledge base, reducing hallucination for factual queries.

**System Prompt**
Instructions provided to the model that set behavior, persona, and constraints for a conversation. Not visible to the end user in most deployments. Forms the first layer of the guardrail stack.

**Temperature**
A sampling parameter controlling randomness in token selection. Temperature 0 = deterministic (always pick the highest-probability token). Temperature > 1 = more random. Typical range: 0.0–1.5.

**Top-k Sampling**
A sampling strategy that restricts token selection to the k highest-probability tokens. Reduces the chance of unlikely/nonsensical outputs.

**Top-p (Nucleus) Sampling**
A sampling strategy that restricts token selection to the smallest set of tokens whose cumulative probability exceeds p. More adaptive than top-k.

**Zero-Shot Learning**
Using a model on a task without providing any examples — relying entirely on the model's pre-training knowledge and the task description in the prompt.

---

## AI Governance and Regulation

**AI System (EU AI Act)**
"A machine-based system that is designed to operate with varying levels of autonomy and that may exhibit adaptiveness after deployment and that, for explicit or implicit objectives, infers, from the input it receives, how to generate outputs such as predictions, content, recommendations, or decisions that can influence physical or virtual environments" — Article 3(1).

**Alignment (Governance Context)**
Ensuring AI system behavior is consistent with the values, goals, and ethical principles of the deploying organisation and the communities affected by the system.

**Bias (Algorithmic)**
Systematic and repeatable errors in an AI system's output that create unfair outcomes. Can originate from training data (data bias), model design (algorithmic bias), or user interpretation (interaction bias).

**CE Marking**
A marking indicating that a product conforms with EU health, safety, and environmental protection standards. Required for high-risk AI systems under the EU AI Act before market placement.

**Conformity Assessment**
The process by which a provider demonstrates that a high-risk AI system meets the requirements of the EU AI Act. May be self-assessed (internal control, Annex VI) or require third-party assessment (Annex VII) depending on the system type.

**Deployer (EU AI Act)**
"A natural or legal person, public authority, agency or other body using an AI system under its authority" — Article 3(4). The entity that puts the AI system to use in a real-world context.

**FLOP (Floating Point Operation)**
A single arithmetic operation on floating-point numbers. Training compute is measured in total FLOPs. The EU AI Act's GPAI systemic risk threshold is 10^25 FLOPs.

**Fundamental Rights Impact Assessment (FRIA)**
Required under EU AI Act Article 27 for deployers of high-risk AI systems. Assesses impacts on fundamental rights including non-discrimination, privacy, freedom of expression, and human dignity.

**General-Purpose AI (GPAI) Model**
"An AI model, including where such an AI model is trained with a large amount of data using self-supervision at scale, that displays significant generality and is capable of competently performing a wide range of distinct tasks" — Article 3(63).

**Guardrails**
Technical safety mechanisms that constrain AI system behavior. Includes input filtering, output classification, content policy enforcement, and system prompt instructions. Operates as defence in depth — multiple layers of control.

**High-Risk AI System (EU AI Act)**
An AI system that falls within one of the categories listed in Annex III (biometric identification, critical infrastructure, education, employment, essential services, law enforcement, migration, justice) or is a safety component of a product requiring conformity assessment (Annex I).

**Model Card**
A structured document describing a machine learning model's intended use, performance characteristics, training data, evaluation results, ethical considerations, and limitations. Originated from Mitchell et al. (2019).

**Provider (EU AI Act)**
"A natural or legal person, public authority, agency or other body that develops an AI system or a general-purpose AI model or that has an AI system or a general-purpose AI model developed and places it on the market or puts the AI system into service under its own name or trademark" — Article 3(3).

**Red Teaming (AI)**
Structured adversarial testing of an AI system by a dedicated team attempting to elicit harmful, unsafe, or unintended behavior. Tests jailbreaks, prompt injection, harmful content generation, data extraction, and policy circumvention.

**Risk Management System (EU AI Act)**
A continuous, iterative process required under Article 9 for high-risk AI systems. Must identify, analyse, evaluate, and manage risks throughout the entire lifecycle of the AI system.

**Statement of Applicability (SoA)**
A document required for ISO 42001 certification listing all Annex A controls, declaring which are applicable, and justifying any exclusions. The cornerstone of an ISO 42001 audit.

**Substantial Modification (EU AI Act)**
A change to an AI system after market placement that was not foreseen by the provider and that affects compliance with requirements or changes the intended purpose. Triggers re-assessment obligations.

**Systemic Risk (EU AI Act)**
Risk at scale from GPAI models with high impact capabilities. Presumed when training compute exceeds 10^25 FLOPs. Triggers additional obligations under Article 55.

**Trustworthiness (NIST AI RMF)**
The composite quality of an AI system across seven characteristics: valid and reliable, safe, secure and resilient, accountable and transparent, explainable and interpretable, privacy-enhanced, and fair with harmful bias managed.

---

## Data and Evaluation

**Benchmark**
A standardised test or suite of tests used to evaluate model performance. Examples: MMLU (knowledge), HumanEval (code), MT-Bench (conversation), TruthfulQA (factual accuracy).

**Common Crawl**
A non-profit that crawls the web and makes the data freely available. Source of the majority of text used in large language model pre-training. Contains billions of web pages.

**Data Contamination**
When information from a benchmark's test set appears in a model's training data. Inflates benchmark scores without reflecting genuine capability. A growing concern as training datasets scale.

**Data Sheet (Datasheet for Datasets)**
A structured document describing a dataset's motivation, composition, collection process, recommended uses, and maintenance plan. Originated from Gebru et al. (2021).

**Demographic Parity**
A fairness metric requiring that the positive prediction rate be equal across demographic groups. Also called statistical parity. One of several conflicting mathematical definitions of fairness.

**Equalized Odds**
A fairness metric requiring equal true positive rates and false positive rates across demographic groups. Provides stronger guarantees than demographic parity but is harder to achieve.

**F1 Score**
The harmonic mean of precision and recall. Ranges from 0 to 1. Useful when both false positives and false negatives matter.

**HELM (Holistic Evaluation of Language Models)**
A comprehensive benchmark framework from Stanford CRFM evaluating language models across scenarios, metrics, and multiple trustworthiness dimensions including accuracy, calibration, robustness, fairness, bias, toxicity, and efficiency.

**MMLU (Massive Multitask Language Understanding)**
A benchmark testing knowledge across 57 academic subjects from STEM to humanities. Multiple-choice format. Widely cited as a general knowledge measure.

**Precision**
Of all positive predictions, the fraction that are correct. Precision = True Positives / (True Positives + False Positives).

**Recall**
Of all actual positives, the fraction that are correctly identified. Recall = True Positives / (True Positives + False Negatives).

**The Pile**
An 825 GB English text dataset created by EleutherAI for language model training. Combines 22 diverse sources including academic papers, books, Wikipedia, GitHub code, and web text.
