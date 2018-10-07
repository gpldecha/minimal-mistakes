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

## Notation

|  variable  |      dimension      |  name |
|----------|:-------------:|------|
| $$\mathbf{y}_i$$ | $$\mathbb{R}^{(M \times 1)}$$ | i*th* predictor|
| $$\mathbf{x}_i$$ | $$\mathbb{R}^{(P \times 1)}$$ | i*th* state    |
| $$\alpha_i$$ | $$\mathbb{R}^{(1 \times 1)}$$ | i*th* sample weight    |
| $$\mathbf{w}$$   | $$\mathbb{R}^{(P \times M)}$$ | weights  |
| $$\mathbf{Y}$$   | $$\mathbb{R}^{(N \times M)}$$ | all predictors    |
| $$\mathbf{X}$$   | $$\mathbb{R}^{(N \times P)}$$ | all states    |
| $$\boldsymbol{\alpha}$$   | $$\mathbb{R}^{(N \times N)}$$ | identity matrix with columns entries being data point weights  |


## Weighted Gaussian Linear regression

The log-likelihood of dataset with $$N$$ weighted samples  $$\mathcal{D} = \{\mathbf{x}_i, \mathbf{y}_i, \alpha_i \}_{i=1:N} $$ which is modeled by a linear gaussian function is given by:

<center>
$$L(\mathcal{D};\boldsymbol{\theta}) \triangleq \sum_{i=1}^N \log p(\mathbf{y}_i|\mathbf{x}_i;\boldsymbol{\theta}) \, \alpha_i$$
</center>

where $$p(\cdot)$$ is a Gaussian probability density function:

$$p(\mathbf{y}_i|\mathbf{x}_i;\boldsymbol{\theta}) = \frac{1}{(2\pi)^{D/2}|\boldsymbol{\Sigma}|^{1/2}} \exp\Bigg(-\frac{1}{2} (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)^{T}\boldsymbol{\Sigma}^{-1}(\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i) \Bigg)$$

with parameters $$\boldsymbol{\theta} \triangleq \{\mathbf{w}, \boldsymbol{\Sigma}\}$$.

### Expansion of the log-likelihood

First without considering the weights $$\alpha$$ we simplify $$L(\mathcal{D};\boldsymbol{\theta})$$

$$\begin{align}
&=\sum_{i=1}^N \log 1 - \log( (2\pi)^{D/2}|\boldsymbol{\Sigma}|^{1/2}) - \frac{1}{2} (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)^{T}\boldsymbol{\Sigma}^{-1}(\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i) \\
&=\sum_{i=1}^N - \frac{1}{2}\log((2\pi)^{D}|\boldsymbol{\Sigma}|) - \frac{1}{2} (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)^{T}\boldsymbol{\Sigma}^{-1}(\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i) \\
&=\sum_{i=1}^N - \frac{1}{2}\log((2\pi)^{D}) - \frac{1}{2}\log |\boldsymbol{\Sigma}| - \frac{1}{2} (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)^{T}\boldsymbol{\Sigma}^{-1}(\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)\\
&= \sum_{i=1}^N - \frac{D}{2}\log(2\pi) - \frac{1}{2}\log |\boldsymbol{\Sigma}| - \frac{1}{2} (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)^{T}\boldsymbol{\Sigma}^{-1}(\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i) \\
&= -\frac{N\,D}{2}\log(2\pi) - \frac{N}{2}\log |\boldsymbol{\Sigma}| - \frac{1}{2} \sum_{i=1}^N (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)^{T}\boldsymbol{\Sigma}^{-1}(\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)
\end{align}$$


Simplifying with the weights:

$$\begin{align}
&= \sum_{i=1}^N - \frac{D}{2}\log(2\pi)\alpha_i - \frac{1}{2}\log |\boldsymbol{\Sigma}|\alpha_i - \frac{1}{2} (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)^{T}\boldsymbol{\Sigma}^{-1}(\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i) \alpha_i\\
&= - \frac{D}{2}\log(2\pi)\left(\sum_{i=1}^N \alpha_i\right) - \frac{1}{2}\log |\boldsymbol{\Sigma}|\left(\sum_{i=1}^N \alpha_i\right) - \frac{1}{2} \sum_{i=1}^N (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)^{T}\boldsymbol{\Sigma}^{-1}(\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i) \alpha_i \end{align}$$

## 1D Maximum likelihood

