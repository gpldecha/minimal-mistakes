---
title: "Safely Approximating the Value Function"
layout: single
author_profile: true
excerpt: "Function approximation of the value function is key to generalisation. However, one has to be careful!"
header:
  overlay_color: "#333"
---

Bootstrapping methods are more difficult to combine with FA than are non-bootstrapping methods.

<!-- KaTeX -->
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

# What is function approximation ?


# What is the main cause of diverging value function ?


# When can the value function diverge ?

<span style="color:blue"><b>The deadly triad</b></span> [*(exert from Sutton's slides NIPS 2015 tutorial)*](http://media.nips.cc/Conferences/2015/tutorialslides/SuttonIntroRL-nips-2015-tutorial.pdf)


The risk of divergence arises whenever we combine three things:

1. <span style="color:red"><b>Function approximation:</b></span><br>
significantly generalizing from large numbers of examples.

2. <span style="color:red"><b>Bootstrapping</b></span><br>
learning value estimates from other value estimates,
as in dynamic programming and temporal-difference learning.

3. <span style="color:red"><b>Off-policy learning</b></span><br>
learning about a policy from data not due to that policy,
as in Q-learning, where we learn about the greedy policy from
data with a necessarily more exploratory policy.

Based on the above the following should converge (always?):

* On-policy with any form of Bootstrapping such as TD(0)


# Off/On-policy

* Value Iteration: off-policy
* Q-learning: off-policy
* Policy Iteration: on-policy
* SARSA: on-policy
