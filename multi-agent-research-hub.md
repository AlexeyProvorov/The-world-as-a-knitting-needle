Useful thoughts and experience about the MAS developing 
# Must have

https://arxiv.org/pdf/2510.26745v1
<details>
  <summary>Deep Sequence Models Tend to Memorize Geometrically; It Is Unclear Why – October 30, 2025</summary>

**Tags:** Deep Learning, Transformers, Parametric Memory, Representation Learning, Spectral Bias

This paper argues that large sequence models (Transformers, Mamba, simple neural nets) don’t just store atomic facts as a brute-force associative table, but instead **spontaneously organize them into a global geometric structure in embedding space**. This is demonstrated on specially constructed path-finding tasks over graphs, where:

- The authors contrast two kinds of parametric memory:  
  - **Associative memory**, where each co-occurrence is stored as a local entry in a weight matrix over otherwise arbitrary token embeddings.  
  - **Geometric memory**, where the embeddings themselves encode global graph structure, so that dot products reflect multi-hop proximity even between nodes that never co-occurred during training.  

- They design an **in-weights path-star task**: the model first memorizes all edges of a large tree-like graph (tens of thousands of nodes), then must output the full path from root to a given leaf purely from its stored weights. In this setup, both Transformer and Mamba achieve near-perfect generalization to unseen leaves, even though analogous **in-context** versions of the same graph task are known to fail under next-token training.

- Analyzing token-wise learning, they show that the **hardest token—the first step on the path—is learned in isolation**, without intermediate supervision or chain-of-thought signals. Under a purely associative-memory view, this requires learning an ℓ-fold composition of lookups, which should be computationally intractable to learn by gradient descent. The success of the models therefore implies that they implicitly reduce this multi-step reasoning task to a **single geometric step**.

- By visualizing embeddings and cosine-distance heatmaps, they show that nodes belonging to the same path form tight clusters and that leaf/first-node pairs are especially aligned—evidence that the model has constructed a **global geometric map of the graph** rather than a local lookup table.

- The authors then challenge standard explanations:  
  - **Capacity/regularization** cannot be the main driver, because for certain graphs geometric and associative representations are shown to be **equally or almost equally succinct** in terms of bits and parameter norms.  
  - **Supervisory pressure** also fails to explain the effect, since similar global geometries emerge even when training only on local edge prediction (no explicit path-finding supervision), and geometry appears for unseen paths as well.

- To probe the origin of this geometric bias, they analyze a simpler Node2Vec-style model (1-layer, 1-hop, cross-entropy loss). They find that training dynamics naturally exhibit a **spectral bias**: embeddings converge to span the top eigenvectors (Fiedler-like vectors) of the graph Laplacian, while the effective update matrix develops those same eigenvectors in its null space. This happens **without** low-rank constraints, early stopping, or explicit multi-hop objectives, suggesting that gradient descent alone can induce **global, spectrally-organized geometries from purely local training signals**.

**Main conclusion:**  
Deep sequence models, when trained even on collections of “incompressible” atomic facts, tend to synthesize **geometric world models** in their embedding spaces rather than simple associative tables. This geometry collapses hard multi-hop reasoning into easy one-step vector computations, yet cannot be fully explained by standard notions of capacity, regularization, or supervision. Understanding and amplifying this naturally arising spectral/geometric bias could lead to models with more powerful implicit reasoning and combinatorial creativity, but also raises challenges for precise knowledge editing, unlearning, and controllable retrieval.
</details>


https://arxiv.org/pdf/2508.10146
<details>
  <summary>Agentic AI Frameworks: Architectures, Protocols, and Design Challenges – August 2025</summary>

**Tags:** Agentic AI, Multi-Agent Systems, Communication Protocols, Service-Oriented Architecture, LLM Frameworks

This paper provides a comprehensive survey of **Agentic AI**—LLM-powered autonomous agents that plan, reason, collaborate, and adapt in open environments. The contributions include:
- Tracing the **evolution of agents** from classical BDI models to modern LLM-driven entities with integrated memory, tool use, and dynamic coordination.  
- Systematically comparing **frameworks** (AutoGen, CrewAI, MetaGPT, LangGraph, Semantic Kernel, Agno, Google ADK, LlamaIndex) on memory design, orchestration, guardrails, and scalability.  
- Analyzing emerging **communication protocols** (MCP, A2A, ANP, ACP, Agora), highlighting advances in interoperability but also fragmentation and the lack of standardized service contracts.  
- Positioning Agentic AI within the lens of **service-oriented computing** (WSDL, BPEL, WS-Policy, WS-Agreement), arguing for contracts, discovery, and composition mechanisms to enable “Agent-as-a-Service.”  
- Identifying key **challenges**: rigid roles, missing runtime discovery, insecure code execution, fragmented abstractions, and the absence of standardized benchmarks.  

**Main conclusion:**  
Agentic AI is the natural successor to LLMs, shifting toward scalable ecosystems of collaborating agents. The field urgently needs **unified protocols, memory standards, modular guardrails, and interoperability layers** akin to those that matured web services. Without these, agent frameworks remain siloed and fragile; with them, they can underpin the next generation of adaptive, service-oriented intelligent systems.  
</details>

https://arxiv.org/pdf/2508.06659
<details>
  <summary>In-Context Reinforcement Learning via Communicative World Models – August 8, 2025</summary>

**Tags:** Reinforcement Learning, In-Context Learning, World Models, Emergent Communication, Zero-Shot Adaptation, Sample Efficiency

This paper introduces **CORAL** (Communicative Representation for Adaptive RL), a framework that decouples world model learning from policy learning by structuring in-context reinforcement learning as a two-agent communication problem:
- An **Information Agent (IA)**, implemented as a Transformer, is pre-trained to model environment dynamics and rewards, producing concise latent **messages** without directly optimizing for task reward.
- A **Control Agent (CA)** uses both observations and IA messages to select actions, with its policy optimized solely for task reward.
- IA training combines **Dynamics Awareness**, **Temporal Coherence**, and a novel **Causal Influence Loss** to ensure messages meaningfully guide CA's policy.

Key contributions include:
- **Functional separation** of representation learning (IA) and control (CA) for better generalization.
- **Emergent communicative prior** enabling faster adaptation in unseen sparse-reward environments.
- **Multi-task pretraining** across diverse environments to avoid overfitting.
- Empirical validation showing **1.5–5× faster learning** and superior zero-shot performance compared to PPO and conventional world models.

