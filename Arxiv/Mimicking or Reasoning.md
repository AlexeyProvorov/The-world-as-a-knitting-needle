Mimicking or Reasoning: Rethinking Multi-Modal In-Context Learning in Vision-Language Models
https://arxiv.org/pdf/2506.07936v1
https://www.youtube.com/watch?v=VFcEanEAXJM

# 📄 Mimicking or Reasoning: Rethinking Multi-Modal In-Context Learning in Vision-Language Models

- **Paper**: Chengyue Huang *et al.*  
- **arXiv**: [2506.07936](https://arxiv.org/abs/2506.07936)  
- **Authors**: Chengyue Huang, Yuchen Zhu, Sichen Zhu, Jingyun Xiao, Moises Andrade, Shivang Chopra, Zsolt Kira  

---

## 🎯 Goals & Motivation  
- **Challenge** the assumption that vision-language models (VLM) genuinely **learn** from few-shot multimodal in-context examples, rather than relying on **surface heuristics** (copying answers, majority voting).  
- Introduce **OOD-MM-ICL**: support examples drawn from a *different* dataset—performance **does not improve** (and can even degrade), indicating **shallow copying** rather than true generalization.

---

## 🔬 Methodology  
1. **Four MM-ICL Protocols** (Sec. 5):  
   - **P1**: demonstrations contain *only answers*.  
   - **P2**: demos include *answer + rationale*, but model output is *only answer*.  
   - **P3**: demos are *only answers*, output is *rationale + answer*.  
   - **P4 (Pseudo Reasoning)**: *rationale + answer* in both demos and output.  

2. **Pseudo Reasoning Pipeline**:  
   - Model generates a rationale + answer for each support example.  
   - **Filter** by answer correctness or replace with **ground-truth rationales**.  
   - Concatenate these enriched demonstrations before the query.

3. **Retrieval Strategies**:  
   - **Random**, **unimodal** and **multimodal** similarity retrieval.  
   - Without reasoning, multimodal retriever boosts copying heuristics; within P4, it **hurts** performance due to inconsistent rationale styles.

---

## 🧪 Experimental Setup  
- **Models**: Qwen2.5-VL, VLM-R1, VL-Rethinker, LLaVA-CoT, InternVL2.5 (3 B–72 B params), plus closed-source Gemini 2.0.  
- **Datasets**:  
  - **Perception**: TextVQA, OK-VQA  
  - **Reasoning**: ScienceQA, A-OKVQA, M³CoT  
- **Evaluation**: Accuracy with string-normalization and GPT-4o mini as judge.

---

## 📊 Main Results  
- **Zero- vs Few-Shot**: Few-shot *never* outperforms zero-shot; adding reasoning demos yields **minimal gains**.  
- **Retrieval**: Multimodal retriever helps **basic** perception tasks but **fails** in reasoning; random support often best.  
- **ID vs OOD**: Format consistency closes the in- vs out-of-distribution gap, yet few-shot still doesn’t beat zero-shot.

---

## 📝 Conclusions & Limitations  
- Current VLMs **lack true** multimodal ICL and fall back on **shallow heuristics**.  
- **Limitations**: focus on open-source models, single closed-source check, no reasoning-aware retrieval.

---

## 🔮 Future Directions  
- **Tight cross-modal fusion** architectures  
- **Reasoning-aware retrieval** strategies  
- **Interleaved-modal Chain-of-Thought**  
- **Compositional reasoning** training in context  

---

## 🔗 Related Works

### 1. What Makes Multimodal In-Context Learning Work? 📋  
- **Authors**: Folco B. Baldassini *et al.*  
- **Venue**: CVPR 2024  
- **Link**: [arXiv:2404.15736](https://arxiv.org/abs/2404.15736)  
- **Summary**:  
  - Extensive ablations on retrieval methods, prompt formats, and text vs image contributions.  
  - Shows models heavily **rely on text**; advanced MM-ICL strategies ≈ majority voting baseline.  
  - **Relevance**: corroborates that VLMs use surface patterns over deep multimodal reasoning.

### 2. M³CoT: A Novel Benchmark for Multi-Domain Multi-Step Multi-Modal Chain-of-Thought 🚀  
- **Authors**: Qiguang Chen *et al.*  
- **Venue**: ACL 2024  
- **Link**: [arXiv:2405.16473](https://arxiv.org/abs/2405.16473)  
- **Summary**:  
  - Introduces a benchmark spanning multiple domains and multi-step CoT tasks in multimodal settings.  
  - Reveals large gaps between SOTA VLMs and human performance; sensitivity to rationale quality.  
  - **Relevance**: highlights VLM weaknesses on complex reasoning tasks.

### 3. From Introspection to Best Practices: Principled Analysis of Demonstrations in MM-ICL 🔍  
- **Authors**: Nan Xu *et al.*  
- **Venue**: arXiv 2024  
- **Link**: [arXiv:2407.00902](https://arxiv.org/abs/2407.00902)  
- **Summary**:  
  - Qualitative and quantitative study of demo selection, filtering, and ordering.  
  - Provides **guidelines** that reduce variance and improve model stability.  
  - **Relevance**: informs reasoning-aware retrieval and demo curation strategies.

### 4. VL-Rethinker: Incentivizing Self-Reflection of Vision-Language Models with RL 🤖  
- **Authors**: Haozhe Wang *et al.*  
- **Venue**: arXiv 2025  
- **Link**: [arXiv:2504.08837](https://arxiv.org/abs/2504.08837)  
- **Summary**:  
  - Uses Group Relative Policy Optimization to reward coherent, complete rationales.  
  - Achieves significant gains in CoT coherence and correctness on reasoning benchmarks.  
  - **Relevance**: a path toward reasoning-aware VLMs missing from vanilla MM-ICL.

### 5. Interleaved-Modal Chain-of-Thought 🔄  
- **Authors**: Jun Gao *et al.*  
- **Venue**: arXiv 2024  
- **Link**: [arXiv:2411.19488](https://arxiv.org/abs/2411.19488)  
- **Summary**:  
  - Alternates text and image segments within CoT sequences.  
  - Improves compositional reasoning and OOD robustness vs. monomodal CoT.  
  - **Relevance**: realizes the “interleaved-modal CoT” direction from the main paper.

### 6. MME-CoT: Benchmarking Chain-of-Thought in Large Multimodal Models for Reasoning Quality, Robustness, and Efficiency ⚡  
- **Authors**: Dongzhi Jiang *et al.*  
- **Venue**: arXiv 2025  
- **Link**: [arXiv:2502.09621](https://arxiv.org/abs/2502.09621)  
- **Summary**:  
  - Evaluates latency/throughput trade-offs, robustness to prompt perturbations, and rationale quality metrics.  
  - Offers prompt-engineering recommendations to balance CoT quality and speed.  
  - **Relevance**: complements format-consistency findings and optimizes reasoning pipelines.

### 7. EMMA: An Enhanced Multi-Modal ReAsoning Benchmark 🎨  
- **Authors**: Yunzhuo Hao *et al.*  
- **Venue**: arXiv 2025  
- **Link**: [arXiv:2501.05444](https://arxiv.org/abs/2501.05444)  
- **Summary**:  
  - Integrates visual, textual, and tabular data into formal and semantic multi-step reasoning tasks.  
  - Introduces fine-grained CoT evaluation metrics.  
  - **Relevance**: provides a rich benchmark for cross-modal fusion and compositional reasoning.  

---

> **Tags:** `#multimodal-ICL` `#vision-language` `#chain-of-thought` `#benchmarks`  
