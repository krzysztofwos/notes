Language models assign a probability distribution over token sequences $t_{0:L}$ where $L$ is the sequence length by factoring out the joint probability:

$$
P(t_{0:L}) = P(t_0) \prod_{i=1}^L P(t_i|t_{0:i - 1})
$$

To model the conditional probability $P(t_i | t_{0:i-1})$, we can use a neural network, e.g., a transformer, to process the character sequence $t_{0:i-1}$.

$$
\begin{align}
P(w_1, w_2, ..., w_n) &= p(w_1)p(w_2|w_1)p(w_3|w1, w_2) ... p(w_n|w_1, w_2, ..., w_{n-1}) \\
&= \prod_{i=1}^n p(w_i|w_1, ..., w_{i - 1})
\end{align}
$$

![[Language Models.png]]

# Entropy

[[Entropy]] is a measure of the average amount of information conveyed in a message.

An intuitive explanation of entropy for languages comes from [[Claude Shannon]] himself in his landmark paper _[[Prediction and Entropy of Printed English]]_:

> The entropy is a statistical parameter which measures, in a certain sense, how much information is produced on the average for each letter of a text in the language. If the language is translated into binary digits (0 or 1) in the most efficient way, the entropy is the average number of binary digits required per letter of the original language.

$F_N$ measures entropy extending over $N$ adjacent letters of text. $b_n$ represents a block of $n$ contiguous letters $(w_1, w_2, ..., w_n)$.

$$
\begin{align}
F_N &= -\sum_{b_n} p(b_n) \log_2 p(w_n|b_{n-1}) \\
&= -\sum_{b_n} p_{b_n} \log_2 p(b_n) + \sum_{b_{n - 1}} p_{b_{n - 1}} \log_2 p(b_{n - 1})
\end{align}
$$

Define $K_N = -\sum_{b_n} p(b_n) \log_2 p(b_n)$. We have:

$$
F_N = K_N - K_{N - 1}
$$

Shannon defined [[language entropy]] $H$ to be:

$$
H = \lim_{N \rightarrow \infty} F_N
$$

# Cross-Entropy

A language model aims to learn, from the sample text, a distribution $Q$ *close* to the empirical distribution $P$ of the language. Cross-entropy is often used to measure the "closeness" of two distributions. The cross-entropy of $Q$ with respect to $P$ is defined as:

$$
H(P, Q) = \mathbb{E}_P(-\log Q)
$$

When $P$ and $Q$ are discrete:

$$
\begin{align*}
H(P, Q) &= -\sum_{x} P(x)\log Q(x) \\
&= -\sum_{x} P(x)[\log P(x) + \log Q(x) - \log P(x)] \\
&= -\sum_{x} P(x)\left[\log P(x) + \log \frac{Q(x)}{P(x)}\right] \\
&= -\sum_{x} P(x)\log P(x) - \sum_{x} P(x)\log \frac{Q(x)}{P(x)} \\
&= H(P) + D_{\text{KL}}(P||Q)
\end{align*}
$$

The cross-entropy of Q with respect to P is the sum of the following two values:

1. The average number of bits needed to encode any possible outcome of $P$ using the code optimized for $P$ (the entropy of $P$).
2. The number of extra bits required to encode any possible outcome of $P$ using the code optimized for $Q$ (the KL divergence).

# Perplexity

Consider a language model with an entropy of three bits. This means that when predicting the next symbol, that language model has to choose among $2^3=8$ possible options. Thus, we can argue that this language model has a perplexity of 8.

$$
\text{PPL}(P, Q) = 2^{H(P, Q)}
$$

# Bits Per Character (BPC)

[[Bits Per Character]] measures the average number of bits needed to encode a character.

> If the language is translated into binary digits (0 or 1) in the most efficient way, the entropy is the average number of binary digits required per letter of the original language.

By this definition, entropy is the average number of BPC.

# References

- https://thegradient.pub/understanding-evaluation-metrics-for-language-models/
