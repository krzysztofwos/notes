By [[Shamil Chandaria]]

<iframe width="560" height="315" src="https://www.youtube.com/embed/UkH-7gZnrr4?si=Xo_kqmn1JInhKkdV" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

An attempt at a general theory of what is happening in the brain from an algorithmic perspective. Bayesian Brain, Predictive Processing, Active Inference, and the Free Energy Principle.

Immanuel Kant (in the 18th century): We only experience the phenomenal world—things as they appear to us. We use the categories of space, time, and causality to arrange our perceptual framework. These are hyperpriors that we bring to bear to organize our sensory data.

Kant's Copernican Revolution in the mind sciences: objects conform to our cognition rather than cognition conforming to objects.

About 100 years later, Helmholtz started crystallizing this as "Perception as inference." We are not just passively experiencing things.

[Visual (In)stability](https://www.youtube.com/watch?v=Lub3lsJdko0)

Bayesian perception problem: we assume that there is something out there in the world that causes our perceptions. We get sensory data. The problem for the agent is to form recognition density—to answer the question, "What are the causes of my sensations given sensory data?" This is solved by using Bayes' theorem. Bayes' theorem gives us a mathematically optimal solution that maximizes the value of all the information.

$$
\underbrace{P(v|u)}_{\text{Posterior}} = \frac{\overbrace{P(u|v)}^{\text{Likelihood}}\overbrace{P(v)}^{\text{Prior}}}{P(u)}
$$

The prior probability, $P(v)$, tells us, before we receive any data, our background beliefs about the causes of sensory data. The likelihood of the data, $P(u | v)$, tells us the probability of getting this particular sensory data, given our best hypothesis about what is going on. The normalizing term, $P(u)$, tells us the probability of receiving the sensory data in the first place.

That normalizing term is very difficult to compute—it's an infinite integral / sum.

$$
P(u) = \sum_v P(u | v)P(v)
$$

We have to go through every single hypothesis. It is computationally explosive.

Although Bayes' theorem is the mathematically optimal solution that maximizes the value of all the information, it is not computationally tractable.

How do we get around it?

Supervised learning. But, there is no supervisor in the brain. The brain must be doing this in an unsupervised way. We don't know the ground truth. The only thing we know is the data itself.

If we only have the data and are trying to guess the feature vector—what are the causes/features of my experience—we can try to guess the feature vector and then use it to generate/predict the data. We can compare the predictions with actual sensory data. This sets up the prediction error, which is used to train the network.

This is called an autoencoder, and the network has three parts. The first part is the Recognition Model (encoder), which tries to go from the data to a feature vector (the code referred to in Predictive Coding). The second part is the Generative Model (decoder), which generates what I would be seeing if these were the correct features of the world.

The problem is that this kind of network is very difficult to train. Variational Autoencoders are trained using the Free Energy loss function. Free Energy takes into account the prediction error, plus it takes into account priors—prior probability around what we would expect the feature vector to be. This gives us a _principled_ way to train the network.

Karl Friston is one of the founders of the Free Energy Principle—the key architect.

We are using this model as an idea of how the brain works, except that in the brain, the generative model folds back onto the recognition model.

In the Predictive Processing framework, what travels up is not the data itself but the prediction errors. The generative model is taking a guess from the latent layer (code, feature vector) and generating what we would be seeing. What is traveling up is prediction errors compared to this generative model. This is likely happening in a hierarchical way.

These priors arise from higher-level models in the brain, and the prediction errors go up to higher levels. This gives us a hierarchical predictive processing framework.

How does the variational algorithm work?

There are features in the world that are generating our sensory data. We cannot solve Bayes' theorem directly. We have to make a guess at an approximate posterior $Q_\phi(v|u)$. We make a functional form, e.g., Gaussian, with certain parameters $\phi$. This is equivalent to the recognition model. From the approximate posterior, we get an estimate of the code (the features) $v'$. From that, we use the generative model with parameters $\theta$, and the output of the generative model are the expectations of sensory data, the expectations of what we would be seeing in the world $u'$. From there, we are in a position to compare the predicted data $u'$ and the actual data $u$, and we get a prediction error. That is at the heart of trying to train this model. But, there is one more factor that goes into the Free Energy: the deviation from prior expectations—how different are these features from prior expectations $D_{\text{KL}}(v'|v_{\text{prior}})$. Using the Free Energy, which combines both the prediction error and the KL divergence from prior expectations, we can then train the recognition model and the generative model to minimize the Free Energy. Hopefully, we then get the convergence between the approximate posterior $Q(v | u)$ and the real posterior $P(v | u)$. This, in a nutshell, is the variational algorithm to solve the approximate Bayesian inference.

(Shannon) Relative Entropy: KL Divergence

$$
D_{\text{KL}} = \sum_{x \in \mathcal{X}} p(x) \log \frac{p(x)}{q(x)}
$$

The KL divergence between two probability distributions is essentially measuring something like a distance—how far away these distributions are. It is not a true distance because it is not symmetric. It is not a metric. It is a divergence.

Suppose we know that a treasure is buried somewhere along the road. Our $q(x)$ is a uniform distribution over the length of the road (measured from 0 to 1). Suppose someone gives us a map $p(x)$ that says that the treasure is somewhere between 0.825 and 1. This is the new information for a more accurate probability distribution. How much information, how many bits of information do we get by going from $q(x)$ to $p(x)$? This is the informational distance—KL divergence. This distance is, roughly speaking, how many yes or no we have to ask to get from $q(x)$ to $p(x)$. What kind of questions? E.g., is it in the first half or the second half? If it's in the second half, is it in the first half of the second half or the second half of the second half? And so on?

Why minimize Free Energy?

The basic idea is that we are trying to solve the fundamental problem of the brain: what are the causes of my sensory data? We are going to use Bayes' theorem, but we can't use it directly because it's computationally intractable.

$$
P(u | v) = \frac{P(u | v)P(v)}{P(u)}
$$

So, we are going to use a variational algorithm. We are going to approximate the actual posterior that we are trying to learn with $Q(v | u) \sim P(v | u)$. $Q(v | u)$ could have a simple form, e.g., Gaussian, with parameters $\phi$. We are going to try to minimize the KL divergence between $Q$ and $P$ by changing the parameters of $Q$.

1. What are the causes of my sensory data? Start with Bayes' theorem
   $$
   P(u | v) = \frac{P(u | v)P(v)}{P(u)}
   $$
1. Use approximate posterior $Q$ and learn its parameters (synaptic weights) $\phi$
   $$
   Q(v | u) \sim P(v | u)
   $$
1. _Minimize_ the Kullback-Leibler divergence ("distance") between $Q$ and true posterior $P$ by changing the parameters $\phi$.

$$
\arg\min_\phi\, D_{\text{KL}}[Q(v | u) \parallel P(v | u)] = \sum_v Q(v | u) \ln \frac{Q(v | u)}{P(v | u)}
$$

When we sum over probabilities like this, this is basically an expectation value. So, we can rewrite this as an expectation value of this log of $Q$ over $P$ term under the $Q$ probability measure. We can separate the log term into a difference of logs.

$$
\mathbb{E}_Q[\ln Q(v | u) - \ln P(v | u)]
$$

Then, we can use Bayes' theorem. The $\ln P(v | u)$ term is the probability of the features given data. That is just the posterior in the Bayes' theorem. Taking the log, we get

$$
\mathbb{E}_Q[\ln Q(v | u) - \ln P(u | v) - \ln P(v) + \ln P(u)]
$$

So, we expand the posterior into three terms: the likelihood of the data $P(u | v)$, the prior $P(v)$, and the evidence $P(u)$. The evidence is a constant with respect to the approximate posterior $Q(v | u)$, so we can ignore it when minimizing the KL divergence.

Then, we rewrite this by taking the prior and putting it together with the first term, and then we separate out the other two terms.

$$
\mathbb{E}_Q[\ln Q(v | u) - \ln P(v)] - \mathbb{E}_Q[\ln P(u | v)] + \ln P(u)
$$

The first term is nothing but another KL divergence, except that what we have is the divergence between the approximate posterior $Q(v | u)$ and the prior probability $P(v)$. The other terms are the expected value under the $Q$ measure of the log probability of sensory data (the likelihood of the data) and the evidence.

We can take the term $\ln P(u)$ out of the expectation operator because it does not depend on $Q$ at all.

$$
\underbrace{\mathbb{E}_Q[\ln Q(v | u) - \ln P(v)] - \mathbb{E}_Q[\ln P(u | v)]}_{\text{Free Energy}\,F} + \underbrace{\ln P(u)}_{\text{Constant}}
$$

The first two terms are the Free Energy.

The term $\mathbb{E}_Q[\ln P(u | v)]$ is, roughly speaking, how surprising is the sensory data. What is the surprise of this data, given that I am assuming a feature $v$. It's a negative log, so it goes from +infinity to 0. The more surprising the data, the more we get penalized.

If the data is not very surprising at all, if it's the kind of data we would expect given the feature, then this value is close to zero.

The expectation is taken with respect to $Q$, so it's the average surprise of the data given the feature.

In other words, this term tells us how good a fit is this explanation for the data.

The first leading term, $\mathbb{E}_Q[\ln Q(v | u) - \ln P(v)]$, is the KL divergence between the approximate posterior that we've learned and the prior.

Why is this called Free Energy?

We can rewrite this into another form that is isomorphic with Helmholtz Free Energy in thermodynamics.

$$
F = \underbrace{\sum_v Q(v | u)[\underbrace{-\ln P(v, u)}_{\text{Energy}\,E_v}]}_{\text{Energy}\,\bar{E}} - \underbrace{\sum_v -Q(v | u)\ln Q(v | u)}_{\text{Entropy}\,H}
$$

The term on the LHS is the average energy of the system. The term on the RHS is the entropy of the system. The (average) energy minus entropy is the Free Energy.

Why is $-\ln P(v, u)$ the energy of the system? Because of Boltzmann distribution, energies are related to probabilities through an exponential:

$$
p_v = \frac{e^{-\beta E_v}}{Z}
$$

If we take the log of both sides, we get

$$
\ln p_v = -\beta E_v - \ln Z
$$

---

The posterior belief is, roughly speaking, the weighted average of the priors and the sensory evidence. The weights of the weighted average are the precisions of the distribution. Precision is inverse variance.

Precision weights influence the balance of the higher-level prior models and the bottom-up data in the perceived gestalt.

The Global Predictive Hierarchy—vision, audition, motor, olfaction, gustation, somatosensation, interoception, proprioception, etc., kind of come together.

Phenomenal self-model: the self is an internal model within a hierarchical predictive processing framework.

Minimal phenomenal self—references:

- Metzinger, T. (2004a). Being No One: The Self-Model Theory of Subjectivity.
- Metzinger, T. (2004b). The Subjectivity of Subjective Experience: A Representionalist Analysis of the First-Person Perspective.
- Metzinger, T. (2003). Précis of Being no one.

Our conscious experience, to the extent that we are conscious of the generative model, will be the contents of the generative model. This will become a Predictive Processing theory of consciousness. If it is worked out, the computational neurophenomenology assumption is that the contents of our generative model are the contents of our conscious experience to the extent that we are conscious of it.

In my generative model, we have a self-avatar, thoughts, visual, auditory, visceral sensations, proprioception, smells, sensations of the breath at the nose, sense of the heartbeat, sounds, and emotions. All these contents of the generative model are organized into phenomenal self-models. They are organized into subject-object duality—a sense of Cartesian theater.

The fact that we are not really aware of the phenomenal self-model is called phenomenal transparency, according to the philosopher Thomas Metzinger.

The real fruit of the Free Energy Principle and Predictive Processing framework is that we can put action into the same framework to minimize Free Energy. That is called Active Inference. It unifies action and perception in a single framework.

Karl Friston came up with this idea around 2008/2009. The goal states are embedded into the priors. Say we reach for an apple. Getting the apple is in my prior—I have a _prior expectation_ to get the apple. That's my reward. Then, immediately, there's a prediction error between where my hand is at the moment and where I want it to go—getting the apple. This prediction error will be resolved not by changing my perception but by moving my muscles—and doing action. Inference and action are resolved together, and there's movement trajectory until prediction error is minimized, and I got the apple.
