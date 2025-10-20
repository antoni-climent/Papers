## ♻️ Continuous Improvement

### May 2025 — AlphaEvolve: A Gemini-Powered Coding Agent for Designing Advanced Algorithms
**Paper:** [AlphaEvolve (PDF)](https://storage.googleapis.com/deepmind-media/DeepMind.com/Blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/AlphaEvolve.pdf)  
**Blog:** [DeepMind Announcement](https://deepmind.google/discover/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/)  

**Summary:**  Announced on May 14, 2025, AlphaEvolve is an evolutionary coding agent powered by large language models for general-purpose algorithm discovery and optimization.  
AlphaEvolve pairs the creative problem-solving capabilities of Gemini models with automated evaluators that verify answers, and uses an evolutionary framework to improve upon the most promising ideas.

---

### June 2025 — Darwin Godel Machine: Open-Ended Evolution of Self-Improving Agents
**Blog:** [Sakana AI](https://sakana.ai/dgm/)  
**Video:** [YouTube Discussion](https://www.youtube.com/watch?v=a1L0frpDE4k)  
**Summary:** TODO

### Can Large Language Models Invent Algorithms to Improve Themselves?:Algorithm Discovery for Recursive Self-Improvement through Reinforcement Learning

**Paper:** [arXiv](https://arxiv.org/abs/2410.15639)

**Summary:** 
The objective is to iteratively improve a base model by merging it with fine-tuned versions. The contribution is that another SLM is in charge of creating the new merging strategies. 
The loop goes as follows:
1. Programming model creates a merging algorithm 
2. Base model is merged with fine-tuned versions of the same model
3. Resulting model is evaluated with two benchmarks 
4. The benchmark results and the merging code is used to create preference data and train the programming model 
5. Go back to step 1 

What are task vectors?? The weights generated during the training of the LoRA fine tunning. 
