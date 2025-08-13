Useful thoughts and experience about the MAS developing 


# Must have



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


## RAG
### Graphs

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

## Approaches
### Anthropic
Important articles
https://www.anthropic.com/engineering/built-multi-agent-research-system
https://www.anthropic.com/engineering/building-effective-agents
https://www.anthropic.com/news/model-context-protocol\


## Architectures LLM
### DeepSeek
https://www.youtube.com/watch?v=0VLAoVGf_74

DeepSeek-V2
https://arxiv.org/pdf/2405.0443

DeepSeek-R1
https://arxiv.org/pdf/2501.12948


## MCP
https://github.com/modelcontextprotocol/servers



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


# Context Engineering