**Main conclusion:**  
CORAL demonstrates that pre-trained communicative world models can act as powerful contextual priors, accelerating learning and improving generalization in challenging RL settings. By leveraging communication as a structured transfer of environment understanding, the method provides a scalable path toward adaptive, generalist agents—though future work should test in more complex domains, explore structured message formats, and consider communication cost models.
</details>

https://arxiv.org/pdf/2503.09501
<details>
  <summary>ReMA: Learning to Meta-think for LLMs with Multi-agent Reinforcement Learning – May 27, 2025</summary>

**Tags:** Large Language Models, Meta-thinking, Multi-agent Systems, Reinforcement Learning, Out-of-distribution Generalization, Mathematical Reasoning

This paper introduces **ReMA**, a framework that trains LLMs to “think about thinking” by splitting reasoning into two cooperating agents:
- A **high-level meta-thinking agent** that plans, monitors, and adjusts reasoning strategies.
- A **low-level reasoning agent** that executes detailed problem-solving under strategic guidance.

Using **multi-agent reinforcement learning (MARL)** with aligned rewards, ReMA improves exploration efficiency, interpretability, and performance, especially on out-of-distribution (OOD) tasks. The method supports both **single-turn** and **multi-turn** meta-reasoning, with innovations like:
- **Turn-level ratio clipping** to stabilize multi-turn RL and prevent degenerate outputs.
- **Parameter sharing** for efficiency without sacrificing coordination quality.

**Key results:**
- On math reasoning benchmarks, ReMA yields up to **+20% accuracy gains** over baselines (AMC23, Llama3-8B) and strong improvements on challenging OOD datasets (e.g., AIME24: +13.33% for Qwen2.5-7B).
- On LLM-as-a-Judge tasks, ReMA improves generalization, achieving **+14.23%** over CoT baselines on RewardBench970.
- Ablations show that meta-thinking boosts low-level generalization, larger LMs adopt richer strategies, and multi-turn setups benefit from parameter sharing.

**Main conclusion:**  
By explicitly separating strategic oversight and execution in LLM reasoning, ReMA achieves superior accuracy and robustness, offering a scalable pathway for building systems that adapt their problem-solving dynamically while maintaining clarity and control over reasoning steps.
</details>

https://cognition.ai/blog/dont-build-multi-agents#principles-of-context-engineering 
<details>
  <summary>Don’t Build Multi-Agents – June 12, 2025</summary>

**Tags:** LLM Agents, Context Engineering, Reliability

The article argues that chaining multiple LLM subagents in parallel is fragile because context and implicit decisions get siloed, leading to compounding errors. Instead, it introduces **Context Engineering**—sharing the full trace of prior actions and recognizing that every action carries hidden assumptions—and advocates for a **single-threaded linear agent**, optionally augmented with a **history-compressor** to summarize long interactions :contentReference[oaicite:0]{index=0}.

**Main conclusion:**  
For robust, long-running AI agents, avoid parallel multi-agent setups and focus on seamless context management—either via one coherent agent or by intelligently compressing history—so that every decision is consistently informed by the complete task context. :contentReference[oaicite:1]{index=1}
</details>

https://www.anthropic.com/engineering/built-multi-agent-research-system
<details>
  <summary>How we built our multi-agent research system – June 13, 2025</summary>

**Tags:** Multi-Agent Systems, Orchestration, Research, Prompt Engineering

This article describes how Anthropic built its Research feature using a lead Claude agent to orchestrate multiple parallel subagents for open-ended research tasks. It covers challenges around orchestration patterns, prompt and tool design, evaluation frameworks, and operational practices, illustrating how careful multi-agent engineering can accelerate research workflows while managing reliability and coordination complexities. :contentReference[oaicite:2]{index=2}

**Main conclusion:**  
With robust orchestration patterns, prompt strategies, evaluation methods, and fault-recovery practices, production-grade multi-agent systems can dramatically enhance complex research tasks—but the gap between prototype and reliable production demands meticulous engineering around tooling, evaluation, and deployment. :contentReference[oaicite:3]{index=3}
</details>


https://arxiv.org/abs/2507.11988 
<details>
  <summary>Aime: Towards Fully-Autonomous Multi-Agent Framework – July 17, 2025</summary>

**Tags:** Multi-Agent Systems, Dynamic Planning, Actor Factory, Progress Management

This paper introduces **Aime**, a novel multi-agent framework that overcomes the limitations of the static plan‑and‑execute paradigm by:
- Employing a **Dynamic Planner** that continuously refines strategy based on real‑time execution feedback.  
- Utilizing an **Actor Factory** to instantiate specialized agents on‑demand, each equipped with tailored tools and knowledge.  
- Maintaining a **Progress Management Module** as a single source of truth for coherent, system‑wide state awareness.  
The framework replaces rigid, precomputed workflows with a fluid, adaptive architecture and is evaluated on GAIA, SWE‑bench Verified, and WebVoyager benchmarks, where it consistently outperforms highly specialized state‑of‑the‑art agents :contentReference[oaicite:3]{index=3}.

**Main conclusion:**  
Aime significantly outperforms conventional multi‑agent systems—achieving new state‑of‑the‑art success rates of 77.6% on GAIA, 66.4% on SWE‑bench Verified, and 92.3% on WebVoyager—demonstrating superior adaptability, efficiency, and overall task success in dynamic environments :contentReference[oaicite:4]{index=4}.
</details>


## RAG, Graphs, Fine-tuning, 


https://arxiv.org/pdf/2401.15884 + [Сode on Google Colab](https://colab.research.google.com/github/lancedb/vectordb-recipes/blob/main/tutorials/Corrective-RAG-with_Langgraph/CRAG_with_Langgraph.ipynb#scrollTo=gUlaOeBxpIxD)
<details>
  <summary>Corrective Retrieval Augmented Generation (CRAG) – October 7, 2024</summary>

**Tags:** Large Language Models, Retrieval-Augmented Generation, Hallucination Mitigation, Web Search, Knowledge Refinement

