---
title: "Jacobian"
layout: single
author_profile: false
excerpt: "Derivation of the Jacobian and its properties"
header:
  overlay_color: "#333"
---


{% include base_path %}

<!-- KaTeX -->
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

The derivation of the Jacobian of a two link arm.

[Introduction to Robotics
Mechanics and Control](http://www.mech.sharif.ir/c/document_library/get_file?uuid=5a4bb247-1430-4e46-942c-d692dead831f&groupId=14040)


{% include image.html
            img="/robotics/two-link-manipulator.png"
            title="Two-link-manipulator"
            fig_id="two-link-manipulator"%}

small notatiom notes before continuing:

  * $$c_1 = cos(\theta_1)$$, the letter indicates if it is sin or cos and the number corresponds to the joint angle.

The kinematic chain of the two-link-manipulator:

$$ {}^0_1T(\theta_1) =  \begin{bmatrix}
       c_1 & -s_1  & 0 & 0 \\
       s_1 &  c_1  & 0 & 0 \\
       0   &  0    & 1 & 0 \\
       0   &  0    & 0 & 1 \\
     \end{bmatrix} $$

$$ {}^1_2T(\theta_2) =  \begin{bmatrix}
      c_2 & -s_2  & 0 & l_1 \\
      s_2 &  c_2  & 0 & 0 \\
      0   &  0    & 1 & 0 \\
      0   &  0    & 0 & 1 \\
      \end{bmatrix}$$

$$ {}^2_3T = \begin{bmatrix}
      1 &  0 & 0 & l_2 \\
      0 &  1 & 0 & 0 \\
      0 &  0 & 1 & 0 \\
      0 &  0 & 0 & 1 \\
      \end{bmatrix} $$

$$ {}^0_3T(\theta_1, \theta_2) = {}^0_1T(\theta_1)\,{}^1_2T(\theta_2)\,{}^2_3T
  =  \begin{bmatrix}
  c_1c_2 - s_1s_2 &  -c_1s_2 - s_1c_2 & 0 & c_1c_2l_2 + c_1l_1 - s_1s_2l_2 \\
  s_1c_2 + c_1s_2 &  -s_2s_1 + c_1c_2 & 0 & s_1c_2l_2 + s_2l_1 + c_1s_2l_2 \\
  0 &  0 & 1 & 0 \\
  0 &  0 & 0 & 1 \\
  \end{bmatrix} $$

The above kinematic equation is a function:

$$ F: \theta \mapsto Y$$  

which maps from joint to cartesian space, where $$Y$$ is the position and orientation
of then end-effector with respect to the base frame. The **Jacobian** is the partial derivative of
$$F$$ with respect to the joint angles.

$$\delta \theta\,\frac{\partial F}{\partial \theta} = \delta Y$$


Each row of $$F$$ corresponds to one non-linear equation and for each row the partial derivative
with respect to $\theta$ is taken. As there are 4 rows there are 4 equations of the following form:

$$J_i(\theta_1, \theta_2) = \frac{\partial F_i(\theta_1, \theta_2)}{\partial \theta_1} + \frac{\partial F_i(\theta_1, \theta_2)}{\partial \theta_2}$$

where $$i = 1, 2, 3, 4$$.

### velocity propergation Link-to-link

$$ {}^{i+1}\omega_{i+1} = {}^{i+1}_iR\,{}^i\omega_i + \dot{\theta}_{i+1} {}^{i+1}\hat{Z}_{i+1}$$

$$ {}^{i+1}v_{i+1} = {}^{i+1}_iR ({}^iv_i + {}^i\omega_i \times {}^iP_{i+1})$$

The superscript index is for the frame and subscript is for the link.

## Jacobian summary

end-effector velocity:
$$ v = \begin{bmatrix}
      \upsilon \\
      \omega
    \end{bmatrix} \in (6 \times 1)$$

$$v = J(\theta)\,\dot{\theta}$$

$$\dot{\theta} = J^{-1}(\theta)\,v$$: invserse of the Jacobian is required. If there
are singularities (loss of full rank) the inverse cannot be commputed.

$$\tau = J^{T}(\theta)\,\mathcal{F}$$: Cartesian forces can be converted to torques without
having to inverse the Jacobian.
