## 🧪 Distillation

### 2020 — DistilBERT: A Distilled Version of BERT (Sanh et al.)
**Summary:** Loss from language modeling, distillation, and cosine-distance. 40% less size retaining 97% of capabilities.

---

### 2024 — A Survey on Knowledge Distillation of Large Language Models
**Paper:** [arXiv 2402.13116](https://arxiv.org/pdf/2402.13116)  
**Summary:** TODO

---

### 2024 — A Survey on Symbolic Knowledge Distillation of Large Language Models
**Paper:** [IEEE](https://www.researchgate.net/publication/383266933_A_Survey_on_Symbolic_Knowledge_Distillation_of_Large_Language_Models/fulltext/66c56bc82fec7d516b5c558c/A-Survey-on-Symbolic-Knowledge-Distillation-of-Large-Language-Models.pdf?_tp=eyJjb250ZXh0Ijp7ImZpcnN0UGFnZSI6InB1YmxpY2F0aW9uIiwicGFnZSI6InB1YmxpY2F0aW9uIn19)  
**Summary:** TODO

---

### June 2024 — Reinforcement Learning Teachers at Test Time Scaling (Sakana AI)
**Paper:** [arXiv 2506.08388](https://www.arxiv.org/pdf/2506.08388)  
**Blog:** [Sakana AI](https://sakana.ai/rlt/)  

**Summary:**  
- **Shifting paradigm:** Focus on teaching, not just problem-solving, enabling the use of smaller, specialized teacher models.  
- **Efficiency & accessibility:** Enables effective reasoning pipelines with lower compute, faster iteration, and improved student models.

---

### November 2024 — Learning with Less: Knowledge Distillation from Large Language Models via Unlabeled Data
**Paper:** [arXiv](https://arxiv.org/abs/2411.08028)  

**Summary:**  
Text classification with data curation. Seeks high teacher confidence (maxarg prob) and high student uncertainty (output entropy) to improve pseudo-label accuracy and data usefulness for the student respectively.  

The threshold is computed using moving averages and a manual adjustment for each label (some classifications are easier than others).  

This technique (LLKD) improves accuracy and reduces computation needed for fine-tuning.
