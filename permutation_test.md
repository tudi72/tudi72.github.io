---
layout: default
title: "Assessing Models on Imbalanced Datasets Using Permutation Tests"
date: 2026-02-18
permalink: /blog/permutation-test/
---

## Assessing Models on Imbalanced Datasets Using Permutation Tests

*February 18, 2026*

---

When building machine learning models in medicine or biology, imbalanced datasets are the norm rather than the exception. 
A cancer detection model might see 95% healthy patients and only 5% positive cases. A naive classifier that predicts 
"healthy" for everyone achieves 95% accuracy — and is completely useless. So how do we know if our model has actually 
learned something meaningful, or if it is just exploiting the class distribution? One principled answer is the 
**permutation test**.

---

---

### Formal Definition

<div class="math-definition">
  <div class="def-title">Definition — Permutation Test</div>
  <p>
    Let \( S(\mathbf{X}, \mathbf{y}) \) be a scoring function (e.g. balanced accuracy) 
    for a model trained on feature matrix \( \mathbf{X} \in \mathbb{R}^{n \times p} \) 
    and label vector \( \mathbf{y} \in \{0, 1\}^n \). 
    The permutation p-value is defined as:
  </p>

  $$
  p = \frac{1}{B} \sum_{b=1}^{B} \mathbf{1}\left[ S(\mathbf{X}, \pi_b(\mathbf{y})) \geq S(\mathbf{X}, \mathbf{y}) \right]
  $$

  <p>
    where \( \pi_b \) is the \( b \)-th random permutation of the label vector, 
    and \( B \) is the total number of permutations.
  </p>
</div>

---

### The Null Hypothesis

The permutation test evaluates:

$$
H_0: \quad S(\mathbf{X}, \mathbf{y}) \overset{d}{=} S(\mathbf{X}, \pi(\mathbf{y}))
$$

That is, under the null hypothesis the score is **distributionally equivalent** 
to what is obtained under random label assignment. We reject $H_0$ when $p < \alpha$, 
typically $\alpha = 0.05$.

---

### Balanced Accuracy

For imbalanced datasets, the preferred scoring function is balanced accuracy:

$$
\text{BA} = \frac{1}{2}\left( \frac{TP}{TP + FN} + \frac{TN}{TN + FP} \right)
= \frac{\text{Sensitivity} + \text{Specificity}}{2}
$$

Under pure chance with a class imbalance ratio $r = n_+ / n$, 
the expected balanced accuracy is always:

$$
\mathbb{E}[\text{BA}] = 0.5 \quad \forall\, r \in (0, 1)
$$

This is why balanced accuracy is a fair baseline metric regardless of imbalance.

---

### The Empirical Null Distribution

After $B$ permutations, we estimate the null distribution of scores 
$\{ s_1, s_2, \ldots, s_B \}$ where each $s_b = S(\mathbf{X}, \pi_b(\mathbf{y}))$. 
The empirical cumulative distribution function is:

$$
\hat{F}_0(t) = \frac{1}{B} \sum_{b=1}^{B} \mathbf{1}[s_b \leq t]
$$

The p-value for the observed score $s^* = S(\mathbf{X}, \mathbf{y})$ is then:

$$
p = 1 - \hat{F}_0(s^*) = P\left(s_b \geq s^* \mid H_0\right)
$$