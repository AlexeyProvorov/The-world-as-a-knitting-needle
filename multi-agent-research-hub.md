Useful thoughts and experience about the MAS developing 


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
 
 # Must have
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



## RAG
### Graphs


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
