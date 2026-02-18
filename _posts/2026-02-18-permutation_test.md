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
During my data science internship, I worked on a classification task in a medical dataset where positive cases 
were severely underrepresented. Our model looked great on paper — until I realised the accuracy score was 
mostly a reflection of the class distribution, not of anything the model had actually learned. 
That experience led me to the permutation test: a simple but powerful way to ask whether your model 
is genuinely doing something meaningful, or just getting lucky with the numbers.
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

