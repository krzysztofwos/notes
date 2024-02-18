<iframe width="560" height="315" src="https://www.youtube.com/embed/vGdB4eI4KBs?si=2BGUiNAL3qTlbZj2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# Backpropagation

[Chain rule](https://webspace.ship.edu/msrenault/GeoGebraCalculus/derivative_intuitive_chain_rule.html)

The definition of the derivative of ReLU

```python
(self.inp > 0).float()
```

# Cross Entropy Loss

$$
\log \left( \frac{a}{b} \right) = \log(a) - \log(b)
$$

$$
\log(ab) = \log(a) + \log(b)
$$

[[LogSumExp]] allows us to compute the sum of exponentials in a more stable way

$$
\log \left( \sum_{j=1}^n e^{x_j} \right) = \log \left( e^a \sum_{j=1}^n e^{x_j - a} \right) = a + \log \left( \sum_{j=1}^n e^{x_j - a} \right)
$$

where $a$ is the maximum of the `x_j`.
