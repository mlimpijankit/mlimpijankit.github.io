---
layout: note
---

<style>
@import url('https://cdn.jsdelivr.net/npm/computer-modern@0.1.2/cmu-serif.css');

body {
  font-family: 'Computer Modern Serif', serif !important;
}
</style>

## <span style="color:#b4321e">Interptability Evaluation</span>

### FADE - Why Bad Descriptions Happen to Good Features ###
Puri, B., Jain, A., Golimblevskaia, E., Kahardipraja, P., Wiegand, T., Samek, W., & Lapuschkin, S. (2025).

Introduces a framework for evaluating feature-description alignment based on multiple aspects.

**Clarity**: is the feature's description precise enough to generate strongly activating samples? 

Prompt evaluator LLM to generate synthetic samples based on the description $A_{c}$, and sample uniformly from the natural dataset $A+{n}$. Measure separability using absolute Gini coefficient,

$$ G_{\text{abs}}(A_c, A_n) = \left| 2 \cdot \left( \frac{\sum_{a_{c} \in A_c} \sum_{a_{n} \in A_n} \textbf{1}_{[a_{c} > a_{n}]}}{\|A_c\|_0 \cdot \|A_n\|_0} \right) - 1 \right| $$

**Responsiveness**: difference between activations for concept vs. non-concept samples. Sample high and low activations from the dataset, prompt an evaluator LLM to judge 0 = not expressed, 1 = partially expressed, 2 = clearly expressed, remove samples with label 1. Calculate absolute Gini coefficient as above (difference is now using natural samples and the LLM labels as concept vs. non-concept).

**Purity**: using the same set of samples above, calculate purity using Average Precision (AP). The focus is whether strong activations are exclusive to the target concept.

$$ AP(A_{c}, A_{n}) = \sum_{j} (r_{j} - r_{j-1}) \cdot p_{j} $$

where $r_{j}$ is the recall, $p_{j}$ is the precision computed at threshold $j$ for each possible threshold based on $A_{c}$ and $A_{n}$.

**Faithfulness**:

Try multiple modifications on the concept (i.e., multiply the concept by a constant factor) and store the output. Below, R is a vector of the proportion of concept-related outputs for each modification, $R_{0}$ is the baseline where the feature is entirely "zeroed out". If the score is 1, that means manipulating the concept (i.e., some addition of the feature) always results in that feature being in the output.

$$\[ \text{Faithfulness}(\mathbf{R}) = \frac{\max(\max(\mathbf{R}) - R_0, 0)}{1 - R_0} \]$$

