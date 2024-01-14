By [[Thomas Parr]], [[Giovanni Pezzulo]], and [[Karl Friston]]

Given the important links between the notion of priors and the conditions that undergird an organism’s existence, we can also say that in Active Inference, the identity of an agent is isomorphic with its priors.

[[Markov blanket]] is a formal way to express a separation between a system and the rest of the environment. Technically, it is defined as

$$
\mu \perp x | b \iff p(\mu, x|b) = p(\mu|b)p(x|b)
$$

This says that a variable $\mu$ is conditionally independent of a variable $x$ if $b$ is known. In other words, if we know $b$, knowing $x$ would give us no additional information about $\mu$.

A Markov blanket is the set of variables that mediate all (statistical) interactions between a system and its environment.

To identify a Markov blanket in a system wherein we know the conditional dependencies, we can follow a simple rule. The blanket for a given variable comprises its parents (the variables it depends on), its ­children (the variables that depend on it) and, in some settings, the other parents of its children.

On average, entropy is the long-­term average of surprise and, on average, the maximization of a log probability of observations is equivalent to minimization of (Shannon) entropy

$$
H(P(y)) = \mathbb{E}_{P(y)}[S(y)] = -\mathbb{E}_{P(y)}[\ln P(y)]
$$

The difference between ­free energy and surprise is the divergence between an exact posterior probability (i.e., the distribution of external states given blanket states) and an approximate posterior probability (i.e., the distribution over external states given average internal states).

Variational inference recasts the inference problem as an optimization problem by minimizing ­free energy.

One perspective on the difference between cognitive and noncognitive systems is that the latter always have a zero KL-­Divergence, while cognitive systems must go through the (perceptual) process of minimizing this term before their actions are guaranteed to minimize surprise.

Teleology means that behavior is internally regulated by a mechanism that continuously tests ­whether a goal is achieved and, if not, steers corrective actions.

Bayes' theorem expresses an equality between the product of a prior and a likelihood and the product of a posterior and a marginal likelihood

$$
P(x)P(y|x) = P(x|y)P(y)
$$

The marginal likelihood (or model evidence), $P(y)$, can be computed directly from the prior and the likelihood

$$
P(y) = \sum_{x} P(y,x) = \sum_{x} P(y|x)P(x)
$$

The prior and the likelihood—which together comprise the generative model—are sufficient for us to compute the model evidence and the posterior probability.

A Partially Observable Markov Decision Process (POMDP) in a factor graph form

![[Active Inference The Free Energy Principle in Mind, Brain, and Behavior Figure 4.3.png]]

Precision = inverse variance

Bayes' theorem

$$
\underbrace{P(u | \theta, m)}_{\text{Likelihood}} \underbrace{P(\theta | m)}_{\text{Prior}} = \underbrace{P(\theta| u, m)}_{\text{Posterior}} \underbrace{P(u | m)}_{\text{Evidence}}
$$

The right-hand side deals with the posterior probability of parameters ($\theta$) given behavioral data ($u$) under a model ($m$) and the model evidence, and the left-hand side tells us what we need to specify for our model: we need prior beliefs about our parameters of interest and a likelihood function.
