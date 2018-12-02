---
title: "Reinforcement learning an introduction"
layout: single
author_profile: false
excerpt: "Excercies of the the book."
header:
  overlay_color: "#333"
---
{% include base_path %}

<!-- KaTeX -->
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>


### Exercise 2.9

Demonstration that the soft-max distribution is equal to the logistic
and sigmoid distribution for the case of two actions.

First we show that the soft-max is a logistic function.
$$\begin{align}
 Pr(A = a_1) &= \frac{\exp H_t(a_1)}{ \exp H_t(a_0) +  \exp H_t(a_1)} \\
             &= \frac{\exp \left( H_t(a_1) -  H_t(a_0) \right)}{ \exp \left(H_t(a_0) - H_t(a_0)\right)  +  \exp \left( H_t(a_1) -  H_t(a_0) \right)} \\
             &= \frac{\exp \left( H_t(a_1) -  H_t(a_0) \right)}{ 1 +  \exp \left( H_t(a_1) -  H_t(a_0) \right)}
\end{align}
$$

Secondly, a sigmoid function refers to the special case of the logistic
function. From the following relation

$$
 f(x) = \frac{\exp(x)}{1 + \exp(x)} =  \frac{1}{1 + \exp(-x)}
$$

it is clear that the logistic function is also a sigmoid function.

### Exercise 2.10

| case | $$q(a_1)$$ |  $$q(a_2)$$ | $$P(X)$$ |
|----|----|----|----|
|  A | 0.1 | 0.2 | $$P(A) = 0.5$$ |
|  B | 0.9 | 0.8 | $$P(B) = 0.5$$ |


If you are not able to tell which case you face at any step, what is the best expectation of success you can achieve and how should you behave to achieve it.

Allways choose action

a1

$$\mathbb{E}_{P}[q|a_1] = P(A)q(a_1|A) + P(B)q(a_1|B) = 0.5$$

a2

$$\mathbb{E}_{P}[q|a_2] = P(A)q(a_2|A) + P(B)q(a_2|B) = 0.5$$

Either choosing $$a_1$$ or $$a_1$$ leads to the same expected value.
