---
title: "Weighted Gaussian Linear Regression"
layout: single
author_profile: false
excerpt: ""
header:
  overlay_color: "#333"
---

{% include base_path %}

<!-- KaTeX -->
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

## Resources

[Vandenberghe Lectures](http://www.seas.ucla.edu/~vandenbe/133A/lectures/ls.pdf)

## General derivation

The Gaussian probability density function of $$\mathbf{y}_i = \mathbf{w}^{T}\mathbf{x}$$ is:
$$p(\mathbf{y}_i|\mathbf{x};\boldsymbol{\theta}) = \frac{1}{(2\pi)^{D/2}|\boldsymbol{\Sigma}|^{1/2}} \exp\Bigg(-\frac{1}{2} (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x})^{T}\boldsymbol{\Sigma}^{-1}(\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}) \Bigg)$$

$$\boldsymbol{\theta} \triangleq \{\mathbf{w}, \boldsymbol{\Sigma}\}$$

which is the same the likelihood of a single data point.

For a data set of points weighted by values $$\boldsymbol{\alpha}$$ the log-likelihood is
defined as follows:

$$l(\boldsymbol{X}, \boldsymbol{\alpha}, \boldsymbol{\theta}) \triangleq \sum_{i=1}^N \log p(\mathbf{y}_i|\mathbf{x}_i;\boldsymbol{\theta}) \, \alpha_i$$

Simplifying first for the case with no $$\boldsymbol{\alpha}$$:

$$\sum_{i=1}^N \log 1 - \log( (2\pi)^{D/2}|\boldsymbol{\Sigma}|^{1/2}) - \frac{1}{2} (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)^{T}\boldsymbol{\Sigma}^{-1}(\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)$$


$$\sum_{i=1}^N - \frac{1}{2}\log((2\pi)^{D}|\boldsymbol{\Sigma}|) - \frac{1}{2} (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)^{T}\boldsymbol{\Sigma}^{-1}(\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)$$

$$\sum_{i=1}^N - \frac{1}{2}\log((2\pi)^{D}) - \frac{1}{2}\log |\boldsymbol{\Sigma}| - \frac{1}{2} (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)^{T}\boldsymbol{\Sigma}^{-1}(\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)$$

$$\sum_{i=1}^N - \frac{D}{2}\log(2\pi) - \frac{1}{2}\log |\boldsymbol{\Sigma}| - \frac{1}{2} (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)^{T}\boldsymbol{\Sigma}^{-1}(\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)$$

$$ - \frac{N\,D}{2}\log(2\pi) - \frac{N}{2}\log |\boldsymbol{\Sigma}| - \frac{1}{2} \sum_{i=1}^N (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)^{T}\boldsymbol{\Sigma}^{-1}(\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)$$

Simplifying first for the case with  $$\boldsymbol{\alpha}$$:

$$\sum_{i=1}^N - \frac{D}{2}\log(2\pi)\alpha_i - \frac{1}{2}\log |\boldsymbol{\Sigma}|\alpha_i - \frac{1}{2} (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)^{T}\boldsymbol{\Sigma}^{-1}(\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i) \alpha_i$$

$$ - \frac{D}{2}\log(2\pi)\left(\sum_{i=1}^N \alpha_i\right) - \frac{1}{2}\log |\boldsymbol{\Sigma}|\left(\sum_{i=1}^N \alpha_i\right) - \frac{1}{2} \sum_{i=1}^N (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)^{T}\boldsymbol{\Sigma}^{-1}(\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i) \alpha_i$$

## 1D derivation

$$ - \frac{1}{2}\log(2\pi)\left(\sum_{i=1}^N \alpha_i\right) - \frac{1}{2}\log \sigma^2 \left(\sum_{i=1}^N \alpha_i\right) - \frac{1}{2\, \sigma^2} \sum_{i=1}^N (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)^{T}\boldsymbol{\Sigma}^{-1}(\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i) \alpha_i$$

$$ l = - \frac{1}{2}\log(2\pi \sigma^2)\left(\sum_{i=1}^N \alpha_i\right) - \frac{1}{2\, \sigma^2} \sum_{i=1}^N (y - \mathbf{w}^{T}\mathbf{x}_i)^2\alpha_i$$

### MLE

$$\frac{\partial l}{\partial \mathbf{w}} = \frac{1}{2\, \sigma^2} \sum_{i=1}^N \frac{\partial}{\partial \mathbf{w}} (y_i - \mathbf{w}^{T}\mathbf{x}_i)^2\alpha_i$$

$$ 0 = \frac{1}{2\, \sigma^2} \sum_{i=1}^N - 2\, (y_i - \mathbf{w}^{T}\mathbf{x}_i)\, \mathbf{x}_i\, \alpha_i$$

$$ 0 = \sum_{i=1}^N - 2\, (y_i - \mathbf{w}^{T}\mathbf{x}_i)\, \mathbf{x}_i\, \alpha_i$$

$$ 0 = \sum_{i=1}^N - 2 y_i\, \mathbf{x}_i\, \alpha_i -  \sum_{i=1}^N \mathbf{w}^{T}\mathbf{x}_i\, \mathbf{x}_i\, \alpha_i$$