This paper introduces **CRAG**, a corrective framework for RAG systems that strengthens robustness against irrelevant or misleading retrieval results by:
- Designing a **lightweight retrieval evaluator** (T5-based) that scores document relevance and triggers corrective actions: **Correct**, **Incorrect**, or **Ambiguous**.  
- Employing a **decompose–filter–recompose algorithm** to refine retrieved documents into key knowledge fragments, reducing noise and redundancy.  
- Integrating **web search as fallback knowledge**, ensuring the system “knows what it doesn’t know” and avoids hallucinations when internal corpora are insufficient.  
- Demonstrating strong improvements across four benchmarks (PopQA, Biography, PubHealth, ARC-Challenge), with gains up to **+37% FactScore** on long-form biography tasks and substantial robustness over Self-RAG baselines.  

**Main conclusion:**  
CRAG represents a **plug-and-play corrective layer for RAG** that makes LLMs more reliable by filtering noise, correcting faulty retrievals, and selectively enriching knowledge via web search. It marks a step toward self-correcting AI systems that balance generative fluency with factual trustworthiness, though future work is needed to remove reliance on external evaluators and better manage web-source reliability.
</details>

https://arxiv.org/pdf/2501.16214
<details>
  <summary>Provence: efficient and robust context pruning for retrieval-augmented generation – January 2025</summary>

**Tags:** Retrieval-Augmented Generation, Context Pruning, Reranking, Efficiency, Robustness

This paper introduces **Provence**, a lightweight method that unifies reranking and context pruning in retrieval-augmented generation (RAG). Its core contributions include:  
- Formulating pruning as **sequence labeling** at the sentence level, allowing dynamic removal of irrelevant sentences instead of fixed-size cuts.  
- Leveraging **silver labels** from LLaMA-3-8B, which answers questions while citing supporting sentences, enabling large-scale supervised training without costly human annotation.  
- **Merging pruning with reranking**, so the same model both orders passages and prunes them, making the operation nearly cost-free in computation.  
- Demonstrating **robustness**: Provence adapts flexibly (keeping 0–all sentences), works across domains (Wikipedia, biomedical, educational, news), and maintains high quality even at 50–80% context reduction.  
- Achieving **practical efficiency**: up to 1.2–2× faster generation and 20× lower overhead than abstractive pruning methods, while often improving answer quality by filtering noise.  

**Main conclusion:**  
Provence shows that sentence-level pruning, unified with reranking, is a practical and domain-agnostic way to make RAG systems faster, cheaper, and sometimes even more accurate. It stands out as a balanced, real-world-ready solution compared to prior token-level or abstractive pruning methods, though current limitations include single-passage QA focus, English-only training, and weaker performance on edge-position sentences (“needle in a haystack” cases).
</details>

https://arxiv.org/pdf/2505.03275v1
<details>
  <summary>RAG-MCP: Mitigating Prompt Bloat in LLM Tool Selection via Retrieval-Augmented Generation – May 6, 2025</summary>

**Tags:** Large Language Models, Retrieval-Augmented Generation, Model Context Protocol, Tool Selection, Prompt Optimization, AI Agents

This paper introduces **RAG-MCP**, a framework that combines Retrieval-Augmented Generation with the Model Context Protocol to address the challenge of **prompt bloat** when LLMs interact with large toolsets:
- Instead of feeding descriptions of all tools into the prompt, RAG-MCP uses **semantic retrieval** to dynamically select only the most relevant tools for a given query.  
- This reduces prompt size by more than half, alleviates decision complexity, and significantly improves tool selection accuracy.  
- Experiments (including an MCP stress test) show that RAG-MCP **triples accuracy** compared to baseline methods (43.13% vs. 13.62%) while halving prompt token usage.  
- The approach scales easily: new tools can be added to the retriever’s index without retraining the LLM, enabling extensibility and real-time adaptability.  

**Main conclusion:**  
RAG-MCP demonstrates that retrieval-based filtering of tool descriptions is a powerful way to maintain accuracy and efficiency as the number of available APIs grows. It lays a foundation for scalable and reliable LLM agents capable of interfacing with thousands of services, though future work must address retrieval precision at extreme scale and multi-tool workflows.
</details>


Graph-based AI agent
https://arxiv.org/pdf/2410.04660
<details>
  <summary>KGAREVION: An AI Agent for Knowledge‑Intensive Biomedical QA – April 24 – 28, 2025</summary>

**Tags:** Biomedical QA, Knowledge Graph, LLM Verification, Iterative Reasoning

This paper presents **KGAREVION**, a knowledge graph–based AI agent for biomedical question answering that executes a four‑stage pipeline:
- **Generate:** LLM generates candidate medical‑concept triples from the input query.  
- **Review:** A fine‑tuned LLM augmented with KG embeddings verifies the correctness of each triple.  
- **Revise:** The system iteratively corrects or supplements any invalid triples.  
- **Answer:** Final answers are constructed based on the verified, context‑relevant triples. :contentReference[oaicite:4]{index=4}

KGAREVION achieves an average accuracy improvement of **+6.75%** over 15 baseline models across seven medical QA datasets, supports both multiple‑choice and open‑ended formats, demonstrates strong zero‑shot generalization on AfriMed‑QA, and shows resilience to answer‑option perturbations. :contentReference[oaicite:5]{index=5}

**Main conclusion:**  
By integrating LLM hypothesis generation with rigorous KG‑based verification and iterative refinement, KGAREVION significantly enhances the precision and reliability of knowledge‑intensive biomedical QA, paving the way for clinical decision support and advanced biomedical research applications. :contentReference[oaicite:6]{index=6}
</details>


https://arxiv.org/pdf/2404.16130
<details>
  <summary>From Local to Global: A GraphRAG Approach to Query-Focused Summarization – February 2025</summary>

**Tags:** Retrieval-Augmented Generation, Query-Focused Summarization, Knowledge Graphs, LLM Evaluation, Sensemaking

This paper introduces **GraphRAG**, a graph-based RAG method designed for answering **global queries** over large document corpora that exceed the context window of LLMs. The pipeline consists of:

- **Extract:** LLM extracts entities, relationships, and factual claims from text chunks.  
- **Graph Build:** Constructs a knowledge graph with entities as nodes and relationships as edges.  
- **Community Detect:** Applies hierarchical graph clustering (Leiden algorithm) to group related concepts.  
- **Summarize:** Generates summaries at multiple community levels (C0–C3).  
- **Query Answer:** Uses map-reduce over community summaries to answer complex, corpus-wide queries. :contentReference[oaicite:4]{index=4}

