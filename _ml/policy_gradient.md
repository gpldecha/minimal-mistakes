---
title: "Policy gradient notes"
layout: single
author_profile: false
excerpt: "Derivation of principals underlying policy gradient methods"
header:
  overlay_color: "#333"
---
{% include base_path %}

<!-- KaTeX -->
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

## Resources

[Policy gradient methods for robotics ](http://www.1-4-5.net/~dmm/ml/policy_gradient_methods_for_robotics.pdf)
[arg min blog: a blog of minimum value](http://www.argmin.net/)

## Notation

|  variable  |      dimension      |  name |
|----------|:-------------:|------|
| $$\tau$$ | $$s_0, u_0, \dots, s_{H-1}, u_{H-1}$$ | trajectory |
| $$p(s_{t+1}\|s_t, u_t)$$ | $$\mathbb{R}$$ | state transition  dynamical model |
| $$\pi_{\theta}(u_t\|s_t)$$ | $$\mathbb{R}$$ | policy |
| $$P_{\theta}(\tau)$$ | $$p(s_0)\prod_{t=0}^{H-1} p(s_{t+1}\|s_t, u_t)\, \pi_{\theta}(u_t\|s_t)$$ | probability of a trajectory |
| $$ R(\tau)$$ | $$\sum_{t=0}^{H-1} r(s_t, u_t)$$ | Utility of a trajectory |



## Policy  gradient likelihood ratio

We seek to maximise the expected reward:

$$\begin{align}
 J(\theta) &= \mathbb{E}_{\tau \sim P_{\theta}}\left[ R(\tau) \right] \\
           &= \sum_{\tau} P_{\theta}(\tau) R(\tau) \\
\end{align}$$


We can derive an expresion of the gradient of the above objective function which
is **independent** of the state transition model $$p(s_{t+1}|s_t, u_t)$$ and only depends
on the policy.

$$\begin{align}
    \nabla_{\theta} J(\theta) &=  \sum_{\tau}   \nabla_{\theta} P_{\theta}(\tau) R(\tau) \\
    &=  \sum_{\tau} P_{\theta}(\tau) \frac{\nabla_{\theta} P_{\theta}(\tau)}{P_{\theta}(\tau)} R(\tau) \\
    &= \sum_{\tau} P_{\theta}(\tau) \nabla_{\theta} \log P_{\theta}(\tau) R(\tau) \\
    &= \sum_{\tau} P_{\theta}(\tau)  \nabla_{\theta} \log \left( p(s_0)\prod_{t=0}^{H-1} p(s_{t+1}|s_t, u_t)\, \pi_{\theta}(u_t|s_t) \right) R(\tau) \\
    &= \sum_{\tau} P_{\theta}(\tau)  \nabla_{\theta} \left( \log p(s_0) + \sum_{t=0}^{H-1} \log p(s_{t+1}|s_t, u_t) + \log \pi_{\theta}(u_t|s_t) \right) R(\tau) \\
    &= \sum_{\tau} P_{\theta}(\tau)   \left(\sum_{t=0}^{H-1} \nabla_{\theta} \log \pi_{\theta}(u_t|s_t) \right) R(\tau)\\
    &= \mathbb{E}_{\tau \sim P_{\theta}}\left[ \left(\sum_{t=0}^{H-1} \nabla_{\theta} \log \pi_{\theta}(u_t|s_t) \right) R(\tau) \right]
\end{align}$$

As this is an expaction over trajectories we can approximate the gradient by sampling trajectories from a
fixed policy and state transition function:

$$\begin{align}
\nabla_{\theta} J(\theta) &\approx \frac{1}{m} \sum_{i=1}^m  \left(\sum_{t=0}^{H-1} \nabla_{\theta} \log \pi_{\theta}(u^{(i)}_t|s^{(i)}_t) \right) R(\tau^{(i)})
\end{align}$$

Each gradient is of a trajectory is weighted by the reward of the full trajectory. An observation is that the
current actions do not depend on past rewards.

$$
\nabla_{\theta} J(\theta) \approx \frac{1}{m} \sum_{i=1}^m  \left(\sum_{t=0}^{H-1} \nabla_{\theta} \log \pi_{\theta}(u^{(i)}_t|s^{(i)}_t)  \left[  \sum_{k=t}^{H-1} r(s^{(i)}_k, u^{(i)}_k)  \right] \right)
$$

This as an effect of reducing the variance of the gradients' estimate.
