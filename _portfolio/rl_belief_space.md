---
title: Reinforcement Learning in belief space
excerpt: A POMDP policy is learned from demonstrations and improved in a Reinforcement learning framework.
permalink: /projects/rl_belief_space/
header:
  teaser: /projects/rl_pomdp/value-function-th.png
  image:  /projects/rl_pomdp/value-function.png

---

<!-- KaTeX -->
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>
{% include base_path %}


# Objective



The parameters of a continuous state and action POMDP policy are initially learned
from human teachers and improved through a fitted reinforcement learning approach.
As an application we consider the task in which both human teachers and robot apprentice
must successfully localize and connect an electrical power socket, a task also known
as Peg in hole (PiH), whilst deprived of vision. To accomplish this the following steps are followed:

* Gather a dataset of demonstrations of the task (find and connect the power socket).
* Learn a value function of the task via fitted reinforcement learning.
* Learn the parameters of the POMDP policy whilst weighting the data points by the value function.

A technical report of this project can be downloaded from [here]({{ site.url }}/documents/fpi_pomdp.pdf).

# Notation and variables


* $$ x \in \mathbb{R}^3$$, Cartesian position of end-effector.
* $$ a \in \mathbb{R}^3 = \dot{x}$$, Cartesian velocity of end-effector.
* $$ y \in \mathbb{R}^N $$, sensory measurement vector.
* $$ b := p(x_{t} \lvert a_{1:t},y_{0:t})$$, probability distribution over state space.
* $$ g : b \mapsto F $$, dimensionality reduction, where $$F$$ is a feature vector.


# Overview

