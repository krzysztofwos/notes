# Part 1

<iframe width="560" height="315" src="https://www.youtube.com/embed/xZWu4-rV45A?si=hApmluYyF3rm6wut" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Energy-Based Models (EBMs) originate from the Gibbs distribution in statistical physics.

![[CVPR 2021 Tutorial Theory and Application of Energy-Based Generative Models --- Part 1 Fundamentals 3-13 screenshot.png]]

The Langevin dynamics is a gradient-based MCMC method which consists of a gradient ascent term and a diffusion term

$$
I_{t+\Delta t} = I_t + \frac{\Delta t}{2} \nabla I f_{\theta}(I_t) + \sqrt{\Delta t}\varepsilon_t \text{, } \varepsilon_t \sim \mathcal{N}(0, I)
$$

![[CVPR 2021 Tutorial Theory and Application of Energy-Based Generative Models --- Part 1 Fundamentals 7-57 screenshot.png]]

The [[Kullback-Leibler Divergence]] between two probability densities $p(x)$ and $q(x)$ is defined as the expectation of $\log \frac{p(x)}{q(x)}$ under the distribution $p(x)$. It usually appears in two scenarios:

1. Maximum likelihood estimation:
   Given a training example $x_i$ that is assumed to be sampled from an unknown data distribution $p_{\text{data}}$, $x_i \sim p_{\text{data}}$, we want to learn the model $p_{\theta}(x)$, parameterized by $\theta$ from the data by maximum likelihood.

   The log-likelihood function is

   $$L(\theta) = \frac{1}{n} \sum_{i = 1}^{n} \log p_{\theta}(x_i) \rightarrow \mathbb{E}_{p_{\text{data}}} \left[ \log p_{\theta}(x) \right]$$

   For a large number of training examples, maximizing the likelihood is equivalent to minimizing the KL divergence between the data distribution and the model.

   The expectation under the data distribution can be approximated by averaging over training examples

   ![[CVPR 2021 Tutorial Theory and Application of Energy-Based Generative Models --- Part 1 Fundamentals 9-54 screenshot.png]]

2. Variational approximation:
   Suppose there is a target distribution $p_{\text{target}}$, which is known up to normalizing constant.

   Suppose we want to approximate the target distribution by a distribution $q_{\phi}$ where $\phi$ are the learning parameters. We can find $\phi$ by minimizing the KL divergence between $q_{\phi}$ and $p_{\text{target}}$.

   ![[CVPR 2021 Tutorial Theory and Application of Energy-Based Generative Models --- Part 1 Fundamentals 10-55 screenshot.png]]

In the MLE scenario, the learned model $p_{\theta}$ tends to cover all the modes of the target $p_{\text{data}}$ while in the scenario of variational approximation, the learned model $q_{\phi}$ tends to focus on some major modes of $p_{\text{target}}$ while ignoring the minor modes.

The reason is that in the latter scenario the KL divergence is the expectation w.r.t. $q_{\phi}$.

![[CVPR 2021 Tutorial Theory and Application of Energy-Based Generative Models --- Part 1 Fundamentals 12-3 screenshot.png]]

## Maximum Likelihood Estimation

[[Maximum Likelihood Estimation]] is a commonly-used method to train energy-based models.

Suppose we observe training examples which follow the unknown data distribution $x_i \sim p_{\text{data}}(x)$. The objective function of MLE learning is the average of the log probability density of the training examples.

$$
L(\theta) = \frac{1}{n} \sum_{i = 1}^{n} \log p_{\theta}(x_i)
$$

The gradient of the log-likelihood involves an expectation term which is analytically intractable. The expectation term comes from the derivative of the $\log Z(\theta)$, where $Z(\theta)$ is the intractable normalizing constant.

![[CVPR 2021 Tutorial Theory and Application of Energy-Based Generative Models --- Part 1 Fundamentals 13-5 screenshot.png]]

The expectation term is intractable because $x$ is high-dimensional. If $x$ is a 100-by-100 grayscale image and each pixel can take value from 0 to 255, the image space is too big to do summation over $x$ for computing the expectation according to the definition.

Therefore, it has to be approximated by Markov Chain Monte Carlo (MCMC) method such as Langevin dynamics or Hamiltonian Monte Carlo (HMC).

We can sample $\tilde{x}$ from the model distribution and use the sample average to approximate the expectation.

![[CVPR 2021 Tutorial Theory and Application of Energy-Based Generative Models --- Part 1 Fundamentals 13-46 screenshot.png]]

## Langevin Dynamics

[[Langevin Dynamics]] is a gradient-based [[MCMC]] method that is used to compute the gradient of the log-likelihood.

