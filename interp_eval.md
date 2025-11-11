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

$$ G_{\text{abs}}(A_c, A_n) = \left| 2 \cdot \left( \frac{\sum_{a_{c} \in A_c} \sum_{a_{n} \in A_n} \textbf{1}_{[a_{c} < a_{n}]}}{\|A_c\|_0 \cdot \|A_n\|_0} \right) - 1 \right| $$

