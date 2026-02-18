---
layout: default
title: "Permutation Test on imbalanced group sets"
date: 2026-02-18
permalink: /blog/permutation-test/
description: "How to use permutation tests to determine if your classifier has learned a real signal on imbalanced medical datasets."
---

## Permutation Tests on imbalanced group sets

*February 18, 2026*

---

<p style="font-size: 0.88em; font-style: italic; color: #555; line-height: 1.7;">
While working on a lab dataset, I was trying to determine whether multiple groups share the same chemical properties. 
I tried different statistical tests, to show that my groups were equivalent based on multiple features. 
The tests failed due to some features suffering from heteroscedasticity or being undersampled. 
Permutation test is an assumption-free choice, more reliable on small datasets than asymptotic tests.
</p>

---

---

### Permutation Test 


<div class="math-definition">
  <div class="def-title">(Definition) Permutation Test</div>
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