GraphRAG **outperforms standard vector RAG** on query-focused summarization tasks by large margins (up to **+33% win rate**) in **comprehensiveness** and **diversity** across podcast and news datasets (~1M tokens each). It also requires **fewer context tokens** than baseline summarization, making it more scalable. :contentReference[oaicite:4]{index=4}

**Main conclusion:**  
By leveraging LLM-derived knowledge graphs and hierarchical summarization, **GraphRAG enables accurate, diverse, and scalable answering of global questions** across large text corpora – a crucial step for deeper AI-powered sensemaking beyond surface-level retrieval. :contentReference[oaicite:4]{index=4}
</details>

https://arxiv.org/pdf/2404.17723
<details>
  <summary>Retrieval-Augmented Generation with Knowledge Graphs for Customer Service Question Answering – July 14, 2024</summary>

**Tags:** Retrieval‑Augmented Generation, Knowledge Graph, Customer Service, Question Answering, Embeddings

This paper presents a novel **Retrieval‑Augmented Generation** approach that leverages a **Knowledge Graph** constructed from historical support tickets to:
- **Preserve ticket structure** by modeling intra‑ticket trees and inter‑ticket links (explicit and embedding‑based), enriching semantic context for retrieval.  
- **Combine KG retrieval with LLM generation**, extracting relevant subgraphs via graph queries and using them as context for answer synthesis.  
- **Validate in production** at LinkedIn, achieving a 77.6 % increase in MRR, a 0.32 BLEU‑point gain, and a 28.6 % reduction in median issue resolution time.

**Main conclusion:**  
Integrating knowledge graphs into RAG pipelines substantially boosts retrieval accuracy and answer quality, resulting in faster and more effective customer support.
</details>

https://arxiv.org/pdf/2306.08302
<details>
  <summary>Unifying Large Language Models and Knowledge Graphs: A Roadmap – July 19, 2025</summary>

**Tags:** Large Language Models, Knowledge Graphs, Retrieval-Augmented Generation, Hybrid Reasoning, Explainability

This paper presents a structured roadmap for bridging LLMs and KGs by:
- Introducing **KG-Enhanced LLMs**, which integrate structured graph facts during pretraining and via retrieval or prompting at inference to improve factual accuracy and reduce hallucinations.  
- Detailing **LLM-Augmented KGs**, leveraging LLMs for embedding, completion, construction, and QA over knowledge graphs to boost coverage and enable natural-language-driven graph creation.  
- Proposing **Synergized LLMs + KGs**, a unified framework where models perform bi-directional reasoning—dynamically retrieving from KGs and traversing graph paths as part of an agent-style inference loop.  

**Main conclusion:**  
By unifying the generative capabilities of LLMs with the precision and interpretability of KGs, the proposed approaches lay the foundation for AI systems that are both highly adaptable and reliably factual, though real-world deployment will require advances in scalable knowledge updates, efficient integration, and robust hallucination detection.
</details>


The Ultimate Guides
https://arxiv.org/pdf/2408.13296
<details>
  <summary>The Ultimate Guide to Fine‑Tuning LLMs – October 2024</summary>

**Tags:** Fine‑Tuning, PEFT, RL, Deployment, Monitoring, Ethics

This report presents a **comprehensive seven‑stage pipeline** for fine‑tuning large language models:
- **Data Preparation**: collection, cleaning, augmentation, handling class imbalance (SMOTE, focal loss).  
- **Model Initialization**: selecting pretrained weights, configuring hyperparameters, environment setup.  
- **Training Setup**: optimizing data throughput, micro‑batching, gradient checkpointing.  
- **Fine‑Tuning Strategies**: full parameter updates vs. PEFT (Adapters, LoRA, QLoRA) and half fine‑tuning.  
- **Evaluation & Validation**: cross‑entropy metrics, safety benchmarks (Llama Guard, WILDGUARD), loss‑curve analysis.  
- **Deployment**: on‑premises/cloud options, WebGPU, vector stores, quantized and vLLM models.  
- **Monitoring & Support**: functional, prompt‑ and response‑level monitoring, alerting, and continual knowledge updates.

**Main conclusion:**  
The guide excels in breadth and depth, marrying theory with actionable best practices and covering state‑of‑the‑art techniques (PEFT, RLHF, multi‑agent, multimodal). Its extensive coverage benefits researchers and engineers alike, though its density suggests adding interactive examples and real‑world benchmark comparisons to improve usability for rapid reference.
</details>

https://ppc.land/content/files/2025/01/Newwhitepaper_Agents2.pdf?utm_source=chatgpt.com
<details>
  <summary>Agents – September 2, 2024</summary>

**Tags:** Agents, Cognitive Architecture, Orchestration, Tools, Prompt Engineering, RAG, LangChain, Vertex AI, Productionization

This whitepaper presents a comprehensive overview of generative AI agents, defining them as autonomous systems that extend foundational language models with external tools through a cyclical orchestration layer. It details the core components—Models, Tools (Extensions, Functions, Data Stores), and the Orchestration Layer—and explores reasoning frameworks like ReAct, Chain‑of‑Thought, and Tree‑of‑Thoughts. Through practical examples using LangChain and Google’s Vertex AI platform, it illustrates how agents can plan, execute, and refine multi‑step tasks by dynamically selecting and invoking tools while maintaining state and memory. :contentReference[filecite:turn0file0]{index=1}

**Main conclusion:**  
Production‑grade multi‑agent systems can dramatically enhance complex research and application workflows by combining robust orchestration patterns, targeted learning strategies, and diverse tool integrations; however, bridging the gap from prototype to reliable, scalable deployments demands meticulous engineering in tool design, evaluation frameworks, fault recovery, and iterative refinement. :contentReference[filecite:turn0file0]{index=2}
</details>


https://arxiv.org/pdf/2507.17168
<details>
  <summary>Improving LLMs’ Generalized Reasoning Abilities by Graph Problems – July 23, 2025</summary>

**Tags:** Graph Reasoning, Generalization, Continue Pretraining, GraphPile, LLM Robustness

