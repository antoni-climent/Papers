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
