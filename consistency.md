# LLM consistency/robustness

### Aligning with Logic: Measuring, Evaluating and Improving  Logical Preference Consistency in Large Language Models
![log_pref_cons.png](images/log_pref_cons.png)

In this paper they measure three types of logical consistency:
- Transitivity: If A > B and B > C, then A > C
- Commutativity: If A > B, then B < A
- Negation conflict: If A > B then not(B > A)

In this context, the relation > is the preference of one answer over the other, so if the preference graph has cycles, it implies that the model has logical inconsistencies.

They propose metrics for each logical consistency type, and propose REPAIR, a method that generates a pairwise dataset to improve logical consistency. 

It uses a datasets that focus on choosing between two answers, and then uses loss rate method to solve the rank aggregation problem. (If A wins to B, C and D, but losses to E and F, the score for A will be (win-loss)/total = (3-2)/5 = 0.2)

Results found that:
- "Zero-shot inference shows considerable logical inconsistency."
- Commutativity correlates strongly with human preferences (they also compared model outputs with the dataset labels)
- "Surprisingly, CoT reasoning did not generally improve consistency, and in some cases, it led to a decrease in transitivity performance"
- Training with REPAIR improves transitivity and commutativity

---

### Multidimensional Consistency Improves Reasoning in Language Models
This paper studies consistency on LLMs by making changes to the prompt (no training is performed)

They work with three types of consistency:
- Language (CLC) -> Changing language effects performance on QA/Math benchmarks.
- Paraphrasing (CPC) -> Same question asked differently.
- Order consistency (COC) -> Few-shot changing the example order.

They calculate consistency by dividing the maximum number of equal answers divided by the total amount. 

Results:
-  Consistency scores are like this: order > paraphrasing > language.
- COC improves all models on GSM8K and MATH500, showing that aggregating across different few-shot orders is useful
- CPC is the strongest individual method overall. Rewriting the question and then solving it often helps, but using only the rewritten question can lose information.
- Combining dimensions helps more: aggregating across order, paraphrase, and language usually gives the best or near-best accuracy.
- COC and CPC strongly correlate with model accuracy, so they may be useful as confidence/uncertainty signals without needing the gold answer

---

### RoParQ: Paraphrase-Aware Alignment of Large Language Models Towards Robustness to Paraphrased Questions

This paper studies whether LLMs give consistent answers when the same multiple-choice question is paraphrased.

They introduce **RoParQ**, a benchmark made from MMLU, ARC, CommonsenseQA, and MathQA. Each question has three versions:

* Original
* Gemini paraphrase
* Claude paraphrase

They also propose **XParaCon**, a metric that measures how stable model accuracy is across paraphrases.
XParaCon is computed by first measuring the model accuracy for each question variant across 8 shuffled answer-choice orders:

- `acc(q_original)`
- `acc(q_gemini)`
- `acc(q_claude)`

Then, they compute the standard deviation of these three accuracies. If the model performs similarly across all paraphrases, the standard deviation is low. Finally, they average this value across all examples and apply `-log2`, so higher XParaCon means better paraphrase consistency.

They train models with a paraphrase-aware SFT method, where the model restates the question, creates a paraphrase, checks that the answer stays the same, and then answers.

Results found that:

* LLMs are sensitive to wording changes.
* Larger models are usually more robust.
* Claude 3.5 Sonnet had the strongest overall robustness.
* Paraphrase-aware fine-tuning improves consistency.
* Small fine-tuned models can become as robust as much larger pre-trained models.

### Enhancing Semantic Consistency of Large Language Models through Model Editing: An Interpretability-Oriented Approach

This paper studies **semantic consistency**: whether an LLM gives the same answer to prompts with the same meaning but different wording.

They propose an interpretability-based **model editing** method instead of using expensive fine-tuning.

Their method:

* Builds paraphrased prompt pairs using GPT-4.
* Finds model components, mainly attention heads and MLPs, that are related to consistency errors.
* Adds biases to those components in a direction that makes the model more semantically consistent.

They locate important components by training linear classifiers on each component’s hidden states. If a component can predict whether the model will be consistent or inconsistent, it is considered important.

The bias they add is computed as the difference between the average activation of **consistent samples** and the average activation of **all samples** for a selected component:

`bias = mean(consistent activations) - mean(all activations)`

Then, during inference, they edit the component by adding this direction to its activation:

`edited activation = original activation + α · bias`