This paper introduces a new paradigm—**Graph Problem Reasoning (GPR)**—as a foundation for improving LLMs' reasoning beyond mathematics. The authors present:
- **GraphPile**, a 10.9B-token dataset spanning 23 graph tasks (pathfinding, enumeration, computation, logic, etc.) with four components:  
  - Chain-of-Thought (CoT)  
  - Program-of-Thought (PoT)  
  - Trace of Execution (ToE)  
  - Real-world Graph Data  
- **GraphMind**, LLaMA and Gemma-based models trained on GraphPile, showing substantial gains:
  - +4.9% in math reasoning
  - +21.2% in logic, commonsense, and algorithmic tasks
  - +53% in graph reasoning

**Key contributions:**  
- Graph tasks are shown to generalize reasoning better than math-only pretraining, due to their diversity and complexity.  
- Ablation studies confirm the critical value of ToE and CoT in building step-by-step, interpretable reasoning.  
- Post-training boosts performance across domains (e.g., +23.6% on GSM8K with Gemma).  

**Main conclusion:**  
By using graph-based problems as a reasoning substrate, LLMs become not only stronger in graph domains but significantly more **generalized and robust** reasoners across mathematics, logic, code, and multi-hop QA—marking a shift from domain-specialized to **universally capable** AI models.
</details>


https://arxiv.org/pdf/2510.21148
<details>
  <summary>How to Auto-optimize Prompts for Domain Tasks (EGO-Prompt) – Oct 24, 2025</summary>

**Tags:** Prompt Optimization, Causal Graphs, Textual Gradients, LLM Reasoning, Domain Adaptation, Neuro-Symbolic AI

This paper introduces **EGO-Prompt (Evolutionary Graph Optimization for Prompting)**, a framework that automatically improves LLM reasoning by jointly evolving prompts and domain knowledge structures through:

- Proposing **Semantic Causal Graphs (SCG)** as flexible, expert-initialized but self-correcting structures that encode domain-specific causal knowledge and act as an interpretable reasoning backbone. :contentReference[oaicite:0]{index=0}  
- Introducing a **two-stage reasoning pipeline** where the model first generates *instance-specific reasoning guidance* from the SCG, then performs final prediction conditioned on this structured guidance. :contentReference[oaicite:1]{index=1}  
- Applying **textual gradients** — natural-language feedback generated by stronger LLMs — to iteratively optimize not only the prompt but also the graph structure itself through add/edit/delete causal relations. :contentReference[oaicite:2]{index=2}  

**Key results:**  
EGO-Prompt achieves **+7–12% F1 improvement** over state-of-the-art prompt optimization baselines and enables **small LLMs to match or exceed larger reasoning models** at a fraction of the inference cost, while also improving interpretability via refined causal graphs. :contentReference[oaicite:3]{index=3}

**Main conclusion:**  
By enabling prompts and structured causal knowledge to co-evolve through language-based gradients, EGO-Prompt represents a shift from static prompt engineering toward **self-adaptive, causally grounded reasoning systems**, laying foundations for future AI systems that can refine not only their answers, but the structure of their own thinking. :contentReference[oaicite:4]{index=4}
</details>

## Approaches
### Anthropic
Important articles
https://www.anthropic.com/engineering/built-multi-agent-research-system
https://www.anthropic.com/engineering/building-effective-agents
https://www.anthropic.com/news/model-context-protocol\



https://arxiv.org/pdf/2509.00189
<details>
  <summary>HiVA: Self-organized Hierarchical Variable Agent via Goal-driven Semantic-Topological Evolution – Aug 29, 2025</summary>

**Tags:** Multi-Agent Systems, Large Language Models, Semantic-Topological Evolution, Textual Gradients, Adaptive Intelligence  

This paper introduces **HiVA**, a novel framework for multi-agent systems that unifies semantic (what agents do) and topological (how agents interact) evolution through the **STEV algorithm**. Unlike static workflows or reactive loops, HiVA enables agents to evolve both behavior and collaboration structure from a single agent into a self-organized hierarchy.  

Key innovations:  
- **Semantic-Topological Evolution (STEV):** joint optimization of prompts, tools, and network structure using **textual gradients** derived from environmental feedback.  
- **Dynamic routing via Bayesian bandits (KABB):** selects task-relevant subgraphs of agents by balancing past performance, task alignment, and synergy.  
- **Hierarchical memory:** distributed across agent parameters, connection weights, and overall topology, enabling retention of collaboration patterns.  
- **Cost-efficient adaptability:** HiVA improves accuracy by 5–10% across tasks (QA, coding, reasoning, complex environments) while reducing LLM usage compared to baselines.  

**Experimental results:**  
- Outperforms ReAct, AutoGPT, MaAS, and others in multi-hop QA (+18.3%), program synthesis (+6.2%), and agentic environments (highest cost-efficiency score).  
- Ablation shows both **Semantic Evolution (SEV)** and **Topological Evolution (TEV)** are critical; removing either reduces performance by 7–11%.  
- Weakness: struggles in math tasks requiring strict logical consistency due to conflicts in agent verification.  

**Main conclusion:**  
HiVA demonstrates that **co-evolving agent semantics and topology is essential** for scalable, adaptive intelligence. By self-organizing into specialized, interconnected roles, HiVA systems achieve higher accuracy, efficiency, and robustness. This framework marks a step toward **self-improving, general-purpose agentic AI**, though challenges remain in conflict resolution and handling ambiguous feedback.  
</details>



## Architectures LLM
### DeepSeek
https://www.youtube.com/watch?v=0VLAoVGf_74

DeepSeek-V2
https://arxiv.org/pdf/2405.0443

DeepSeek-R1
https://arxiv.org/pdf/2501.12948


## MCP
https://github.com/modelcontextprotocol/servers

https://arxiv.org/pdf/2508.15760
<details>
  <summary>LiveMCP-101: Stress Testing and Diagnosing MCP-enabled Agents on Challenging Queries – August 21, 2025</summary>

**Tags:** AI Agents, Model Context Protocol, Tool Orchestration, Benchmarks, Error Analysis, Token Efficiency

