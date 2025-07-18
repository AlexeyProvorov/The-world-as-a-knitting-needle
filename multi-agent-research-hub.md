Useful thoughts and experience about the MAS developing 
https://cognition.ai/blog/dont-build-multi-agents#principles-of-context-engineering 
<details>
  <summary>Overview of “Don’t Build Multi-Agents”</summary>

  The article argues that parallel multi-agent chains are fragile because context fragments and implicit decisions get siloed, causing errors to compound. Instead, it introduces **Context Engineering**—sharing the full trace of prior actions and treating each action as carrying hidden assumptions—and shows that the most reliable pattern is a **single-threaded linear agent**, possibly augmented with a **history-compressor** LLM to summarize long interactions into key events without overflowing context windows.

  **Main conclusion:**  
  For robust, long-running AI agents, avoid parallel multi-agent setups and focus on seamless context management—either via one coherent agent or via intelligent history compression—so that every decision is consistently informed by the complete task context.
</details>

https://www.anthropic.com/engineering/built-multi-agent-research-system