So the model is pushed toward activation patterns associated with semantically consistent behavior.

They also introduce three NLU benchmarks:

* RobustSST2
* RobustMRPC
* RobustBOOLQ

Results found that:

* Middle-to-late layers are most related to semantic consistency.
* Editing selected components improves both consistency and accuracy.
* Random component editing or random editing directions hurt performance.
* The method generalizes reasonably well to out-of-domain tasks.
* SFT performs better overall, but model editing is much cheaper, using 12x to 23x fewer GPU hours.

The main takeaway is that semantic consistency can be improved by editing specific internal components of the model, not only by fine-tuning on paraphrases.

---

### Robustness in Large Language Models: A Survey of Mitigation Strategies and Evaluation Metrics
This paper review classifies robustness enhancing strategies in four types:

1. Pre-processing: Actions taken on the data before model training or fine-tuning begins (e.g., data cleaning, augmentation).  
2. In-processing: Modifications integrated during the model training or fine-tuning process (e.g., robust optimization, adversarial training, alignment techniques).  
3. Intra-processing: Techniques applied during the model’s inference or generation phase (e.g., robust prompting, modified decoding, inference-time adaptation).  
4. Post-processing: Methods applied after the model generates an output, but before it is presented to the user or used downstream (e.g., output filtering, validation, using a judge model).

---

### Information-consistent language model recommendations through group relative policy optimization
They apply GRPO to consistency.
To do that they use two loss functions:
#### 1. For helpfulness they use the Shannon entropy formula:
$$
H(r) = -\sum_v p(v) \log p(v)
$$
They state that "Higher entropy indicates information-rich, complete responses."

And they normalize it:
$$
H_{\text{norm}}(r) = \frac{H(r) - H_{\min}}{H_{\max} - H_{\min}}
$$

#### 2. For consistency they use the entropy gap of two semantically equivalent prompts:

$$
\text{Gap} = \left|H(r^a) - H(r^b)\right|
$$

"A normalized stability score $F_{norm} \in [0,1]$ is obtained by scaling and inverting this gap (smaller gaps -> higher stability).

For a group \(G\) of size \(K\), the aggregate stability measure is:

$$F_{\mathrm{norm}} = 1 - \frac{1}{K}\sum_{k=1}^{K}\frac{\left|H(r(q_k^{(i)}))-H(r(q_k^{(j)}))\right|}{\mathrm{MAX\_GAP}}.$$

Here, MAX_GAP is the maximum difference between the entropies of the two groups."

Then they use alpha an beta variables to do a wheighted sum of both formulas.

---

### Consistency in Language Models: Current Landscape, Challenges, and Future Directions

#### Types of Consistency

##### 1. Logical Consistency

Refers to consistency based on formal logical relationships, including:

* Negational consistency
* Symmetric consistency
* Transitive consistency
* Additive consistency

##### 2. Semantic Consistency

The ability of a model to make consistent decisions across semantically equivalent contexts.

##### 3. Nonlogical or Informal Consistency

Covers definitions of consistency that do not follow the rules of formal logic.

##### 4. Factual Consistency

The ability of a model to generate new information without contradicting the source document.

##### 5. Self-Consistency

Examines whether similar inputs produce consistent explanations or outputs.

##### 6. Faithfulness

Evaluates whether the generated text accurately reflects the model’s actual reasoning process.

#### Future Research Directions

* **Multilingual consistency**
* **Cross-lingual consistency**
* **Consistency evaluation**
* **Improving consistency**
* **Structural foundations of consistency**
* **Representational spaces**
* **Consistency-oriented pre-training**
* **Architectures designed to maintain consistency across diverse contexts**

---

### Metamorphic Testing of Large Language Models for Natural Language Processing

This paper studies whether **metamorphic testing (MT)** can detect inconsistent LLM behavior without needing a labelled correct answer for every input.

The authors review 44 studies and collect 191 metamorphic relations, then introduce **LLMORPH**, a framework that implements 36 of them. **LLMORPH** uses two methods to generate extra data: function-based and LLM-based. The first is programmed modification, such as adding a random phrase at the end of the prompt or adding keyboard mistakes (NLPAug library). And the seccond uses an LLM to generate paraphrasings.
As evaluation tasks they used question answering with context (QAc), natural language inference (NLI), sentiment analysis (SA), and relation extraction (RE).

