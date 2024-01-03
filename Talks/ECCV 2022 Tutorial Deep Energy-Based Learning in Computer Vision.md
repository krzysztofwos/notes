By [[Jianwen Xie]]

[Slides](https://energy-based-models.github.io/document/Energy-Based-Models-Tutorial-ECCV-2022.pdf) [Website](https://energy-based-models.github.io/eccv2022-tutorial)

<iframe width="560" height="315" src="https://www.youtube.com/embed/F9CxyBP5zjY?si=BpC53WEGpRVd1ioO" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

The Energy-Based Models can unify bottom-up representation and top-down generation into a single framework.

A population of images can be represented by a probability distribution parameterized by a set of parameters that can be trained from observed data. Such a probabilistic model can be used for supervised, unsupervised, and semi-supervised learning, as well as model-based reinforcement learning.

Energy-Based Models are one type of probabilistic models.

A concept is a set of images which share some sufficient statistics.

The EBM can also be called Markov random field, Gibbs distribution, descriptive model, maximum entropy model, or exponential family model.

![[ECCV 2022 Tutorial_ Deep Energy-Based Learning in Computer Vision 3-43 screenshot.png]]

# Pattern Theory

![[ECCV 2022 Tutorial_ Deep Energy-Based Learning in Computer Vision 5-29 screenshot.png]]

# Research Directions

![[ECCV 2022 Tutorial_ Deep Energy-Based Learning in Computer Vision 15-16 screenshot.png]]

# Deep EBMs in Data Space

[[Maximum Likelihood Estimation]] is a commonly-used method for training EBMs.

Suppose we observe training examples $x_i$ which follow the unknown data distribution $p_\text{data}$. The objective function of the MLE is the average of the log probability density of the training examples. The gradient of the loss involves an expectation term which is analytically intractable. The expectation term comes from the derivative of the $\log Z(\theta)$ w.r.t. $\theta$, where $Z(\theta)$ is the normalization constant.

![[ECCV 2022 Tutorial_ Deep Energy-Based Learning in Computer Vision 16-32 screenshot.png]]

The expectation term is intractable because $x$ is high-dimensional. If $x$ is a $100 \times 100$ image, each pixel taking value from the range $[0, 255]$, the image space is $256^{10000}$, which is too big to do the summation over $x$ to compute the expectation. Therefore, the expectation term has to be approximated by [[Markov Chain Monte Carlo]] (MCMC) such as [[Langevin Dynamics]] or [[Hamiltonian Monte Carlo]] (HMC).

We can sample $\tilde{x}$ from the model distribution and use the sample average to approximate the expectation.

![[ECCV 2022 Tutorial_ Deep Energy-Based Learning in Computer Vision 17-20 screenshot.png]]

## Langevin Dynamics

A gradient-based MCMC method that can be used to compute the gradient of the log likelihood. It's a stochastic gradient descent algorithm that finds data $x$ to maximize the function $f$. The larger $f$ corresponds to the larger probability density.

![[ECCV 2022 Tutorial_ Deep Energy-Based Learning in Computer Vision 18-18 screenshot.png]]

## [[Analysis by Synthesis]]

At each iteration, we first sample synthesized examples from the learned distribution by MCMC. We then used the synthesized and training examples to compute the gradient of the log likelihood such that the model parameters can be updated by a gradient-based learning algorithm.

The learning algorithm tries to match the synthesized examples to the data in terms of statistics.

![[ECCV 2022 Tutorial_ Deep Energy-Based Learning in Computer Vision 19-41 screenshot.png]]

It's a mode-seeking and mode-shifting process.

![[ECCV 2022 Tutorial_ Deep Energy-Based Learning in Computer Vision 20-24 screenshot.png]]

## Adversarial Interpretation of Energy-Based Learning

The update of parameters $\theta$ is based on the gradient of log likelihood, which is the difference between the observed statistics and synthesized statistics. The learning and sampling algorithm actually play a [[Minimax]] game. In the learning step, the algorithm finds $\theta$ to maximize $V$. In the sampling step, the algorithm finds $\tilde{x}$ to maximize the score function $f_\theta$, thus minimizing the value function $V$.

![[ECCV 2022 Tutorial_ Deep Energy-Based Learning in Computer Vision 21-38 screenshot.png]]

## Continuous Inverse Optimal Control

The problem of [[Continuous Inverse Optimal Control]] is to learn unknown cost function from expert demonstrations.

![[ECCV 2022 Tutorial_ Deep Energy-Based Learning in Computer Vision 56-22 screenshot.png]]

![[ECCV 2022 Tutorial_ Deep Energy-Based Learning in Computer Vision 57-9 screenshot.png]]

![[ECCV 2022 Tutorial_ Deep Energy-Based Learning in Computer Vision 57-53 screenshot.png]]

# Deep EBMs in Cooperative Learning

Deep EBMs are trained together with different types of deep latent variable models.

The deep EBM and the deep latent variable model cooperate with each other to learn the data distribution.

https://youtu.be/F9CxyBP5zjY?si=oEFEuQf1zrreeUro&t=3596

# Deep EBMs in Latent Space

Build EBMs on top of latent variable models and learn them together. Data space EBMs represent raw data directly while the latent space EBMs capture the intrinsic rules of the data.
