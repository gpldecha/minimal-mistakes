---
title: "Link manipulator dynamics "
layout: single
author_profile: false
excerpt: "Derivation of dynamic equations of a three link manipulator"
header:
  overlay_color: "#333"
---


{% include base_path %}

<!-- KaTeX -->
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

[Introduction to Robotics
Mechanics and Control](http://www.mech.sharif.ir/c/document_library/get_file?uuid=5a4bb247-1430-4e46-942c-d692dead831f&groupId=14040)

**The outward iteration for link 3**

$$ {}^3\omega_3 =  \begin{bmatrix}
       0  \\
       0 \\
       \dot{\theta_1} + \dot{\theta_2} + \dot{\theta_3}   
     \end{bmatrix}$$

$$ {}^3\dot{\omega}_3 =  \begin{bmatrix}
       0  \\
       0 \\
       \ddot{\theta_1} + \ddot{\theta_2} + \ddot{\theta_3}   
\end{bmatrix}$$

$$ {}^3\dot{v}_3 = {}^3_2R \Bigg( {}^2\dot{\omega}_2 \times {}^2P_3 + {}^2\omega_2 \times ({}^2\omega_2 \times {}^2P_3) + {}^2\dot{v}_2 \Bigg)$$

$$ {}^3\dot{v}_3 = \begin{bmatrix}
       c_3 & s_3   & 0  \\
       -s_3 &  c_3  & 0 \\
       0   &  0    & 1
     \end{bmatrix}
     \begin{bmatrix}
      l_1\ddot{\theta}_1s_2 - l_1\dot{\theta}^2_1c_2 + gs_{12} \\
      l_1\ddot{\theta}_1c_2 + l_1\dot{\theta}^2_1 s_2 + gc_{12} \\
      0
     \end{bmatrix}$$
$$
=
\begin{bmatrix}
 l_1\ddot{\theta}_1(c_2s_3 + s_2c_3) - l_1\dot{\theta}^2_1(c_2c_3 - s_2s_3) + g(c_3s_{12} + s_3c_{12}) \\
 l_1\ddot{\theta}_1(c_2c_3 - s_2s_3) + l_1\dot{\theta}^2_1(c_2s_3 + s_2c_3) + g(c_{12}c_3 - s_{12}s_3) \\
 0
\end{bmatrix}$$
$$
=
\begin{bmatrix}
 l_1\ddot{\theta}_1s_{23} - l_1\dot{\theta}^2_1c_{23} + gs_{123} \\
 l_1\ddot{\theta}_1c_{23} + l_1\dot{\theta}^2_1s_{23} + gc_{123} \\
 0
\end{bmatrix}$$<br/>

$$ {}^3\dot{v}_{C_3} = {}^3\dot{v}_3 $$ because $$ {}^3P_{C_3} = 0$$<br/>

$$ {}^3F_3 = m_3\,{}^3\dot{v}_{C_3}
           = \begin{bmatrix}
            m_3\,l_1\ddot{\theta}_1s_{23} - m_3\,l_1\dot{\theta}^2_1c_{23} + m_3\,gs_{123} \\
            m_3\,l_1\ddot{\theta}_1c_{23} + m_3\,l_1\dot{\theta}^2_1s_{23} + m_3\,gc_{123} \\
            0
           \end{bmatrix}$$<br/>

$$ {}^3N_3 =  {}^{C_3}I_3\, {}^3\dot{\omega}_3 + {}^3\omega_3 \times {}^{C_3}I_3\, {}^3\omega_3
           = \begin{bmatrix}
           0 \\
           0 \\
           I_{zz}(\ddot{\theta_1} + \ddot{\theta_2} + \ddot{\theta_3})
           \end{bmatrix}$$<br/>

**The inward iteration for link 3**

$$ {}^3f_3 = {}^3F_3$$<br/>

$$ {}^3n_3 = {}^3N_3$$<br/>

**The inward iteration for link 2**

$$ {}^2f_2 = {}^2_3R\, {}^3f_3 + {}^2F_2
           = \begin{bmatrix}
                  c_3 & -s_3   & 0  \\
                  s_3 &  c_3  & 0 \\
                  0   &  0    & 1
                \end{bmatrix}
                \begin{bmatrix}
                 m_3\,l_1\ddot{\theta}_1s_{23} - m_3\,l_1\dot{\theta}^2_1c_{23} + m_3\,gs_{123} \\
                 m_3\,l_1\ddot{\theta}_1c_{23} + m_3\,l_1\dot{\theta}^2_1s_{23} + m_3\,gc_{123} \\
                 0
                \end{bmatrix} + {}^2F_2$$
$$ =
\begin{bmatrix}
  m_3\,l_1\ddot{\theta}_1s_2 - m_3\,l_1\dot{\theta}^2_1c_2 + m_3\,gs_{12} \\
  m_3\,l_1\ddot{\theta}_1c_2 + m_3\,l_1\dot{\theta}^2_1s_2 + m_3\,gc_{12}  \\
  0
\end{bmatrix} +
\begin{bmatrix}
m_2l_1\ddot{\theta}_1s_2 - m_2l_1\dot{\theta}^2_1c_2 + m_2 g s_{12} - m_2l_2(\dot{\theta}_1 + \dot{\theta}_2)^2 \\
m_2l_1\ddot{\theta}_1c_2 + m_2l_1\dot{\theta}^2_1s_2 + m_2 g c_{12} + m_2l_2(\ddot{\theta}_1 + \ddot{\theta}_2) \\
0
\end{bmatrix}
$$<br/>

$$ {}^2n_2 = {}^2N_2 + {}^2_3R\,{}^3n_3 + {}^2P_{C_2} \times {}^2F_2 + {}^2P_3 \times {}^2_3R\, {}^3f_3$$<br/>

$$ = \begin{bmatrix}
       c_3 & -s_3  & 0 \\
       s_3 &  c_3  & 0 \\
       0   &  0    & 1
     \end{bmatrix}
     \begin{bmatrix}
     0 \\
     0 \\
     I_{zz}(\ddot{\theta_1} + \ddot{\theta_2} + \ddot{\theta_3})
     \end{bmatrix} +
     \begin{bmatrix}
     l_2 \\
     0 \\
     0
     \end{bmatrix} \times {}^2F_2
$$
$$ = \begin{bmatrix}
  0 \\
  0 \\
  m_2l_1l_2\ddot{\theta}_1c_2 + m_2l_1l_2\dot{\theta}^2_1s_2 + m_2 l_2 g c_{12} + m_2l^2_2(\ddot{\theta}_1 + \ddot{\theta}_2) + I_{zz}(\ddot{\theta_1} + \ddot{\theta_2} + \ddot{\theta_3})
\end{bmatrix}
$$

**The inward iteration for link 1**

$$ {}^1f_1 = {}^1_2R\, {}^2f_2 + {}^1F_1 $$
$$ = \begin{bmatrix}
       c_2 & -s_2  & 0 \\
       s_2 &  c_2  & 0 \\
       0   &  0    & 1
     \end{bmatrix}
     \begin{bmatrix}
       m_3\,l_1\ddot{\theta}_1s_2 - m_3\,l_1\dot{\theta}^2_1c_2 + m_3\,gs_{12} + m_2l_1\ddot{\theta}_1s_2 - m_2l_1\dot{\theta}^2_1c_2 + m_2 g s_{12} - m_2l_2(\dot{\theta}_1 + \dot{\theta}_2)^2 \\
       m_3\,l_1\ddot{\theta}_1c_2 + m_3\,l_1\dot{\theta}^2_1s_2 + m_3\,gc_{12} + m_2l_1\ddot{\theta}_1c_2 + m_2l_1\dot{\theta}^2_1s_2 + m_2 g c_{12} + m_2l_2(\ddot{\theta}_1 + \ddot{\theta}_2) \\
       0
     \end{bmatrix} + {}^1F_1$$
     $$ =\begin{bmatrix}
      -m_3\,l_1\dot{\theta}^2_1 + m_3 g s_1 + m_2 g s_1 - m_2 l_2 (\dot{\theta}_1 + \dot{\theta}_2)^2 c_2 - m_2 l_2 (\dot{\theta}_1 + \dot{\theta}_2)^2 s_2 \\
      m_3 l_1 \ddot{\theta}_1 + m_3 g s_{12} s_2 + m_3 g c_{12} c_2 + m_2 l_1 \ddot{\theta}_2 +  m_2 g s_{12} s_2 + m_2 g c_{12} c_2 - m_2 l_2 s_2 (\ddot{\theta}_1 + \ddot{\theta}_2)^2 + m_2 l_2 c_2 (\ddot{\theta}_1 + \ddot{\theta}_2) \\
      0
     \end{bmatrix} $$
     $$ +\begin{bmatrix}
     -m_1l_1\dot{\theta}^2_1 + m_1gs_1 \\
     m_1l_1\ddot{\theta}_1 + m_1 g c_1 \\
     0
     \end{bmatrix}
     $$

$$ {}^1n_1 = {}^1N_1 + {}^1_2R\,{}^2n_2 + {}^1P_{C_1} \times {}^1F_1 + {}^1P_2 \times {}^1_2R\, {}^2f_2$$<br/>

$$ = \begin{bmatrix}
  0 \\
  0 \\
  m_2l_1l_2 c_2 \ddot{\theta}_1 + m_2l_1l_2 s_2 \dot{\theta}^2_1 + m_2 l_2 g c_{12} + m_2l^2_2(\ddot{\theta}_1 + \ddot{\theta}_2) + I_{zz}(\ddot{\theta_1} + \ddot{\theta_2} + \ddot{\theta_3})
\end{bmatrix}$$
$$ + \begin{bmatrix}
0 \\
0 \\
m_1 l^2_1\ddot{\theta}_1 + m_1 l_1 g c_1
\end{bmatrix} $$

$$ + \begin{bmatrix}
0 \\
0 \\
m_3 l^2_1 \ddot{\theta}_1 + m_3 l_1 g s_{12} s_2 + m_3 l_1 g c_{12} c_2 + m_2 l^2_1 \ddot{\theta}_2 +  m_2 l_1 g s_{12} s_2 + m_2 l_1 g c_{12} c_2 - m_2 l_1 l_2 s_2 (\dot{\theta}_1 + \dot{\theta}_2)^2 + m_2 l_1 l_2 c_2 (\ddot{\theta}_1 + \ddot{\theta}_2)
\end{bmatrix} $$

**Extracting the torque components**

$$ \tau_i = {}^in^{T}_i\; {}^i\hat{Z}_i $$<br/>

$$ \tau_1 = $$
$$ m_3 l^2_1 \ddot{\theta}_1 + m_3 l_3 g (s_{12}s_2 + c_{12} c_2) + I_{zz}(\ddot{\theta_1} + \ddot{\theta_2} + \ddot{\theta_3})$$
$$ + m_2l^2_2(\ddot{\theta}_1 + \ddot{\theta}_2) + m_2 l_1 l_2 c_2 (2\ddot{\theta}_1 + \ddot{\theta}_2) + (m_1 + m_2)l^2_1 \ddot{\theta}_1 - m_2 l_1 l_2 s_2 \dot{\theta}^2_2 $$
$$ -2m_2 l_1 l_2 s_2 \dot{\theta}_1 \dot{\theta}_2 + m_2 l_2 g c_{12} + (m_1 + m_2)l_1 g c_1$$<br/>

$$ \tau_2 = m_2l_1l_2c_2 \ddot{\theta}_1 + m_2l_1l_2\dot{\theta}^2_1s_2 + m_2 l_2 g c_{12} + m_2l^2_2(\ddot{\theta}_1 + \ddot{\theta}_2) + I_{zz}(\ddot{\theta_1} + \ddot{\theta_2} + \ddot{\theta_3})$$<br/>

$$\tau_3 = I_{zz}(\ddot{\theta_1} + \ddot{\theta_2} + \ddot{\theta_3})$$


**Dynamic Equation**

$$ \tau = M(\theta)\ddot{\theta} + V(\theta, \dot{\theta}) + G(\theta)$$

$$ M(\theta)\ddot{\theta} = \begin{bmatrix}
 m_3 l^2_1 + I_{zz} + l^2_2m_2 + 2l_1l_2m_2c_2 +l^2_1(m_1 + m_2) & I_{zz} + l^2_2 m_2 + l_1l_2m_2c_2 +  l^2_2 m_2 + l_1l_2m_2c_2 & I_{zz} \\
 I_{zz} + l^2_2m_2 + l_1l_2m_2c_2 & I_{zz} & I_{zz} \\
 I_{zz} & I_{zz} & I_{zz}
\end{bmatrix}
\begin{bmatrix}
\ddot{\theta}_1 \\
\ddot{\theta}_2 \\
\ddot{\theta}_3
\end{bmatrix}
$$

$$V(\theta, \dot{\theta}) =
\begin{bmatrix}
  -m_2 l_1 l_2 s_s \dot{\theta}^2_2 - 2m_2l_1l_2s_s\dot{\theta}_1\dot{\theta}_2 \\
  m_2 l_1 l_2 s_2 \dot{\theta}^2_1 \\
  0
\end{bmatrix}$$

$$G(\theta) =
\begin{bmatrix}
  m_3 l_3 g c_1 + m_2 l_2 g c_{12} + (m_1 + m_2)l_1 g c_1 \\
  m_2 l_2 g c_{12} \\
  0
\end{bmatrix}$$