Given that we are in the 1D case $$\boldsymbol{\Sigma} = \sigma$$, $$D=1$$

$$\begin{align}
&L(\mathcal{D};\boldsymbol{\theta}) = \\
&-\frac{1}{2}\log(2\pi)\left(\sum_{i=1}^N \alpha_i\right) - \frac{1}{2}\log \sigma^2 \left(\sum_{i=1}^N \alpha_i\right) - \frac{1}{2\, \sigma^2} \sum_{i=1}^N (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)^{T}\boldsymbol{\Sigma}^{-1}(\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i) \alpha_i\\
 &= - \frac{1}{2}\log(2\pi \sigma^2)\left(\sum_{i=1}^N \alpha_i\right) - \frac{1}{2\, \sigma^2} \sum_{i=1}^N (y - \mathbf{w}^{T}\mathbf{x}_i)^2\alpha_i
 \end{align}$$

Set the derivaties with respect to the parameters to zero, $$ \frac{\partial L}{\partial \mathbf{w}} = 0$$ and $$ \frac{\partial L}{\partial \sigma^2} = 0 $$,  and solve for $$\mathbf{w}$$ and $$\sigma^2$$:

### maximise weights

$$\frac{\partial L}{\partial \mathbf{w}} = \frac{1}{2\, \sigma^2} \sum_{i=1}^N \frac{\partial}{\partial \mathbf{w}} (y_i - \mathbf{w}^{T}\mathbf{x}_i)^2\alpha_i$$


$$\begin{align}
 0 &= \frac{1}{2\, \sigma^2} \sum_{i=1}^N - 2\, (\mathbf{Y}_i - \mathbf{w}^{T}\mathbf{x}_i)\, \mathbf{x}_i\, \alpha_i\\
 0 &= \sum_{i=1}^N - \, (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)\, \mathbf{x}_i\, \alpha_i\\
 0 &= -\sum_{i=1}^N  \mathbf{y}_i\, \mathbf{x}_i\, \alpha_i +  \sum_{i=1}^N \mathbf{w}^{T}\mathbf{x}_i\, \mathbf{x}_i\, \alpha_i \\
 0 &= -\mathbf{X}^{T}\boldsymbol{\alpha}\mathbf{Y} +  \mathbf{w} \mathbf{X}^{T}\boldsymbol{\alpha}\mathbf{X}\\
 \mathbf{w} \mathbf{X}^{T}\boldsymbol{\alpha}\mathbf{X} &= \mathbf{X}^{T}\boldsymbol{\alpha}\mathbf{Y}\\
 \mathbf{w} &= (\mathbf{X}^{T}\boldsymbol{\alpha}\mathbf{X})^{-1}\mathbf{X}^{T}\boldsymbol{\alpha}\mathbf{Y}
 \end{align}$$

### maximise variance

$$\begin{align}
\frac{\partial L}{\partial \sigma^2} &= \frac{\partial \left[-\frac{1}{2}\log(2\pi)\left(\sum_{i=1}^N \alpha_i\right) -\frac{1}{2}\log(\sigma^2)\left(\sum_{i=1}^N \alpha_i\right) - \frac{1}{2\, \sigma^2} \sum_{i=1}^N (\mathbf{y}_i - \mathbf{w}^{T}\mathbf{x}_i)^2\alpha_i\right]}{\partial \sigma^2}\\
&= -\frac{1}{2 \sigma^2}\left(\sum_{i=1}^N \alpha_i\right) + \frac{1}{2\, \sigma^4} \sum_{i=1}^N (\mathbf{y}_i  - \mathbf{w}^{T}\mathbf{x}_i)^2\alpha_i \\
0 &= -\left(\sum_{i=1}^N \alpha_i\right) + \frac{1}{\sigma^2} \sum_{i=1}^N (\mathbf{y}_i  - \mathbf{w}^{T}\mathbf{x}_i)^2\alpha_i\\
\sigma^2 \left(\sum_{i=1}^N \alpha_i\right) &= \sum_{i=1}^N (\mathbf{y}_i  - \mathbf{w}^{T}\mathbf{x}_i)^2\alpha_i \\
\sigma^2 &= \frac{1}{\left(\sum_{i=1}^N \alpha_i\right)} \sum_{i=1}^N (\mathbf{y}_i  - \mathbf{w}^{T}\mathbf{x}_i)^2\alpha_i
\end{align}
$$
