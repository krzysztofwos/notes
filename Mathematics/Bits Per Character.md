[[Bits Per Character]] ([[BPC]]) is the average cross-entropy using log base 2. The character-level model aims to approximate the probability distribution of the next character given past characters.

At each time step $t$, call this (approximate) distribution $\hat{P}_t$ and let $P_t$ be the true distribution. These discrete probability distributions can be represented by a vector of size $n$, where $n$ is the number of possible characters in the alphabet.

The BPC is calculated as follows:

$$
\begin{align}
\frac{1}{T}\sum_{t=1}^T H(P_t, \hat{P}_t) &= -\frac{1}{T}\sum_{t=1}^T \sum_{c=1}^n P_t(c) \log_2 \hat{P}_t(c) \\
& = -\frac{1}{T}\sum_{t=1}^T \log_2 \hat{P}_t(x_t)
\end{align}
$$

where $T$ is the length of the input string.

The equality in the second line comes from the fact that the true distribution $P_t$ is zero everywhere except at the index corresponding to the true character $x_t$ in the input string at location $t$.

When we use an RNN, $\hat{P}_t$ can be obtained by applying a *softmax* to the RNN's output at time step $t$. The number of output units in the RNN should equal the number of characters in the alphabet $n$.

The equation above calculates the average cross-entropy over one input string of size $T$. In practice, we may have more than one string in our batch. Therefore, we should average over all of them.

# Example

```python
# Simulated logits from a model for 3 time steps with a vocabulary size of 4 (e.g., ['A', 'B', 'C', 'D'])
logits = torch.tensor([
    [2.0, 1.0, -1.0, -2.0],  # Logits for time step 1
    [-1.0, 2.0, 1.0, -2.0],  # Logits for time step 2
    [1.0, -1.0, 2.0, -2.0]   # Logits for time step 3
])

# Indices of the true next characters (e.g., 'B', 'C', 'C')
true_indices = torch.tensor([1, 2, 2])

# Convert logits to log probabilities
log_probs = torch.nn.functional.log_softmax(logits, dim=-1)

# Gather the log probabilities of the true next characters
true_log_probs = log_probs[torch.arange(len(true_indices)), true_indices]

# Calculate the negative log-likelihood in bits
nll_bits = -true_log_probs / np.log(2)

# Calculate the average BPC
bpc = nll_bits.mean().item()
```

```python
def calculate_bpc(logits, true_indices):
    # Convert logits to log probabilities
    log_probs = torch.nn.functional.log_softmax(logits, dim=-1)
    # Gather the log probabilities of the true next characters
    true_log_probs = log_probs[torch.arange(len(true_indices)), true_indices]
    # Calculate the negative log-likelihood in bits
    nll_bits = -true_log_probs / np.log(2)
    # Calculate the average BPC
    bpc = nll_bits.mean().item()
    return bpc
```

# References

- https://thegradient.pub/understanding-evaluation-metrics-for-language-models/
