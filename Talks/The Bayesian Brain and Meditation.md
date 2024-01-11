By [[Shamil Chandaria]]

<iframe width="560" height="315" src="https://www.youtube.com/embed/Eg3cQXf4zSE?si=JtNE-DUFux3Bg4zV" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

# Bayesian perception problem

[Link](https://youtu.be/Eg3cQXf4zSE?si=SRJXPfz4xXadXpg9&t=676)

$$
\underbrace{P(v | u)}_{\text{Posterior}} = \frac{\overbrace{P(u | v)}^{\text{Likelihood}}\overbrace{P(v)}^{\text{Prior}}}{P(u)}
$$

Prior $P(v)$ — how likely am I to see an apple?

Likelihood (of the data) $P(u|v)$ — what is the probability that if this were an apple, if I were correct about my hypothesis that this is an apple, I would see this particular sensory data from it?

$P(u)$ — how likely will I see this sensory data in general?

Posterior — how likely is it that this is an apple, given this sensory data?

# Why minimize Free Energy?

[Link](https://youtu.be/Eg3cQXf4zSE?si=WcMQrgjDZVRc97YS&t=1620)

1. What are the causes of my sensory data? Start with Bayes' theorem:
   $$
   P(v | u) = \frac{P(u | v)P(v)}{P(u)}
   $$
2. Use approximate posterior $Q_{\phi}(v | u)$ and learn its parameters $\phi$ to approximate the true posterior $P(v | u)$
3. Minimize the Kullback-Leibler divergence between $Q$ and the true posterior $P$ by changing the parameters $\phi$ of $Q$:

   $$
   \phi^* = \arg\min_\phi\, D_{text{KL}}[Q_{\phi}(v | u) \parallel P(v | u)]
   $$

   $$
   \begin{aligned}
   D_{\text{KL}}[Q_{\phi}(v | u) \parallel P(v | u)] &= \sum_v Q_{\phi}(v | u) \ln \frac{Q_{\phi}(v | u)}{P(v | u)} \\
   &= \mathbb{E}_{Q_{\phi}(v | u)}[\ln Q_{\phi}(v | u) - \ln P(v | u)] \\
   &= \mathbb{E}_{Q_{\phi}(v | u)}[\ln Q_{\phi}(v | u) \underbrace{- \ln P(u | v) - \ln P(v) + \ln P(u)}_{\text{Bayes' theorem}}] \\
   &= \mathbb{E}_{Q_{\phi}(v | u)}[\ln Q_{\phi}(v | u) - \ln P(v)] + \mathbb{E}_{Q_{\phi}(v | u)}[-\ln P(u | v) + \ln P(u)] \\
   &= D_{\text{KL}}[Q_{\phi}(v | u) \parallel P(v)] + \mathbb{E}_{Q_{\phi}}[-\ln P(u | v)] + \ln P(u)
   \end{aligned}
   $$

The step involving Bayes' theorem allows us to decompose the KL divergence into terms involving the approximate posterior, $Q_{\phi}(v | u)$, the likelihood, $P(u | v)$, the true prior $P(v)$, and the evidence $P(u)$.

The evidence term, $\ln P(u)$, is constant with respect to the approximate posterior $Q_{\phi}(v | u)$, so we can ignore it when minimizing the KL divergence.

We are trying to minimize

$$
\underbrace{D_{\text{KL}}[Q_{\phi}(v | u) \parallel P(v)] + \mathbb{E}_{Q_{\phi}}[-\ln P(u | v)]}_{\text{Free Energy}} + \underbrace{\ln P(u)}_{\text{Constant}}
$$

The $\mathbb{E}_{Q_{\phi}}[-\ln P(u | v)]$ term in the Free Energy is the surprise in the sensory data. How surprising are these sensations if it was an apple? The more surprising the data, the more we get penalized.

The $D_{\text{KL}}[Q_{\phi}(v | u) \parallel P(v)]$ term is the distance between our best guess of what's going on—our hypothesis—and the prior.

Why is it called Free Energy?

If we rewrite this Free Energy term again in another way, we can see that it has the same mathematical form as the energy in physics.

The negative log probability is the energy of a system. The more likely something is, the lower its energy. The more unlikely something is, the higher its energy.

$$
F = \sum_v Q(v | u)[\underbrace{-\ln P(v, u)}_{\text{Energy}\,E_v}] - \sum_v -Q(v | u)\ln Q(v | u)
$$

Because of Boltzmann distribution, energies are related to probabilities through an exponential:

$$
p_v = \frac{e^{-\beta E_v}}{Z}
$$

The log is an inverse function to the exponential. So, the probability of a state $v$ is related to its energy $E_v$ through a log:

$$
\ln p_v = -\beta E_v - \ln Z
$$

And so the first term is the average energy of the system, $\bar{E}$, and the second term is the entropy of the system, $H$. Energy minus entropy is the free energy.

$$
F = \underbrace{\sum_v Q(v | u)[\underbrace{-\ln P(v, u)}_{\text{Energy}\,E_v}]}_{\text{Average energy}\,\bar{E}} - \underbrace{\sum_v -Q(v | u)\ln Q(v | u)}_{\text{Entropy}\,H}
$$

The goal of minimizing the Kullback-Leibler divergence term, $D_{\text{KL}}[Q_{\phi}(v | u) \parallel P(v | u)]$, in the context of variational free energy is to make the approximate posterior distribution, $Q_{\phi}(v | u)$, as close as possible to the true posterior distribution, $P(v | u)$.

In other words, this objective aims to align the beliefs or predictions of the _model_ (approximate posterior) with the true underlying data-generating _process_ (true posterior) given the observed data $u$. By minimizing the KL divergence, we are effectively finding the best approximation of the true posterior within the family of distributions parameterized by $\phi$. This is a fundamental step in variational inference, as it seeks to find a distribution that captures the uncertainty in the latent variables $v$ given the observed data $u$ as accurately as possible.

Minimizing the KL divergence term helps in building a tractable and computationally efficient approximation to the true posterior, which can be useful for various tasks such as Bayesian inference, generative modeling, or probabilistic reasoning.

# Precision weighting and attention

[Link](https://youtu.be/Eg3cQXf4zSE?si=7lX2YqV_5Ki_hPHB&t=1870)

Roughly speaking, in the Free Energy Principle, if we make an approximation that all the distributions that we are talking about are Gaussian, then a very simple result comes out: the posterior belief is a weighted average of prior belief and sensory evidence.

In other words, what I experience is somehow a weighted average of my prior and the likelihood of the data.

Precision is the inverse of variance.

# Dependent co-arising as Bayesian inference

[Link](https://youtu.be/Eg3cQXf4zSE?si=U9K_R18Fri51BWIB&t=4230)

The experience of the world is a constrained construction, constrained by the external data and internal beliefs, priors, and assumptions.

We get external data, and what we bring to the experienced world is ways of looking—high-level priors, high-level beliefs, and high-level models. These come together as the terms of Bayes' theorem as the priors $P(v)$—ways of looking—and the likelihood of the data—how likely is the data if that was the correct hypothesis $P(u | v)$. That gives us our experienced world.