This paper introduces **LiveMCP-101**, a benchmark of 101 complex real-world tasks designed to evaluate how AI agents use the **Model Context Protocol (MCP)** for multi-step reasoning and tool integration. Key contributions include:  
- A dataset of queries (easy, medium, hard), refined by LLM rewriting and human review, requiring web search, file operations, mathematical reasoning, and data analysis.  
- A **dual-execution evaluation method**: a reference agent follows a validated ground-truth execution plan, while test agents solve tasks autonomously, enabling robust comparison under dynamic tool outputs.  
- Experimental results showing that **even frontier models like GPT-5 succeed in fewer than 60% of tasks** (39% on hard tier), while open-source models perform significantly worse.  
- Ablation studies on iteration limits and MCP server pools, revealing clear efficiency ceilings and higher sensitivity to distractors in weaker models.  
- A detailed **failure analysis** across seven categories (planning, parameter errors, output handling), with semantic errors dominating even strong models.  

**Main conclusion:**  
LiveMCP-101 demonstrates that current LLM-based agents remain far from reliable autonomous tool users. They face persistent issues with dynamic environments, robust planning, and efficient token use. The benchmark establishes a new rigorous standard and highlights clear directions for advancing reasoning, orchestration, and error recovery in the next generation of AI agents.
</details>




## Test models 

Test model's reasoning
https://arxiv.org/pdf/2507.22411
<details>
  <summary>NeedleChain: Measuring Intact Long-Context Reasoning Capability of Large Language Models – July 30, 2025</summary>

**Tags:** Large Language Models, Long Context, Reasoning, Evaluation Benchmarks, ROPE, Model Limitations

This paper introduces **NeedleChain**, a novel benchmark designed to test whether large language models (LLMs) can perform *intact long-context reasoning*—that is, fully comprehend and integrate all relevant parts of a long context to answer a query.

Key contributions include:
- Demonstrating that traditional benchmarks like **Needle-in-a-Haystack (NIAH)** significantly overestimate LLMs’ long-context comprehension, as they only test retrieval of relevant snippets amid noise, not full-context understanding.
- Designing three **reasoning chains** (Forward, Backward, Mixed) where all context is query-relevant, and models must logically integrate chained salary statements to answer correctly.
- Showing that even state-of-the-art models like **GPT-4o, Qwen2.5, and LLaMA3.3** fail drastically on NeedleChain beyond 500 tokens—despite supporting 128K to 1M token contexts—especially on backward and mixed reasoning chains.
- Providing an **error taxonomy** (Instruction Miss, Needle Omission, Calculation Error) and **heatmap analysis**, revealing that models are "logically lost in the middle," struggling not with position but with logic integration in mid-sequence.
- Proposing a simple yet effective fix: **ROPE Contraction**, which improves positional encoding during inference by reducing the ROPE base, outperforming even advanced extension techniques like Yarn.

**Main conclusion:**  
Modern LLMs can technically *process* long contexts but cannot *understand* them when all information matters. NeedleChain exposes this gap and sets a new standard for evaluating—and improving—true long-context reasoning. The findings urge a shift from merely scaling input length to enhancing *semantic integration* within that length.
</details>

https://arxiv.org/pdf/2511.16043
<details>
  <summary>Agent0: Unleashing Self-Evolving Agents from Zero Data via Tool-Integrated Reasoning – Nov 20, 2025</summary>

**Tags:** Self-Evolving Agents, Reinforcement Learning, Tool Use, Curriculum Generation, Zero-Data Training

Agent0 introduces a fully autonomous framework where two agents—**a Curriculum Agent** and **an Executor Agent**—co-evolve without any human-provided data.  
The Curriculum Agent generates frontier tasks rewarded for **executor uncertainty**, **tool-use induction**, and **task diversity**, while the Executor Agent learns to solve them through **multi-turn tool-integrated reasoning** using a Python sandbox.  
A novel **Ambiguity-Dynamic PPO (ADPO)** stabilizes learning by scaling advantages and relaxing clipping for ambiguous tasks, enabling emergence of new reasoning patterns.

**Key contributions:**
- A **closed self-evolution loop** that continually increases task difficulty and agent capability.  
- **Tool-driven curricula**, where tasks progressively require more computation and structured reasoning.  
- Significant improvements: **+18% mathematical reasoning** and **+24% general reasoning** over base models.

**Main conclusion:**  
By coupling autonomous curriculum generation with tool-augmented, ambiguity-aware reinforcement learning, Agent0 demonstrates a scalable path for LLMs to self-improve beyond the limits of their initial knowledge—pointing toward genuinely self-evolving, high-capability AI agents.
</details>


## Agentic Web

https://arxiv.org/pdf/2507.21206
<details>
  <summary>Agentic Web: Weaving the Next Web with AI Agents – July 28 2025</summary>

**Tags:** Agentic Web, AI Agents, Large Language Models, Multi-Agent Systems, Autonomous Web, Web Infrastructure  

This paper lays out a blueprint for the coming **Agentic Web**, in which:

- **Autonomous LLM-powered agents** become first-class citizens, able to plan, coordinate, and execute multi-step informational, transactional, and communicational tasks with minimal human intervention.  
- The Web’s fabric is re-engineered for **machine-native interaction**: resources publish standardized, semantically rich endpoints (e.g., MCP, A2A) that agents can invoke directly.  
- A three-axis framework—**Intelligence · Interaction · Economy**—organizes research challenges: long-horizon reasoning & memory, dynamic tool orchestration & inter-agent collaboration, and machine-to-machine value exchange (pricing, metering, payments).  
- **Algorithmic pivots** are identified: passive search → proactive *agentic retrieval*; one-shot recommendations → iterative plans; single-agent loops → cooperative multi-agent graphs.  
- The authors survey emerging **systems** (agent browsers, orchestration frameworks, granular billing models) and early **applications** (end-to-end travel booking, deep-research agents, automated negotiations).  
- A dedicated risk section advocates **zero-trust architecture**, automated red-teaming, and market-manipulation defenses, while enumerating open problems in safety, economics, and governance.

**Main conclusion:**  
By merging autonomous agents with a machine-readable, economically incentivized Web, the Internet can evolve from static content delivery to goal-oriented execution chains. Realizing this vision will require advances in reliable long-term planning, secure agent protocols, transparent cost/accountability mechanisms, and cross-disciplinary policy—but promises a vastly more capable, self-optimizing digital ecosystem.
</details>


# MAS cooperation

https://arxiv.org/pdf/2508.04652
<details>
  <summary>MaGRPO in Multi-Agent and LLM Systems – August 7, 2025</summary>

