## ♻️ Continuous Improvement

### May 2025 — AlphaEvolve: A Gemini-Powered Coding Agent for Designing Advanced Algorithms
**Paper:** [AlphaEvolve (PDF)](https://storage.googleapis.com/deepmind-media/DeepMind.com/Blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/AlphaEvolve.pdf)  
**Blog:** [DeepMind Announcement](https://deepmind.google/discover/blog/alphaevolve-a-gemini-powered-coding-agent-for-designing-advanced-algorithms/)  

**Summary:** AlphaEvolve is a system that leverages LLMs to iteratively improve a code that solves a problem. They find that for mathematical problems it works better to optimize the code that will find the solution (such as an heuristic search) than trying to find the solution directly. 

It has 4 components:
1. Prompt optimization 
2. Automated evaluation functions 
3. A database with the code instances generated + the evaluation feedback 
4. An ensamble of LLMs that direct the code evolution 

System workflow:
1. A human creates an initial prompt with problem definition + examples + initial code to evolve 
2. LLMs propose changes to the code 
3. The code is evaluated and both the code and the results are added to a Data Base 
4. The codes to evolve for the next concurrent iterations are selected from the DB using MAP elites algorithm and island-base population models 
5. An LLM is also asked to improve the current prompt
6. Back to step 2

They use this system to optimize 4x4 matrix multiplications, kernel operations, computer center resource managing systems, TPU design, etc.

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