For high-dimensional data $x$, sampling from the distribution $p(x)$ which is in the form of energy-based model requires MCMC.

The Langevin dynamics is a stochastic gradient ascent algorithm that updates the parameters $\theta$ to maximize the likelihood function. Larger values of the likelihood correspond to higher probability density under the model. $\Delta t$ is the step size and $e_t$ is the Gaussian noise term introducing randomness.

As the step size goes to zero and the number of steps goes to infinity, the distribution of $x_t$ will converge to the target distribution $p_{\theta}(x)$.

![[CVPR 2021 Tutorial Theory and Application of Energy-Based Generative Models --- Part 1 Fundamentals 14-21 screenshot.png]]

## Adversarial Interpretation

The update of parameters $\theta$ is based on the gradient of the log likelihood which is the difference between the observed statistics and the synthesized statistics.

The learning and sampling algorithm algorithm play a [[Minimax]] game. In the learning step, the algorithm finds $\theta$ to maximize the value function $V$ and in the sampling step finds $\tilde{x}$ to maximize the score function $f_\theta$ thus minimizing the value function $V$.

![[CVPR 2021 Tutorial Theory and Application of Energy-Based Generative Models --- Part 1 Fundamentals 17-8 screenshot.png]]

---

The [[Analysis by Synthesis]] learning algorithm is a mode-seeking and mode-shifting process.

![[CVPR 2021 Tutorial Theory and Application of Energy-Based Generative Models --- Part 1 Fundamentals 18-11 screenshot.png]]

## Equivalence Between EMBs and Discriminative Models

![[CVPR 2021 Tutorial Theory and Application of Energy-Based Generative Models --- Part 1 Fundamentals 26-0 screenshot.png]]

![[CVPR 2021 Tutorial Theory and Application of Energy-Based Generative Models --- Part 1 Fundamentals 27-3 screenshot.png]]

![[CVPR 2021 Tutorial Theory and Application of Energy-Based Generative Models --- Part 1 Fundamentals 28-38 screenshot.png]]

![[CVPR 2021 Tutorial Theory and Application of Energy-Based Generative Models --- Part 1 Fundamentals 31-3 screenshot.png]]

# Part 2

<iframe width="560" height="315" src="https://www.youtube.com/embed/cqnWywy3GuM?si=hNtDMTIg3Y7_CsAx" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Diffusion-Based Modeling and Sampling

![[CVPR 2021 Tutorial Theory and Application of Energy-Based Generative Models --- Part 2 Advanced 4-49 screenshot.png]]

We keep adding Gaussian noise to the image in a diffusion process. By adding more and more noise, we eventually arrive at a white noise image $\mathbf{x}_T$. At time step $t$, $\mathbf{x}_t$ is obtained by adding Gaussian noise $\sigma\epsilon_t$ of variance $\sigma^2$ to the image at time step $t - 1$. If we repeat this, this is the diffusion process $q(x_t|x_{t - 1})$. We want to learn an EBM for the images at all those noise levels, corresponding to all those time steps. The model is parameterized by a single network that is a function of both $x$ and $t$.

$$
p_\theta(x_t) = \frac{1}{Z(\theta, t)}\exp(f_\theta(x_t, t))
$$

It is very difficult to learn those EBMs marginally. We can, however, first translate this EBM into a conditional version so that if we consider the conditional distribution of $x_{t - 1}$ given $x_t$, i.e., given $x_t$ we want to recover $x_{t - 1}$ where $x_t$ is a noisy version of $x_{t - 1}$.

$$
p_{\theta}(x_{t-1}|x_t) \propto \exp\left( f_{\theta}(x_{t-1}) - \frac{1}{2\sigma^2} \|x_t - x_{t-1}\|^2 \right)
$$

The distribution $f_\theta(x_{t - 1})$ can be considered as a prior distribution of $x_{t - 1}$. We also add the data likelihood $\frac{1}{2\sigma^2} \|x_t - x_{t-1}\|^2$ which is a least square term, so that the marginal distribution continues to be an EBM with the energy function $f_{\theta}(x_{t-1}) - \frac{1}{2\sigma^2} \|x_t - x_{t-1}\|^2$.

The data likelihood term requires $x_{t - 1}$ to be close to $x_t$ if $\sigma^2$ is small. So, even though the original energy function is may be highly multimodal, with this regularization it is actually quite close to unimodal around $x_t$ and the sampling becomes very easy—it is just sampling from a conditional distribution that is close to unimodal.

In the generation process, after learning these models, we start from white noise image, and repeatedly sample from the conditional distribution $p_\theta(x_{t - 1} | x_t)$. Eventually, we generate a clean image. It is the reverse of the diffusion process, aided by the EBM.