Following the [*Programming by Demonstration (PbD)*](http://www.scholarpedia.org/article/Robot_learning_by_demonstration)
approach, human teachers demonstrate the search and connection task, see Figure [Peg-in-hole search task](#pih_h_v).

<!-- Sina peg-in-hole search video -->
{% include yvideo.html id="w3MgWHjoSVg" width=560 height=316
                                        title = "Peg-in-hole search task:"
                                        cap_id="pih_h_v"
                                        caption = "A blindfolded human teacher demonstrating the peg-in-hole search task. The holder is equipped
                                        with markers and an ATI force/torque sensor from which both velocity and wrench information can be read at
                                        every time step."
%}
<br>

The tool the teacher is using is a peg holder from which the velocity and wrench can be obtained, with the help
of a motion tracking system ([Optitrack](http://optitrack.com/)) and ATI force torque sensor. With both motion (velocity)
and sensing information (wrench) we recursively update a Bayesian state space estimation of the peg's Cartesian position.
A position estimation is necessary as both the human teacher and robot apprentice do not have access to any visual information
when they have to accomplish the task. Figure [Point Mass Filter](#pmf_v), illustrated the Bayesian state space estimation
obtained through the recursive application of the motion and measurement models.

<!-- Sina peg-in-hole search video -->
{% include yvideo.html id="0yf-lkg-Hr0" width=300 height=300
                                        title = "Point Mass Filter:"
                                        cap_id="pmf_v"
                                        caption = "Given an initially known probability distribution all future distributions obtained via the Bayesian update.
                                                   The red line represents the path followed by a human teacher."
%}
<br>

After learning a value function $$V^{\pi}(F)$$ and improving the policy $$\pi_{\boldsymbol{\theta}}: F \mapsto a $$
we can successfully transfer the teachers' behavior to the KUKA LWR robot, see Figure [KUKA LWR PiH](#pih_lwr_v).

<!-- KUKA peg-in-hole search video -->
{% include yvideo.html id="eQRLpqUTvGA" width=250 height=250
                                        title = "KUKA LWR PiH:"
                                        cap_id="pih_lwr_v"
                                        caption = "Application of the learned POMDP policy."
%}
<br>

# Fitted Policy Iteration

Fitted Policy Iteration (FPI) is an off-line on-policy Reinforcement Learning (RL) methods which iteratively
estimates a value function (<b>policy evaluation</b>) and then uses it to update the parameters of the policy (<b>policy improvement</b>).
It is also an Actor-Critic and Batch/Experience replay RL method. The steps of FPI are in essence the same as [Policy Iteration](#http://webdocs.cs.ualberta.ca/~sutton/book/4/node4.html) where the difference is that we use a Fitted RL approach to learn the value function and an Expectation-Maximisation (EM) to improve the parameters of the policy.

## Fitted Policy Evaluation (FPE)

Given a table of state-reward  $$\mathcal{D} = \{ (x^{[i]}_{0:T},a^{[i]}_{0:T})  \}_{i=1:M}$$ where
$$i$$ stands for the $$i$$th demonstration (episode). The value function is learned through the repeated
application of Bellman's on-policy backup operator to the dataset,

* $$\hat{V}_{k+1}^{\pi}(x) = Regress(x, r + \gamma  \hat{V}_{k}^{\pi}(x)) $$

until converges of the bellman residual. Figure [2D teacher demonstrations](#rl_2D_demonstrations)
illustrates a set of demonstrations given by two teachers. The task is reach to goal state (start)
given the starting state. Neither teacher demonstrates the optimal solution which is to go in
a straight line from start to goal.

<!-- 2D Demonstrations -->
{% include image.html
            img="/projects/rl_pomdp/blue-red-trajectory.png"
            title="2D teacher demonstrations"
            fig_id="rl_2D_demonstrations"
            caption="Two teachers demonstrate the task of going form start go goal state. Neither of the two demonstrate the optimal solution, which is to
            go in a straight path to the goal."
%}
<br>

In Figure [Fitted Policy Evaluation](#fpe_v), the on-policy Bellman equation is
repeatably applied to the dataset. At the first time step the target value of
the regressor function  (which is Locally Weighted Regression) is simply the reward: $$\hat{V}_0^{\pi} : x \mapsto r$$.
In the second iteration, a new target for the regressor function is computed: $$\hat{V}_1^{\pi}  : x \mapsto r + \gamma  \hat{V}_0^{\pi}(x)$$ which
depends on the previous value function estimate.

<!-- Fitted Policy Evaluation 2D -->
{% include yvideo.html id="lmKc5ccbbpM" width=250 height=250
                                        title = "Fitted Policy Evaluation:"
                                        cap_id="fpe_v"
                                        caption = "At each time iteration: First the target value of the regression is updated, that the bellman value. Second
                                        a regression function mapping state to value function is learned. In this case we are using Locally Weighted Regression (LWR)."
%}
<br>


## Policy Improvement

Given the estimate of the value function $$\hat{V}^{\pi}(x)$$ we can use it to improve
the parameters of the policy, which is a Gaussian Mixture Model (GMM) in our application.
This can be achieved my maximizing the logarithmic lower point of the objective function $$J(\boldsymbol{\theta}) = \mathbb{E}\{R\}$$  of
the task with respect to the policies parameters $$ \boldsymbol{\theta} $$:

$$\nabla_{\boldsymbol{\theta}} Q(\boldsymbol{\theta},\boldsymbol{\theta}') = \sum\limits_{i=1}^{N}\sum\limits_{t=0}^{T^{[i]}} \nabla_{\boldsymbol{\theta}} \log \pi_{\boldsymbol{\theta}}(x^{[i]}_t,a^{[i]}_t) \mathcal{Q}^{\boldsymbol{\theta}'}(x^{[i]}_t,a^{[i]}_t) \$$

<!-- 2D PbD-POMDP -->
{% include image.html
            img="/projects/rl_pomdp/GMM-Policy.png"
            title="Policy learned from demonstrations"
            fig_id="rl_em_2D"
            caption="" %}


<!-- 2D RL-PbD-POMDP -->
{%  include image.html
    img="/projects/rl_pomdp/QEM-GMM-Policy.png"
    title="Policy learned from demonstrations"
    fig_id="rl_qem_2D"
    caption="" %}



# Socket search task



<!--3 different sockets -->
{% include image.html
            img="/projects/rl_pomdp/sockets-ch4.png"
            title="Three different sockets"
            fig_id="fig_3_sockets"
            caption="" %}

<!-- Table Value function-->
{% include image.html
            img="/projects/rl_pomdp/value-function.png"
            title="Belief space value function:"
            fig_id="bel_value_f"
            caption="" %}


# KUKA


<!-- Search Socket B -->
{% include yvideo.html id="k32qV4JODas" width=560 height=315
                                        title = "KUKA search for power socket:"
                                        cap_id="socket_A_v"
                                        caption = "Search for socket A"
%}


<!-- Search Socket B -->
{% include yvideo.html id="DvRG_7Knijw" width=560 height=315
                                        title = "Socket B:"
                                        cap_id="socket_B_v"
                                        caption = "Search for socket B"
%}


<!-- Search Socket C -->
{% include yvideo.html id="P1-0v0J90D0" width=560 height=315
                                        title = "Socket C:"
                                        cap_id="socket_c_v"
                                        caption = "Search for socket C"
%}
