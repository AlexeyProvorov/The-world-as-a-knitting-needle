Mimicking or Reasoning: Rethinking Multi-Modal In-Context Learning in Vision-Language Models
https://arxiv.org/pdf/2506.07936v1
https://www.youtube.com/watch?v=VFcEanEAXJM

# 📄 Mimicking or Reasoning: Rethinking Multi-Modal In-Context Learning in Vision-Language Models

- **Paper**: Chengyue Huang *et al.*  
- **arXiv**: [2506.07936](https://arxiv.org/abs/2506.07936)   
- **Authors**: Chengyue Huang, Yuchen Zhu, Sichen Zhu, Jingyun Xiao, Moises Andrade, Shivang Chopra, Zsolt Kira  

---

## 🎯 Goals & Motivation  
- **Question** whether vision-language models (VLMs) truly **learn** from few-shot multimodal in-context examples (MM-ICL) or merely apply **surface heuristics** (copy last example, majority vote).  
- Propose **OOD-MM-ICL**, drawing support examples from a *different* dataset; observe that performance **does not improve** (and can degrade), indicating **shallow copying** rather than real generalization. 

---

## 🔬 Methodology  
1. **Four MM-ICL Protocols** (Sec. 5):  
   - **P1**: demos contain *only answers*.  
   - **P2**: demos include *answer + rationale*, but model output is *only answer*.  
   - **P3**: demos are *only answers*, output is *rationale + answer*.  
   - **P4** (*Pseudo Reasoning*): *rationale + answer* in both demos and output.   
2. **Pseudo Reasoning Pipeline**:  
   - Generate rationale+answer for each support example.  
   - **Filter** by answer correctness or replace with **ground-truth rationales**.  
   - Concatenate enriched demonstrations before the query.   
3. **Retrieval Strategies**:  
   - **Random**, **unimodal** & **multimodal** similarity retrieval.  
   - Without reasoning, multimodal retriever boosts copying heuristics; in P4 it **hurts** performance due to inconsistent rationale styles.   

---

## 🧪 Experimental Setup  
- **Models**: Qwen2.5-VL, VLM-R1, VL-Rethinker, LLaVA-CoT, InternVL2.5 (3 B–72 B params) + closed-source Gemini 2.0.  
- **Datasets**:  
  - **Perception**: TextVQA, OK-VQA  
  - **Reasoning**: ScienceQA, A-OKVQA, M³CoT  
- **Evaluation**: Accuracy with string-normalization & GPT-4o mini as judge.   

---

## 📊 Main Results  
- **Zero- vs Few-Shot**: Few-shot *never* beats zero-shot; adding reasoning demos yields **minimal** gains.   
- **Retrieval**: Multimodal retriever helps basic perception but **fails** in reasoning; random support often best.   
- **ID vs OOD**: Format consistency closes the in- vs out-distribution gap, yet few-shot still doesn’t surpass zero-shot.   

---

## 📝 Conclusions & Limitations  
- Current VLMs **lack true** MM-ICL and fall back on **shallow heuristics**.  
- **Limitations**: focus on open-source, single closed-source test, no reasoning-aware retrieval.

---

## 🔮 Future Directions  
- **Tight cross-modal fusion** architectures  
- **Reasoning-aware retrieval** strategies  
- **Interleaved-modal Chain-of-Thought**  
- **Compositional reasoning** training in context  

---

## 🔗 Related Works  

### 📋 What Makes Multimodal In-Context Learning Work?  
- **Authors**: Folco B. Baldassini, Mustafa Shukor, Matthieu Cord *et al.*  
- **Venue**: CVPR 2024 Workshop  
- **Link**: [arXiv:2404.15736](https://arxiv.org/abs/2404.15736) :contentReference[oaicite:9]{index=9}  
- **Key Insights**:  
  - Proposes a **comprehensive framework** to study M-ICL across tasks (VQA, captioning, classification) and models (IDEFICS, OpenFlamingo).  
  - **Finds** M-ICL is overwhelmingly **text-driven**, with visual modality playing little role except in pure image→text tasks; advanced retrieval (RICES) **≃** majority vote; strong **recency bias**, copying last example. :contentReference[oaicite:10]{index=10}  
- **Relevance**: Empirically demonstrates **surface shortcuts** in M-ICL, motivating the need for **reasoning-aware pipelines**.

### 🚀 M³CoT: A Novel Benchmark for Multi-Domain Multi-Step Multi-Modal Chain-of-Thought  
- **Authors**: Qiguang Chen, Libo Qin, Jin Zhang *et al.*  
- **Venue**: ACL 2024  
- **Link**: [ACL Anthology](https://aclanthology.org/2024.acl-long.446/) :contentReference[oaicite:11]{index=11}  
- **Contributions**:  
  1. **Identifies** three gaps in existing MCoT benchmarks:  
     - *No visual modal reasoning* (text suffices).  
     - *Single-step* visual reasoning only.  
     - *Domain missing* (commonsense, math).  
  2. **Constructs** M³CoT via manual removal of trivial samples, expert annotation of multi-step CoT, and LLM-guided domain augmentation.  
  3. **Evaluates** SOTA MCoT methods on M³CoT, showing:  
     - Emergence of CoT only at **≥13 B params**.  
     - **Fine-tuning** outperforms vanilla ICL and prompting.  
     - **Large performance gap** remains vs. humans. :contentReference[oaicite:12]{index=12}  
- **Relevance**: Provides a **rigorous, multi-domain** testbed highlighting VLM weaknesses in **complex multi-step** CoT.

### 🔍 From Introspection to Best Practices: Principled Analysis of Demonstrations in MM-ICL  
- **Authors**: Nan Xu, Fei Wang, Sheng Zhang, Hoifung Poon, Muhao Chen  
- **Venue**: arXiv (NAACL submission) 2025  
- **Link**: [arXiv:2407.00902](https://arxiv.org/abs/2407.00902) :contentReference[oaicite:13]{index=13}  
- **Approach**:  
  - **Systematically perturb** visual/textual inputs across diverse tasks (OCR, KIE, autonomous driving instructions).  
  - **Quantify** modality impact, inductive biases (flipped labels, hallucinations).  
- **Findings**:  
  1. **Modality importance** differs by task: visual matters in KIE, text in application tasks.  
  2. **Modality-driven demo selection** (CLIP vs. BERTScore vs. ALBEF) **boosts** performance accordingly.  
  3. **Emergent inductive bias**: larger models learn to follow demo biases even if they contradict pretraining. :contentReference[oaicite:14]{index=14}  
- **Relevance**: Offers **best practices** for crafting effective demonstrations, directly addressing **modality-aware retrieval**.

### 🤖 VL-Rethinker: Incentivizing Self-Reflection of Vision-Language Models with RL  
- **Authors**: Haozhe Wang, Chao Qu, Zuming Huang, Wei Chu, Fangzhen Lin, Wenhu Chen  
- **Venue**: arXiv 2025  
- **Link**: [arXiv:2504.08837](https://arxiv.org/abs/2504.08837) :contentReference[oaicite:15]{index=15}  
- **Contributions**:  
  1. **Adapts** Group Relative Policy Optimization (GRPO) with **Selective Sample Replay (SSR)** to counter vanishing advantages in RL fine-tuning of VLMs.  
  2. **Proposes** *Forced Rethinking*, appending a trigger token to enforce an explicit reflection step.  
  3. **Demonstrates** state-of-the-art open-source performance on MathVista (80.4%), MathVerse (63.5%), EMMA, MMMU-Pro, narrowing gap to GPT-o1. :contentReference[oaicite:16]{index=16}  
- **Relevance**: Presents a **direct RL pathway** to instill **slow-thinking** and self-verification in VLMs missing from few-shot pipelines.

### 🔄 Interleaved-Modal Chain-of-Thought  
- **Authors**: Jun Gao, Yongqi Li, Ziqiang Cao, Wenjie Li  
- **Venue**: arXiv 2025  
- **Link**: [arXiv:2411.19488](https://arxiv.org/abs/2411.19488) :contentReference[oaicite:17]{index=17}  
- **Innovation**:  
  - **Interleaves** visual patches and textual rationales in CoT steps, aligning reasoning closely with image content.  
  - **Attention-driven Selection (ADS)**: a plug-and-play method using VLM attention maps to insert fine-grained image regions without retraining.  
- **Results**: Up to **14%** absolute gain in interpretability & accuracy over text-only CoT on three benchmarks. :contentReference[oaicite:18]{index=18}  
- **Relevance**: Realizes the “**interleaved-modal CoT**” direction, enriching cross-modal fusion within CoT.

### 📈 MME-CoT: Benchmarking CoT in Large Multimodal Models  
- **Authors**: Dongzhi Jiang, Renrui Zhang, Ziyu Guo, et al.  
- **Venue**: arXiv 2025  
- **Link**: [arXiv:2502.09621](https://arxiv.org/abs/2502.09621) :contentReference[oaicite:19]{index=19}  
- **Benchmark**: Six domains—math, science, OCR, logic, space-time, general scenes; **2,xxx** fine-grained problems.  
- **CoT Evaluation Suite**: Three novel metrics assessing **Quality**, **Robustness**, **Efficiency**, yielding six sub-scores per model.  
- **Insights**:  
  1. Models with **reflection** (Kimi k1.5) top CoT quality.  
  2. CoT prompting often **degrades** perception tasks (overthinking).  
  3. Reflection-enabled models remain **inefficient** (longer self-correction). :contentReference[oaicite:20]{index=20}  
- **Relevance**: Provides a **holistic evaluation** tool to dissect CoT behaviors and guide future architectures.

### 🎨 EMMA: An Enhanced MultiModal Reasoning Benchmark  
- **Authors**: Yunzhuo Hao, Jiawei Gu, Huichen W. Wang, *et al.*  
- **Venue**: ICML 2025 Oral; arXiv 2025  
- **Link**: [arXiv:2501.05444](https://arxiv.org/abs/2501.05444) :contentReference[oaicite:21]{index=21}  
- **Benchmark Composition**: 2,788 total problems (1,796 newly created) across **math, physics, chemistry, coding**, each labeled for specific multimodal skills. :contentReference[oaicite:22]{index=22}  
- **Findings**:  
  - **State-of-the-art MLLMs** struggle on complex multi-step tasks; **CoT prompting** & **test-time compute scaling** provide limited gains, still **27%** behind humans. :contentReference[oaicite:23]{index=23}  
- **Relevance**: Highlights urgent need for **integrated reasoning** paradigms beyond independent modality processing.

---

> **Tags:** `#multimodal-ICL` `#vision-language` `#chain-of-thought` `#benchmarks`
