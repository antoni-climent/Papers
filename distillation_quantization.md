## 🧪 Distillation and quantization

### 2020 — DistilBERT: A Distilled Version of BERT

**Paper:** [arXiv](https://arxiv.org/abs/1910.01108)
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

### uDistil-Whisper: Label-Free Data Filtering for Knowledge Distillation in Low-Data Regimes

**Paper:** https://arxiv.org/abs/2407.01257
**Summary:** TODO

### Self-calibration for Language Model Quantization and Pruning

**Paper:** https://arxiv.org/abs/2410.17170
**Summary:** Quantization and pruning algorithms need data that is aligned with the distribution of the model.
Usually we do not have access to the training data, so they propose to sample the original model to create synthetic one.
They prompt the model with the <init> token and let it generate until the <end> token or if a max num is reached.
General knowledge benchmarks are used to test different quantization and pruning techniques, using also different dataset baselines: From web data and synthetic data generated with a bigger model.
Results show that:

1. Self-generated synthetic data normally outperforms other datasets.
2. Self-generated data is less diverse, but more coherent than other baselines.
3. Temperature in generation does not have a huge impact, so using the normal T=1 is fine.

### HIGGS: Pushing the Limits of Large Language Model Quantization via the Linearity Theorem

**Paper:** https://arxiv.org/abs/2411.17525
**Summary:** TODO
