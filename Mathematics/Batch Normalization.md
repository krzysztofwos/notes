Batch Normalizing Transform

**Input:** Values of $x$ over a mini-batch: $\mathcal{B} = \{x_1, ..., x_m\}$

Parameters to be learned: $\gamma$, $\beta$

**Output**: $\{y_i = \text{BN}_{\gamma, \beta}(x_i)\}$

In the algorithm, $\epsilon$ is a constant added to the mini-batch variance for numerical stability

$$
\begin{aligned}
\mu_{\mathcal{B}} &\leftarrow \frac{1}{m} \sum_{i = 1}^m x_i &\text{mini-batch mean} \\
\sigma^2_{\mathcal{B}} &\leftarrow \frac{1}{m} \sum_{i = 1}^m (x_i - \mu_{\mathcal{B}})^2 &\text{mini-batch variance} \\
\hat{x}_i &\leftarrow \frac{x_i - \mu_{\mathcal{B}}}{\sqrt{\sigma^2_{\mathcal{B}} + \epsilon}} &\text{normalize} \\
y_i &\leftarrow \gamma\hat{x}_i + \beta \equiv \text{BN}_{\gamma,\beta}(x_i) &\text{scale and shift}
\end{aligned}
$$
