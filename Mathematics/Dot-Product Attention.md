$$
\text{Attention}(q,K,V)
=
\text{softmax}\left(qK^\mathrm{T}\right)V
=
\sum_{i}{\frac{e^{qk_i}}{\sum_{j}{e^{qk_j}}}v_i}
$$

Scaled dot-product attention:

$$
\text{Attention}(q,K,V)
=
\text{softmax}\left(\frac{qK^\mathrm{T}}{\sqrt{d_k}}\right)V
$$

The attention weights are divided by the square root of the dimension of the key vectors, ${\displaystyle {\sqrt {d_{k}}}}$, which stabilizes gradients during training.

We can compute attention on a set of queries packed together into a matrix $Q$:

$$
\text{Attention}(Q,K,V)
=
\text{softmax}\left(\frac{QK^\mathrm{T}}{\sqrt{d_k}}\right)V
$$

The result of vector-matrix multiplication $qK^\mathrm{T}$ is a vector of dot products of the vector $q$ with each column of the matrix $K^\mathrm{T}$:

$$
qK^\mathrm{T} =
\begin{bmatrix}
    — q —
\end{bmatrix}
\begin{bmatrix}
     |   &   |   &        &   |  \\
    k_1  &  k_2  & \cdots &  k_n \\
     |   &   |   &        &   |
\end{bmatrix}
     =
\begin{bmatrix}
     q \cdot k_1  &  q \cdot k_2  & \cdots &  q \cdot k_n
\end{bmatrix}
$$

The result of matrix-matrix multiplication $QK^\mathrm{T}$ is a matrix of dot products of each row of the matrix $Q$ with each column of the matrix $K^\mathrm{T}$:

$$
QK^\mathrm{T} =
\begin{bmatrix}
    — q_1 — \\
    — q_2 — \\
    \vdots  \\
    — q_m —
\end{bmatrix}
\begin{bmatrix}
     |   &   |   &        &   |  \\
    k_1  &  k_2  & \cdots &  k_n \\
     |   &   |   &        &   |
\end{bmatrix}
=
\begin{bmatrix}
    q_1 \cdot k_1  &  q_1 \cdot k_2  &  \cdots  &  q_1 \cdot k_n \\
    q_2 \cdot k_1  &  q_2 \cdot k_2  &  \cdots  &  q_2 \cdot k_n \\
    \vdots         &  \vdots         &  \ddots  &  \vdots        \\
    q_m \cdot k_1  &  q_m \cdot k_2  &  \cdots  &  q_m \cdot k_n
\end{bmatrix}
$$

## References

- https://en.wikipedia.org/wiki/Attention_(machine_learning)
- https://en.wikipedia.org/wiki/Transformer_(machine_learning_model)#Scaled_dot-product_attention
