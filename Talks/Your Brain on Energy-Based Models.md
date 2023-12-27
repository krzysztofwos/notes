Talks by [[Will Grathwohl]]

# [[Your Brain on Energy-Based Models: Applying and Scaling EBMs to Problems of Interest to Machine Learning]]

<iframe width="560" height="315" src="https://www.youtube.com/embed/taob_eW0OFs?si=Tz4HgyA_5b1sGrHt" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

An energy-based model (EBM) is a density model—we are trying to model a probability distribution—parameterized with

$$
p_{\theta}(x) = \frac{e^{-E_{\theta}(x)}}{Z(\theta)}
$$

$$
Z(\theta) = \int_{x} e^{-E_{\theta}(x)} \text{d}x
$$

where $E_{\theta}: \mathbb{R}^D \rightarrow \mathbb{R}$ fully specifies the model.

The density is an exponential of the negative value of some function $E_{\theta}(x)$ divided by a normalizing constant $Z(\theta)$.

The function $E_{\theta}(x)$ is called an energy function. It is a function that maps from the data to a scalar value.

The model is completely specified by the energy function because the normalizing constant is a function of the energy function.

The appeal of generative models:

- We can use them to discover latent structures that are hidden in high-dimensional data.
- They can be trained on unlabeled data.
- If we had a perfect generative model, we could easily use it to solve many problems.

We can re-purpose the architectures we use for discriminative tasks as energy functions without having to change the models that we know work well for these tasks.

The normalization constant $Z(\theta)$ is intractable to compute or even to estimate. We cannot compute likelihoods or draw samples efficiently.

The main technique to learn the parameters from data is an approximation to the gradient of the likelihood.

While $\log p_{\theta}(x)$ does not have a nice form, $\frac{\partial \log p_{\theta}(x)}{\partial \theta}$ can be written more simply as

$$
\frac{\partial \log p_{\theta}(x)}{\partial \theta} = \mathbb{E}_{p_{\theta}(x')}\left[ \frac{\partial E_{\theta}(x')}{\partial \theta} \right] - \frac{\partial E_{\theta}(x)}{\partial \theta}
$$

With an EBM, to compute the likelihood, we need to evaluate or estimate the normalizing constant, which is not easy. But the derivative can be represented in a much easier form where it is an expected derivative of the energy function evaluated over the model $\mathbb{E}_{p_{\theta}(x')}\left[ \frac{\partial E_{\theta}(x')}{\partial \theta} \right]$ minus the derivative of the energy function at the data $\frac{\partial E_{\theta}(x)}{\partial \theta}$.

The $\mathbb{E}_{p_{\theta}(x')}\left[ \frac{\partial E_{\theta}(x')}{\partial \theta} \right]$ is still an expectation over the model distribution, which is itself not quite tractable to estimate, but we can approximate it reasonably well with MCMC sampling.

Historically, this estimator was used to train Restricted Boltzmann Machines (RBMs) and Product of Experts (PoEs) models.

In classification, one of the most-studied problems in machine learning, we are modeling a conditional distribution $p(y | x)$ (and maximize the likelihood) using some parametric function $f_{\theta}: \mathbb{R}^D \rightarrow \mathbb{R}^K$ that maps from our data to $K$ unconstrained real values, where $K$ is the number of classes.

We take these $K$ unconstrained values and pass them through some transformation (softmax) to parameterize a probability distribution and obtain $p(y | x)$.

We can take the exact same thing and redefine what the outputs mean. Now, we have the same function that maps from the data to $K$ values, and we are going to say that each of these outputs is an unnormalized log density of an EBM over the joint distribution of the data and the label.

$$
p_{\theta}(x, y) = \frac{e^{f_{\theta}(x)[y]}}{Z(\theta)}
$$

This is just an EBM with energy $E_{\theta}(x, y) = -f_{\theta}(x)[y]$.

We take our data, pass it through our function, we take the y-th index, and that's our unnormalized density.

We can now sum over the labels, and we can now also get an unnormalized density model for the unconditional data density

$$
p_{\theta}(x) = \sum_y p_{\theta}(x, y) = \frac{\sum_y e^{f_{\theta}(x)[y]}}{Z(\theta)}
$$

which is an EBM with energy $E_{\theta}(x) = -\text{LogSumExp}_y(f_{\theta}(x)[y])$.

We take whatever classifier you are already using, and we say that's your energy function.

We take this interpretation of the model and use the basic rules of probability to compute $p_{\theta}(y | x)$—the class-conditional distribution—and we recover the standard softmax transformation. In other words, when we take this model and compute $p_{\theta}(y | x)$, we arrive at what we would have had normally.

When we compute $p_{\theta}(y | x) = \frac{p_{\theta}(x, y)}{p_{\theta(x)}}$ we get

$$
p_{\theta}(y | x) = \frac{e^{f_{\theta}(x)[y]}}{\sum_{y'} e^{f_{\theta}(x)[y']}}
$$

— a standard softmax.

Putting it all together.