**Tags:** Multi-Agent Systems, Reinforcement Learning, Role-based Policies, LLM Coordination, Agent Collaboration

This concept describes a framework called **MaGRPO** (*Multi-agent Generalized Role-based Policy Optimization*), aimed at optimizing the behavior of multiple agents that can dynamically assume different roles in a shared environment:

- Emphasizes **role-based learning**, allowing agents to generalize and switch between roles (e.g. planner, executor, verifier) based on context and task demands.  
- Supports **cooperative reinforcement learning**, where agents coordinate through shared rewards, role assignments, and mutual policy updates.  
- Enables **LLM-based agents** to better collaborate by structuring their behavior according to defined roles, facilitating modular task execution in areas such as autonomous dialogue, retrieval, synthesis, or tool use.

**Main conclusion:**  
MaGRPO provides a scalable way to manage role dynamics in complex multi-agent LLM systems. By optimizing role-aware policies, it enhances collaboration, specialization, and adaptability—laying the groundwork for advanced AI systems capable of reasoning and acting as cohesive teams.
</details>

<details>
  <summary>Galaxy: A Cognition-Centered Framework for Proactive, Privacy-Preserving, and Self-Evolving LLM Agents – August 6, 2025</summary>

**Tags:** LLM Agents, Cognitive Architecture, Proactive Assistance, Privacy Preservation, Self-Evolution

This paper introduces Galaxy, a cognition-centered IPA framework by:
- Proposing **Cognition Forest**, a tree-structured mechanism aligning cognitive modeling with system design for self-reinforcing co-evolution between architecture and implementation.  
- Implementing **KoRa**, a cognition-enhanced generative agent supporting both responsive and proactive skills through a Cognition–Action pipeline.  
- Introducing **Kernel**, a meta-cognition meta-agent with Privacy Gate for context-aware masking, system monitoring, and self-evolution capabilities.  

**Main conclusion:**  
Galaxy outperforms state-of-the-art benchmarks by integrating proactive behavior, robust privacy management, and continuous self-improvement, demonstrating the potential of co-constructive cognitive architectures in LLM agents.
</details>

https://arxiv.org/pdf/2511.09030
<details>
  <summary>Solving a Million-Step LLM Task with Zero Errors — Nov 12, 2025</summary>

**Tags:** Large Language Models, Multi-Agent Systems, Error Correction, Long-Horizon Reasoning, AI Scaling

This paper introduces a new paradigm for scaling LLM-based systems through **Massively Decomposed Agentic Processes (MDAPs)**, implemented as the MAKER framework, which successfully executes a task requiring over one million LLM steps with zero errors by:

- Applying **Maximal Agentic Decomposition (MAD)**, breaking complex tasks into the smallest possible micro-steps handled by specialized micro-agents to eliminate context overload and reduce per-step error rates.  
- Introducing **First-to-ahead-by-k voting**, a statistically grounded multi-agent error-correction mechanism that scales reliability logarithmically with task length.  
- Using **Red-flagging mechanisms** that discard malformed or overly long model outputs to reduce correlated and pathological errors, dramatically improving overall stability.  

The framework is validated on the **Towers of Hanoi (20 disks)** benchmark, achieving perfect execution across **1,048,575 steps**, demonstrating that scalable reliability can be achieved through architectural design rather than increasingly powerful base models.

**Main conclusion:**  
The paper demonstrates that superhuman reliability in long-horizon tasks is achievable through extreme task decomposition and distributed error correction, suggesting that future AI scalability will depend more on system architecture and agent orchestration than on further enlarging monolithic language models.

</details>

# Issues


https://arxiv.org/pdf/2511.02687
<details>
  <summary>The Collaboration Gap – November 2025</summary>

**Tags:** Multi-Agent Systems, Large Language Models, Collaboration, Coordination, Relay Inference, AI Communication

This paper introduces and empirically defines the **Collaboration Gap** — the performance drop that occurs when large language models (LLMs) must cooperate with other agents, including identical copies of themselves.  
Through a new **Collaborative Maze Benchmark**, the authors evaluate 32 modern models (OpenAI, Google, Anthropic, xAI, Cohere, etc.) in scenarios requiring partial information sharing and joint problem-solving.

Key findings include:
- **Severe collaboration degradation:** Most models lose 30–70% accuracy when moving from solo to paired performance, even with identical partners.  
- **Heterogeneous asymmetry:** Stronger models tend to mirror weaker partners’ reasoning styles, leading to performance loss unless dialogue order is controlled.  
- **Relay Inference breakthrough:** Allowing a strong model to “prime” the conversation (set structure and strategy) dramatically restores joint accuracy, suggesting that conversation framing is a core factor in machine cooperation.  

**Main conclusion:**  
Collaborative intelligence is a distinct dimension of capability, not an emergent property of solo intelligence.  
Future AI systems must be trained and architected for **mutual understanding, role negotiation, and communication grounding**—skills that cannot be patched post hoc. The study establishes a new foundation for evaluating and improving multi-agent AI ecosystems.
</details>


# Others


https://arxiv.org/pdf/2508.19227
<details>
  <summary>Generative Interfaces for Language Models – August 26, 2025</summary>

**Tags:** Large Language Models, Human-AI Interaction, Generative Interfaces, User Experience, Cognitive Offloading

This paper introduces a new paradigm called **Generative Interfaces (GenUI)**, where LLMs move beyond static chat to dynamically generate **interactive user interfaces** tailored to queries. Instead of long text outputs, models create adaptive tools such as learning simulators, analysis dashboards, or workflow managers.

Key contributions:
- Proposes **structured interface-specific representations** (interaction flows + finite state machines) to formally map user queries into UI logic.  
- Develops a **generation pipeline** that produces executable HTML/JS interfaces using reusable components and web retrieval.  
- Implements **iterative refinement with adaptive reward functions**, where LLMs evaluate, score, and improve interfaces until high-quality results are achieved.  
- Introduces **UIX benchmark** and a multi-dimensional evaluation (functional, interactive, emotional), validated through large-scale human and LLM-based studies.  

