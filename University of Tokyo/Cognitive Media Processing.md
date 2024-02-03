# Lecture #9

Theory of relational invariance
Also known as theory of distinctive features
Compare with Qualia Structure Project in BIPS

[Why We See What We Do](https://sci-hub.ru/10.2307/27857659)

# Lecture #10

At 1:14.

Bhattacharyya distance is a distance measure between two probability distributions.

$$
x = x(u, v) \text{, } y = y(u, v)
$$

$$
\begin{align*}
BD(p_1(x,y), p_2(x,y)) &= -\log \iint \sqrt{p_1(x,y)p_2(x,y)} \, dx \, dy \\
&= -\log \iint \sqrt{q_1(u,v)q_2(u,v)} \, |J(u,v)| \, dx \, dy \\
&= -\log \iint \sqrt{P_1(u,v)P_2(u,v)} \, du \, dv \\
&= BD(P_1(u,v), P_2(u,v))
\end{align*}
$$

$$
q_1(u, v) = p_1(x(u, v), y(u, v))
$$

Bhattacharyya distance is transform-invariant: it stays the same after the mapping.

f-divergence is invariant with any kind of transformation

$$
f_{\text{div}}(p_1, p_2) = \int p_2(x)g\left( \frac{p_1(x)}{p_2(x)} \right) dx
$$

Topology focuses on invariant features w.r.t. any kind of transformation.

Language is a system of only conceptual differences and phonic differences. — Ferdinand de Saussure

# Lecture \#12

Speech waveforms:

- Phase characteristics
- Amplitude characteristics
  - Source characteristics
  - Filter characteristics
    - Word characteristics $P(o|w)$
    - Speaker characteristics $P(o|s)$

![[Cognitive Media Processing Lecture 12 Screenshot 1.png]]

## Invariance

![[Cognitive Media Processing Lecture 12 Screenshot 2.png]]

![[Cognitive Media Processing Lecture 12 Screenshot 3.png]]

# Mathematical evidence of the acoustic universal structure in speech

Bhattacharyya distance (BD) measure between two probability density functions $d_x(c)$ and $d_y(c)$ is formulated as

$$
BD(d_x(c), d_y(c)) = -\ln\int_{-\infty}^\infty \sqrt{d_x(c)d_y(c)} dc
$$

where $0 \leq \sqrt{d_x(c)d_y(c)} \leq 1$. This distance measure is derived based on information theory and can be interpreted as the amount of self-information of joint probability of the two independent distributions $d_x(c)$ and $d_y(c)$.