We start with this energy-based parameterization—or interpretation—of the same architecture. We find that we have this function that maps the data to a number of outputs. Then, by applying various simple transformations to those outputs, we can model a more interesting family of distributions. We can use softmax to model a classifier, we can do nothing to model this joint distribution, and we can do LogSumExp to model the conditional density.

This means that we have more avenues for training the parameters of this large function approximator than we had before.

We have found a [[Joint Energy Model]] (JEM) inside a classifier.

Using the interpretation of the classifier architecture as a model of the joint distribution, we can now maximize $p_{\theta}(x, y)$ instead of $p_{\theta}(y | x)$ using approximate likelihood gradient, or we can factor the likelihood and maximize $\log p_{\theta}(x) + \log p_{\theta}(y | x)$.

Results show that training a model this way minimally affects the classification performance, but it allows the model to perform roughly as a SOTA generative model. There is a consistent but relatively small decrease in accuracy.

# [[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind)]]

<iframe width="560" height="315" src="https://www.youtube.com/embed/M9JlCa4Mtrg?si=ONjEM9kELf8soKS2" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Energy Based Models parameterize a probability distribution using an energy function—some function that maps from the data to a single, unconstrained, scalar value that represents the unnormalized log probability of the distribution that we are trying to model.

Variational Autoencoders, GANs, and Normalizing Flows get around many of the difficulties that arise when working with unnormalized probability distributions. Diffusion models are also highly related to EBMs.

## [[Your Classifier is Secretly an Energy Based Model and You Should Treat it Like One]]

Published ICLR 2020

To define an EBM, all we need is the energy function. It can be almost any function we want. Because of that, it is straightforward to incorporate known structures, or we can use a parametric model architecture that we know performs well on the downstream tasks that we care about.

![[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind) 12-27 screenshot.png]]

This does come at a cost. In general, it is intractable to compute or estimate the normalizing constant of these models. It is also very difficult to draw approximate samples.

### The Approach

![[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind) 14-59 screenshot.png]]

Parameterize the model of the conditional distribution $p(y | x)$ of the labels $y$ given $x$ data with some function $f_{\theta}: \mathbb{R}^D \rightarrow \mathbb{R}^K$ which maps from the input data to $K$ unconstrained real-valued outputs, where $K$ is the number of classes.

Pass these unconstrained outputs through the softmax function to get the parameters of the categorical distribution over our $K$ class labels.

![[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind) 15-26 screenshot.png]]

We can define these outputs to mean anything. We can take a different perspective on this and redefine each output to be an unnormalized log probability over the joint distribution between the data example and each class label.

This way, we define an EBM for this joint distribution with energy $E_{\theta}(x, y) = -f_{\theta}(x)[y]$, where we index the output of this function with the class label.

![[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind) 15-38 screenshot.png]]

From this perspective, we can easily sum out the class label to obtain a model for $p_{\theta}(x)$ or the unconditional data density. This is also an EBM.

![[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind) 16-4 screenshot.png]]

We can use basic rules of probability to compute the classifier $p_{\theta}(x | y)$ distribution from this current model perspective. This way, we recover the standard softmax function we would normally be using to parameterize this classifier in the first place.

![[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind) 16-22 screenshot.png]]

Putting this all together, without changing the architecture, we found models of the joint distribution $p_{\theta}(x, y)$, the unconditional data distribution $p_{\theta}(x)$, and the classifier distribution $p_{\theta}(y | x)$. We obtain these by applying different very simple transformations on top of the outputs of the function that we would already be using to address this classification task.

![[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind) 16-58 screenshot.png]]

### Training

How do we act on these insights to change the way we train the models?

We can optimize the joint distribution $p_{\theta}(x, y)$ using the approximate gradient approach, or we can factorize the probability into $\log p_{\theta}(x) + \log p_{\theta}(y | x)$ and train the $\log p_{\theta}(x)$ using the approximate gradient approach and train the $\log p_{\theta}(y | x)$ classifier using the standard cross-entropy loss.

![[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind) 18-27 screenshot.png]]

As a hybrid generative-discriminative model, these models perform very well. They retain the very strong accuracy of the discriminative model used, with a slight decrease in accuracy, but also, at the same time, obtain generative results that are on par with the SOTA.

### [[Langevin Sampling]]

Recent work on larger-scale EBMs has had a lot of success using samplers based on [[Langevin Dynamics]]. Generate samples by recursively applying this update, which looks like a noisy form of gradient descent. We are stepping down the energy and adding calibrated amounts of Gaussian noise, which will encourage the exploration of the samples.

![[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind) 37-10 screenshot.png]]

When doing the Langevin Sampling, we have a step size $\alpha$, which is the hyper-parameter of the sampler that is related to the amount of noise we add $\mathcal{N}(0, \sqrt{2\alpha})$. At a large scale, it is crucial to decouple these two. We end up with a sampler that has a step size and a separate amount of noise added. Typical parameters people use are setting the step size to be 1, 10, or 100, and then the standard deviation of the Gaussian noise is 0.1 for image data.