**Findings:**
- GenUI outperforms traditional conversational UIs in **70–84% of cases**, especially for information-dense and structured tasks.  
- Strongest gains appear in **data analysis, visualization, and business strategy**, where visual structure and interactivity reduce cognitive load.  
- Users cite **cognitive offloading**, **professional visual structure**, and **greater trustworthiness** as main drivers of preference.  
- Limitations include frontend-only support, iteration latency, and occasional over-generation of interfaces for simple queries.  

**Main conclusion:**  
Generative Interfaces mark a shift from LLMs as “textual copilots” to **designers of adaptive digital environments**. By combining structured UI logic with iterative refinement, GenUI significantly enhances usability, clarity, and user satisfaction, laying groundwork for future multimodal, domain-specific, and collaborative AI systems.
</details>

https://arxiv.org/pdf/2508.16876v1
<details>
  <summary>Dream to Chat: Model-based Reinforcement Learning on Dialogues with User Belief Modeling – August 23, 2025</summary>

**Tags:** Dialogue Systems, Reinforcement Learning, World Models, User Belief Modeling, Empathetic AI  

This paper introduces **DreamCUB**, a framework that combines model-based reinforcement learning (MBRL) with user belief modeling to enhance dialogue systems:  
- Defines a **Dialogue World Model (DWM)** capable of predicting user beliefs (emotion, sentiment, intention), next utterances, and rewards, extending beyond observable text.  
- Frames dialogues as a **POMDP**, where hidden psychological states are modeled via an information bottleneck, improving policy optimization.  
- Demonstrates **state-of-the-art results** on sentiment/emotion classification, query prediction, and dialogue generation across datasets like DailyDialog, ESConv, and EmpatheticDialogues.  
- Shows **strong generalization** to out-of-domain empathetic conversations and achieves the highest scores in **human evaluations** of fluency, sensitivity, and satisfaction.  
- Ablation studies confirm that incorporating user beliefs into both the world model and reward model is critical for optimal performance.  

**Main conclusion:**  
DreamCUB represents a significant step toward emotionally intelligent dialogue agents. By enabling systems to imagine future dialogue trajectories and reason about users’ emotional dynamics, it balances response quality with empathy and robustness. While limited to a subset of belief features (emotion, sentiment, intention), this approach opens pathways toward more human-centric and generalist AI assistants.  
</details>

<details>
  <summary>Simulating Psychological Risks in Human-AI Interactions – Nov 12, 2025</summary>

**Tags:** Large Language Models, AI Safety, Mental Health, Human-AI Interaction, Risk Simulation, Psychosis, Suicide, AI Alignment

This paper presents a real-case-driven framework for proactively identifying psychological risks in human–AI interactions by:
- Building a **simulation pipeline grounded in real-world harm cases**, extracting *Action → Outcome* patterns from 18 documented incidents involving addiction, anorexia, depression, homicide, psychosis, and suicide.  
- Generating **2,160 demographically diversified scenarios** combined with clinically validated mental health staging models to test how AI systems behave across escalating crisis levels.  
- Evaluating **four major LLMs** (GPT-5, Llama 4, Gemma 3, Sao10K Euryale) through multi-turn dialogues, revealing that nearly **37% of responses actively worsen psychological risk**.  
- Introducing a **taxonomy of AI failure modes**, classifying harmful responses into four major classes and fifteen subtypes (e.g., aggression normalization, emotional minimization, parasocial reinforcement, and eating disorder enablement).  

**Main conclusion:**  
Current large language models are not merely imperfect in high-risk psychological contexts — they systematically amplify harmful cognitive and emotional patterns. Without preventive, clinically grounded safety evaluation, conversational AI poses a structurally embedded risk of escalating mental health deterioration, particularly in vulnerable populations.

Source: :contentReference[oaicite:0]{index=0}

</details>


https://arxiv.org/pdf/2510.20967
<details>
  <summary>3DReasonKnee: Advancing Grounded Reasoning in Medical Vision-Language Models – Oct 23, 2025</summary>

**Tags:** Medical AI, Vision-Language Models, 3D MRI, Grounded Reasoning, Chain-of-Thought, MOAKS, Clinical AI

This paper introduces the first large-scale **3D grounded reasoning dataset** for medical imaging by:
- Proposing **3DReasonKnee**, a dataset of 494K expert-annotated quintuples combining 3D MRI volumes, diagnostic questions, 3D bounding boxes, clinician-authored chain-of-thought reasoning, and structured MOAKS severity scores.  
- Establishing **ReasonKnee-Bench**, a benchmark to evaluate both anatomical localization (3D IoU) and diagnostic reasoning accuracy in vision-language models.  
- Demonstrating that current state-of-the-art VLMs fail to perform reliable region-level localization and step-by-step diagnostic reasoning, revealing a critical gap between machine perception and real clinical reasoning workflows.  

**Main conclusion:**  
The work shows that modern multimodal models do not truly “think” like clinicians and that grounded 3D spatial reasoning is the main bottleneck. By providing expert-level reasoning traces and volumetric localization, 3DReasonKnee lays the foundation for next-generation medical AI that can move from surface-level pattern recognition toward trustworthy, interpretable, and clinically aligned decision-making.

**Source (local PDF):** /mnt/data/2510.20967v1.pdf
</details>

# Hallucinations


https://arxiv.org/pdf/2512.01797v2 ⚡⚡⚡
<details>
  <summary>H-Neurons: On the Existence, Impact, and Origin of Hallucination-Associated Neurons in LLMs – December 1, 2025</summary>

**Tags:** Large Language Models, Hallucinations, Neuron-Level Mechanisms, Over-Compliance, Reliability

This paper uncovers a tiny, highly predictive subset of **hallucination-associated neurons (H-Neurons)** inside LLMs by training a sparse linear probe on neuron contributions for answer tokens.  
It then shows that **scaling these neurons’ activations** causally controls a spectrum of **over-compliance behaviors**—accepting false premises, trusting misleading context, sycophancy under user pressure, and bypassing safety constraints.  
Finally, cross-model and pretrain–chat transfer analyses reveal that **H-Neurons originate during pre-training** and remain largely unchanged by instruction tuning, yet still reliably signal hallucination risk.

**Main conclusion:**  
Hallucinations and “trying too hard to please the user” are not diffuse properties of the whole model but are strongly concentrated in an ultra-sparse set of neurons whose activations both *predict* and *drive* over-compliant behavior, suggesting a concrete handle for future hallucination detection and targeted alignment interventions.
</details>