A metamorphic relation defines how an output should change or remain the same after modifying the input. For example, paraphrasing a question should usually preserve the answer. If the output changes unexpectedly, the model may be inconsistent.

They test GPT-4, Llama 3.1, and Hermes 2 on four NLP tasks, running about 561,000 tests.

The general workflow is as the follows:
Get data QA -> Do data augmentation -> Do Metamorphic testing -> Evaluate output distances (Using BERT)

Results found that:

- The average violation rate was **18%**.
- MT found faults missed by traditional labelled testing.
- About **62%** of manually checked violations were genuine faults.
- False positives often came from poor transformations or difficulty comparing free-form answers.
- Results depended more on the task and relation than on the model.
- Model randomness was not the main cause of failures.

The main takeaway is that MT is a useful low-cost complement to labelled benchmarks, but false positives remain a major limitation.

---

| Title                                                                                           | Verified year | Publication site                                                                                                                                                        |
| ----------------------------------------------------------------------------------------------- | ------------: | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Consistency in Language Models: Current Landscape, Challenges, and Future Directions            |          2025 | [ICML 2025 Workshop on Reliable and Responsible Foundation Models — OpenReview](https://openreview.net/forum?id=ejvvhJZJSf)                                             |
| Internal Consistency and Self-Feedback in Large Language Models: A Survey                       |          2024 | [arXiv](https://arxiv.org/abs/2407.14507) — no formal venue verified                                                                                                    |
| Bidirectional Empowerment of Metamorphic Testing and Large Language Models: A Systematic Survey |          2026 | [arXiv](https://arxiv.org/abs/2605.13898) — no ACM publication record verified                                                                                          |
| Evaluating and Improving Robustness in Large Language Models: A Survey and Future Directions    |          2025 | [arXiv](https://arxiv.org/abs/2506.11111) — no formal venue verified                                                                                                    |
| Self-Consistency Improves Chain-of-Thought Reasoning in Language Models                         |          2023 | [International Conference on Learning Representations — ICLR 2023](https://openreview.net/forum?id=1PL1NIMMrw)                                                          |
| BECEL: Benchmark for Consistency Evaluation of Language Models                                  |          2022 | [29th International Conference on Computational Linguistics — COLING 2022](https://aclanthology.org/2022.coling-1.324/)                                                 |
| Semantic Consistency for Assuring Reliability of Large Language Models                          |          2023 | [arXiv](https://arxiv.org/abs/2308.09138) — no formal venue verified                                                                                                    |
| ProSA: Assessing and Understanding the Prompt Sensitivity of LLMs                               |          2024 | [Findings of EMNLP 2024](https://aclanthology.org/2024.findings-emnlp.108/)                                                                                             |
| What Did I Do Wrong? Quantifying LLMs’ Sensitivity and Consistency to Prompt Engineering        |          2025 | [NAACL 2025 — Long Papers](https://aclanthology.org/2025.naacl-long.73/)                                                                                                |
| Metamorphic Testing of Large Language Models for Natural Language Processing                    |          2025 | [IEEE International Conference on Software Maintenance and Evolution — ICSME 2025](https://www.computer.org/csdl/proceedings-article/icsme/2025/958700a174/2bgg0S2ty00) |
| Self-Consistency of Large Language Models under Ambiguity                                       |          2023 | [BlackboxNLP 2023](https://aclanthology.org/2023.blackboxnlp-1.7/)                                                                                                      |
| Evaluating Robustness of LLMs to Numerical Variations in Mathematical Reasoning                 |          2025 | [Sixth Workshop on Insights from Negative Results in NLP](https://aclanthology.org/2025.insights-1.16/)                                                                 |
| Metamorphic Testing for Semantic Invariance in Large Language Models                            |          2025 | [IEEE Access](https://ieeexplore.ieee.org/document/11305018)                                                                                                            |
| **Towards** Reasoning in Large Language Models: A Survey                                        |      **2023** | [Findings of ACL 2023](https://aclanthology.org/2023.findings-acl.67/)                                                                                                  |
| The Prompt Report: A Systematic Survey of Prompting Techniques                                  |          2024 | [arXiv](https://arxiv.org/abs/2406.06608) — no formal venue verified                                                                                                    |
| Language Model Behavior: A Comprehensive Survey                                                 |          2024 | [Computational Linguistics, volume 50, issue 1 — MIT Press](https://direct.mit.edu/coli/article/50/1/293/118131/Language-Model-Behavior-A-Comprehensive-Survey)         |
