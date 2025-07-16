

[The Collapse of AI Reasoning (by Apple)](https://www.youtube.com/@code4AI)

https://ml-site.cdn-apple.com/papers/the-illusion-of-thinking.pdf

---
title: The Illusion of Thinking: Detailed Analysis & Related Works
tags: [LLM, reasoning, algorithms, survey]

---
# 📖 Introduction  
Modern **Large Reasoning Models (LRMs)**—LLMs augmented with explicit chain-of-thought (CoT)—score highly on benchmarks yet mask fundamental reasoning limits. **The Illusion of Thinking** (Shojaee et al., 2025) exposes these limits via a **controlled puzzle suite**, varying problem complexity with surgical precision. This note merges a deep dive into that core study with in-depth overviews of six contemporary works that extend, challenge or complement its insights.

---

# ⚙️ 1. Core Study: *The Illusion of Thinking*  
**Parshin Shojaee, Rolf Carlsson, Emily Harding et al. (2025)**  
**Venue:** arXiv: [2506.06941](https://arxiv.org/abs/2506.06941) • **PDF:** [Download](https://ml-site.cdn-apple.com/papers/the-illusion-of-thinking.pdf)

## 1.1 Methodology  
- **Controlled Puzzle Suite**  
  - **Tower of Hanoi** (N disks)  
  - **Checker Jumping** (N checker pairs)  
  - **River Crossing** (N passenger pairs)  
  - **Blocks World** (N blocks)  
  - Complexity scales linearly with N; puzzles are fully deterministic.  
- **Data & Evaluation Pipeline**  
  1. For each N ∈ {2…10}, generate 25 random instances.  
  2. Prompt each model with the puzzle description; allow up to 64 K tokens for CoT.  
  3. Extract every reasoning step and verify against a **deterministic simulator** for exact correctness.  
- **Model Comparisons**  
  - **Thinking** vs. **Non-Thinking** variants at equal token budgets:  
    - *Claude 3.7 Sonnet Thinking* vs. *Claude 3.7*  
    - *DeepSeek-R1* vs. *DeepSeek-V3*  
    - *o3-mini* (baseline LRM)

## 1.2 Key Findings  
1. **Three Complexity Regimes**  
   - **Low N:** Classic LLMs (no CoT) match or outperform LRMs in accuracy & token efficiency.  
   - **Medium N:** LRMs leverage longer CoT to gain clear accuracy advantage.  
   - **High N:** **All models collapse**—accuracy falls to near zero beyond a threshold N.

2. **CoT Length vs. Complexity**  
   - CoT length initially **grows** with N, then **abruptly shrinks** at the collapse point, despite unused token budgets.

3. **Intermediate Reasoning Patterns**  
   - **Overthinking (Low N):** Models find the correct solution early, then produce extraneous incorrect steps.  
   - **Self-Correction (Medium N):** Early missteps are progressively corrected later in the CoT trace, yielding a valid solution by the end.  
   - **No Valid Steps (High N):** Traces contain zero correct intermediate moves.

4. **Algorithmic Prompting Effects**  
   - Injecting explicit pseudocode **does not** raise the collapse threshold or improve final accuracy.  
   - Performance varies by puzzle type: e.g., *Claude 3.7 Sonnet* solves ~100 moves in Hanoi (N=10) but only ~4 in River Crossing (N=3), suggesting **training bias** in puzzle exposure.

## 1.3 Contributions & Limitations  
- **Contributions:**  
  1. **Fine-grained benchmark** for reasoning complexity using deterministic puzzles.  
  2. Identification of **three performance regimes** and a **collapse phenomenon**.  
  3. Discovery of a **non-monotonic CoT scaling** (volume-then-collapse).  
  4. New **stepwise metrics**: overthinking rate, correction dynamics.  
  5. Evidence that **explicit algorithmic hints** alone cannot overcome reasoning limits.

- **Limitations:**  
  - Narrow domain: four puzzle types may not generalize to open-ended or knowledge-intensive tasks.  
  - Black-box evaluation: lack of model internals prevents mechanistic explanations of collapse.  
  - Data bias: varied performance across puzzles hints at uneven training exposure.

---

# 🔗 2. Related & Extending Works  

## 2.1 MAGMA 🔍  
**Alexander K. Taylor et al. (Oct 2024)**  
**Benchmark:** arXiv: [2410.22597](https://arxiv.org/abs/2410.22597)  
- **Scope:** Evaluates LLMs on **graph algorithms**—BFS, DFS, Dijkstra, Floyd–Warshall, Prim’s MST—using step-by-step prompts.  
- **Method:** Generate random graphs up to 50 nodes; ask models to output each algorithmic step; verify with graph simulators.  
- **Findings:** Accuracy decays sharply as graph size and path length grow; LLMs fail to maintain correct frontier sets or distances beyond ~10 nodes.  
- **Relation to Core Study:** Demonstrates that **structural reasoning collapse** extends from puzzles to classical algorithms in graph domains.

## 2.2 TransNAR 🚀  
**Wilfried Bounsi, Borja Ibarz et al. (Jun 2024)**  
**Paper:** arXiv: [2406.09308](https://arxiv.org/abs/2406.09308)  
- **Approach:** Hybrid **GNN + Transformer** architecture. Pre-train a Neural Algorithmic Reasoner (NAR) on graph tasks, then cross-attend a Transformer to NAR embeddings.  
- **Evaluation:** Textual CLRS-30 suite (30 algorithmic problems described in English).  
- **Results:** TransNAR outperforms pure Transformers by 15–25% on both in-distribution and out-of-distribution splits, especially on **longer reasoning chains**.  
- **Relation:** Suggests embedding **specialized modules** (e.g., GNNs) within LLMs can extend collapse thresholds identified in the core puzzle study.

## 2.3 Think-and-Execute 🛠️  
**Hyungjoo Chae, Yeonghyeon Kim et al. (Apr 2024)**  
**Paper:** arXiv: [2404.02575](https://arxiv.org/abs/2404.02575)  
- **Framework:**  
  1. **Think:** Generate **high-level pseudocode** skeleton for the task.  
  2. **Execute:** Specialize and simulate that pseudocode on each instance, verifying step correctness.  
- **Benchmarks:** Seven algorithmic reasoning tasks (e.g., sequence sorting, pathfinding).  
- **Impact:** Outperforms CoT and Program-of-Thought methods by 10–30%, reducing error accumulation.  
- **Relation:** Validates that **decoupling logic discovery from execution** can mitigate overthinking and collapse in core puzzles.

## 2.4 Distilling Algorithmic Reasoning 📚  
**Jierui Li & Raymond Mooney (Apr 2024)**  
**Paper:** arXiv: [2404.08148](https://arxiv.org/abs/2404.08148)  
- **Method:**  
  1. Use a strong LLM to generate **natural-language explanations** for correct <problem, program> pairs.  
  2. **Distill** a smaller “Reasoner” by fine-tuning on <problem, explanation> examples.  
- **Evaluation:** Standard competitive programming problems (e.g., Codeforces-style).  
- **Results:** Distilled Reasoner achieves similar or better accuracy than LLM CoT baselines while using <10% parameters.  
- **Relation:** Addresses **overthinking** by training on concise, human-style explanations rather than raw CoT traces.

## 2.5 Matching Markets Meet LLMs ⚖️  
**Hadi Hosseini, Samarth Khanna, Ronak Singh (Jun 2025)**  
**Paper:** arXiv: [2506.04478](https://arxiv.org/abs/2506.04478)  
- **Benchmark:** Stable matching & preference reasoning tasks—Gale-Shapley, blocking-pair detection, preference completion.  
- **Findings:** LLMs succeed on small markets (<20 agents) but **fail to maintain stability** or detect blocking pairs in larger markets (>50 agents); error accumulation parallels puzzle collapse.  
- **Relation:** Extends collapse phenomenon to **preference-based multi-step reasoning**, highlighting the generality of reasoning limits.

## 2.6 LLM4AD Survey 💡  
**Liu et al. (Oct 2024)**  
**Survey:** arXiv: [2410.14716](https://arxiv.org/abs/2410.14716)  
- **Content:** Reviews 180+ works on LLMs in **algorithm design**, proposes a **4-axis taxonomy**:  
  1. **Role** of LLM (planner, executor, explainer)  
  2. **Search** methods (beam, heuristic, self-ask)  
  3. **Prompt strategies** (CoT, PoT, self-critique)  
  4. **Application domains** (graphs, puzzles, markets)  
- **Insights:** Identifies trends in **scalability**, **robustness**, and **interpretability**; calls for unified benchmarks.  
- **Relation:** Places *The Illusion of Thinking* and its extensions within a **broader ecosystem** of algorithmic LLM research.

---

# 💡 Integrated Insights & Outlook  
- **Universal Collapse:** From puzzles to graphs to markets, LLMs exhibit an **accuracy cliff** beyond modest reasoning depths.  
- **Mitigation Paths:**  
  - **Hybrid Modules:** GNN+Transformer (TransNAR) to extend reasoning horizon.  
  - **Decoupled Execution:** Think-and-Execute’s skeleton-then-simulate paradigm.  
  - **Explain-Based Training:** Distilled Reasoners to curb overthinking.  
- **Future Directions:**  
  1. **Unified Complexity Benchmarks** merging puzzles, graphs, markets.  
  2. **Modular LRM Architectures** integrating symbolic, neural and hybrid components.  
  3. **Interpretable Metrics** beyond final accuracy—stepwise fidelity, error accumulation rates.

---

# 📚 References  
- **The Illusion of Thinking** — Shojaee et al., 2025. [arXiv:2506.06941](https://arxiv.org/abs/2506.06941)  
- **MAGMA** — Taylor et al., 2024. [arXiv:2410.22597](https://arxiv.org/abs/2410.22597)  
- **TransNAR** — Bounsi & Ibarz et al., 2024. [arXiv:2406.09308](https://arxiv.org/abs/2406.09308)  
- **Think-and-Execute** — Chae et al., 2024. [arXiv:2404.02575](https://arxiv.org/abs/2404.02575)  
- **Distilling Algorithmic Reasoning** — Li & Mooney, 2024. [arXiv:2404.08148](https://arxiv.org/abs/2404.08148)  
- **Matching Markets Meet LLMs** — Hosseini et al., 2025. [arXiv:2506.04478](https://arxiv.org/abs/2506.04478)  
- **LLM4AD Survey** — Liu et al., 2024. [arXiv:2410.14716](https://arxiv.org/abs/2410.14716)  
