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

### Can Large Language Models Invent Algorithms to Improve Themselves?:Algorithm Discovery for Recursive Self-Improvement through Reinforcement Learning

**Paper:** [arXiv](https://arxiv.org/abs/2410.15639)

**Summary:** 
The objective is to iteratively improve a base model by merging it with fine-tuned versions. The contribution is that another SLM is in charge of creating the new merging strategies. 
The loop goes as follows:
1. Programming model creates a merging algorithm 
2. Base model is merged with fine-tuned versions of the same model
3. Resulting model is evaluated with two benchmarks 
4. The benchmark results and the merging code is used to create preference data and train the programming model with DPO 
5. Go back to step 1 

What are task vectors?? The weights generated during the training of the LoRA fine tunning. 

---

### Darwin Godel Machine: Open-Ended Evolution of Self-Improving Agents
**Paper:** [arXiv](https://arxiv.org/abs/2505.22954) 

**Summary:** 
They say that improving coding capabilities = learning to improve itself, but I disagree. To make breakthroughs, intuition and knowledge are way more necessary than coding skills.

The system they propose consists in a loop of improvement of the code base that uses closed models to perform programming tasks. They prompt the model to improve both the tools (bash access and edit tool) used and the workflow (such as iterative problem solving and retries, history-aware generation and context management).
They evaluate all this with some open-source benchmarks and create a DB that the next prompts will use.

NOTE: The title is misleading, there is no self-improving agents, and the evolution of the system that uses the frozen Foundational Models is quite closed. Also, the paper is super repetitive and the writing is verbose. I suspect LLMs have been really involved in the writing. 

---

### Mitigating Tail Narrowing in LLM Self-Improvement via Socratic-Guided Sampling

**Paper:** [arXiv](https://arxiv.org/abs/2411.00750)

**Summary:** Self-improvement techniques consist on making the model generate synthetic data that then will be used to continue training the model.
But due to the Tail Narrowing effect, in which the model only gets better at the things it already knows how to do, the improvement stops at some near point. To mitigate this issue, the paper proposes to guide the synthetic data generation, to make the model more likely to create useful and correct data.

They make it with 4 approaches, they already have a dataset with reasoning paths and answers:
1. Providing the final answer to the model and letting it create the reasoning.
2. Providing the reasoning and letting the model generate the final answer.
3. Provide only a portion of the reasoning path, making the model complete it and generating the answer
4. When the model fails, a bigger model is prompted to explain the correction, and the inference is re-executed with the new info.

This methods are compared with SFT with the dataset and with the vanilla Self-Improvement implementation.
Results show that when the fine-tuning is done with 3, the results in the evaluation benchmarks (that are different than the ones used for the fine-tuning) show that 3 works better in general, and that 1 fails when the model do not have enough reasoning capabilities.  

---

### Self-Consuming Generative Models Go MAD

**Paper:** https://openreview.net/forum?id=ShjMHfmPs0