Most of the large-scale work on EBMs is focused on images because people figured out good hyper-parameters for the sampler on images, but those don't work on other types of data, like tabular data.

### Semi-Supervised Learning

Train the $\log p(x)$ model whenever we have unlabeled data and then maximize the joint probability $\log p(x, y)$ when we have labeled data.

![[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind) 29-41 screenshot.png]]

### Challenges and Limitations of EBMs

We can't compute exact likelihoods, so we can't use likelihoods to train or evaluate the models.

Training via an approximate maximum likelihood training procedure is very unstable. The bias can be quite large.

The parameters of the sampler and the optimization need to be tuned perfectly, or else no learning is going to happen.

The most popular metrics for evaluating these models are based on annealed importance sampling, and that involves MCMC, which is difficult to work with and tune.

**---**

EBMs make the fewest assumptions about the data. This can lead, when the models are trained properly, to much-improved performance.

[[Glow]] is a [[Normalizing Flow]]. It takes a Gaussian distribution and warps it through invertible transformations. When you train flows, you observe likelihoods that look like a Gaussian distribution.

![[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind) 35-34 screenshot.png]]

JEM produces this interesting three-modal structure. In [[CIFAR-10]], the top likelihoods (top row, middle, green) come from classes that have the lowest entropy, e.g., the cars, airplanes, and boats; the middle mode are deer, horses, and birds, which have more variation in their background but they are also more static, and at the bottom we have the highest entropy classes such as frogs, cats, and dogs, which have much fuzzier image statistics.

The EBMs can capture this kind of uncertainty much more easily.

## Oops I Took A Gradient: Scalable Sampling for Discrete Distributions

Most of the success in EBMs comes from using a deep neural network as the energy function: $E_{\theta}(x) = -f_{\theta}(x)$. How to sample? We use Langevin Sampling when our data is continuous

$$

x_{t + 1} = x_t + \frac{\epsilon}{2} \nabla_x f_{\theta}(x) + \epsilon\eta \text{, } \eta \sim \mathcal{N}(0, I)


$$

What about discrete data?

The most successful method for training EBMs is based on MCMC sampling.

This work presents a new MCMC sampler for discrete distributions that enables Deep EBMs on discrete data.

### Discrete Sampling

Focus on sampling from discrete probability distributions $p(x) = \frac{e^{f(x)}}{Z}$ which are unnormalized, restricted to binary or categorical data $x \in \{0,1\}^D \text{ or } x \in \{0,\ldots,K\}^D$.

### Gibbs Sampling

The most popular, common, and simple approach for sampling discrete probability distributions is [[Gibbs Sampling]]. Pick some dimension and then re-sample that dimension with all other dimensions kept fixed.

Consider the dimension indicated by the red arrow. Evaluate the likelihood of the distribution at the sample.

![[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind) 43-58 screenshot.png]]

Then, flip the bit at that location and re-evaluate the likelihood.

![[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind) 44-0 screenshot.png]]

Then, accept the flipped version with the probability that is a sigmoid of the difference of probabilities before and after we flipped the bit.

![[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind) 44-4 screenshot.png]]

Typically, people fix the ordering of dimensions and repeat over and over again. This is called raster scan Gibbs sampling.

![[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind) 44-30 screenshot.png]]

However, some dimensions may not make much sense to try to flip.

If we want to improve Gibbs sampling, we would want to choose which pixels to propose to change, but that is going to need to be a function of the entire input.

![[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind) 46-25 screenshot.png]]

Sample the pixel that we would like to change from some proposal distribution. We want this proposal to be conditioned on the input.

![[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind) 53-52 screenshot.png]]

![[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind) 54-58 screenshot.png]]

### Gibbs With Gradients

Do a [[Taylor Series]] approximation using the gradients. We are at the point $x$. The only places we can move to are Hamming distance 1. We do a Taylor series approximation of the likelihood using the gradients. In this simple two-dimensional example, we take the gradients and project them onto vectors going out in each direction. This gives us an estimate of the probability there.

With the Taylor series, we are approximating the value of a function at some point near another point. So, $x$ is the starting point, and we can choose the values that we want to approximate the values of this function at. Those we pick to be all discrete points that are Hamming distance 1 away from our current point.

![[Your Brain on Energy-Based Models (Will Grathwohl, Deepmind) 1-3-24 screenshot.png]]

# Research Advice

First, tweet about the paper, then Figure 1, then the title, and then do the research.

# Follow-Up

[Implicit Generation and Modeling with Energy Based Models](https://proceedings.neurips.cc/paper/2019/hash/378a063b8fdb1db941e34f4bde584c7d-Abstract.html) by [[Yilun Du]] and [[Igor Mordatch]]

Ignore sampling. Train EBMs to reconstruct the inputs where we have some energy function, and we generate an image to minimize the energy. Then, we use L2 reconstruction loss, which is very similar to VAE, to learn representations in an unsupervised way.
