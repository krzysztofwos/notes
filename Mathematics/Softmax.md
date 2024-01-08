$$
\text{softmax}(X)_{ij}
=
\frac{\exp(X_{ij})}{\sum_{k}{\exp(X_{ik})}}
$$

The denominator, or normalization constant, is also sometimes called _partition function_, and its logarithm is called the log-partition function.

The origins of that name are in statistical physics where a related equation models the distribution over an ensemble of particles.

$$
\begin{aligned}
    l(\mathbf{y}, \hat{\mathbf{y}})
    &= -\sum_{j=1}^{q}{
        y_j \log \frac{\exp(o_j)}{\sum_{k=1}^{q}{\exp(o_k)}}
    } \\
    &= \sum_{j=1}^{q}{y_j \log \sum_{k=1}^{q}{\exp(o_k)}} - \sum_{j=1}^{q}{y_j o_j} \\
    &= \log \sum_{k=1}^{q}{\exp(o_k)} - \sum_{j=1}^{q}{y_j o_j}
\end{aligned}
$$
