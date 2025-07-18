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

