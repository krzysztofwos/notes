The result of matrix-matrix multiplication $AB$ is a matrix of dot products of each row of the matrix $A$ with each column of the matrix $B$:

$$
\begin{bmatrix}
    — a_1 — \\
    — a_2 — \\
    \vdots  \\
    — a_m —
\end{bmatrix}_{m \times n}
\begin{bmatrix}
     |   &   |   &          &   |  \\
    b_1  &  b_2  &  \cdots  &  b_k \\
     |   &   |   &          &   |
\end{bmatrix}_{n \times k}
=
\begin{bmatrix}
    a_1 \cdot b_1  &  a_1 \cdot b_2  &  \cdots  &  a_1 \cdot b_k \\
    a_2 \cdot b_1  &  a_2 \cdot b_2  &  \cdots  &  a_2 \cdot b_k \\
    \vdots         &  \vdots         &  \ddots  &  \vdots        \\
    a_m \cdot b_1  &  a_m \cdot b_2  &  \cdots  &  a_m \cdot b_k
\end{bmatrix}_{m \times k}
$$

$$
\begin{bmatrix}
    — \vec{a}_1 — \\
    — \vec{a}_2 — \\
    \vdots        \\
    — \vec{a}_m —
\end{bmatrix}_{m \times n}
\begin{bmatrix}
           |   &         |   &          &         |  \\
    \vec{b}_1  &  \vec{b}_2  &  \cdots  &  \vec{b}_k \\
           |   &         |   &          &         |
\end{bmatrix}_{n \times k}
=
\begin{bmatrix}
    \vec{a}_1 \cdot \vec{b}_1  &  \vec{a}_1 \cdot \vec{b}_2  &  \cdots  &  \vec{a}_1 \cdot \vec{b}_k \\
    \vec{a}_2 \cdot \vec{b}_1  &  \vec{a}_2 \cdot \vec{b}_2  &  \cdots  &  \vec{a}_2 \cdot \vec{b}_k \\
    \vdots                     &  \vdots                     &  \ddots  &  \vdots                    \\
    \vec{a}_m \cdot \vec{b}_1  &  \vec{a}_m \cdot \vec{b}_2  &  \cdots  &  \vec{a}_m \cdot \vec{b}_k
\end{bmatrix}_{m \times k}
$$
