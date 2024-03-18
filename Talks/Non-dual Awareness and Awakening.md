<iframe width="560" height="315" src="https://www.youtube.com/embed/WvPtqGp9PHA?si=d-DCLFvc5SWa6op4" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

By [[Shamil Chandaria]]

[[Immanuel Kant]]: Are we seeing things as they really are, or are we trapped in our minds?

Kant distinguished between the phenomenal world as it appears to us, our experience of the world—and the things in themselves ("ding an sich"), the noumenal world.

Kant's idea was that space, time, and causality are fundamental parts of our perceptual framework. These are called the Kantian hyperpriors.

Kantian's "Copernican Revolution": objects must conform to our cognition rather than our cognition conforming to objects.

We have the environment. Certain features of the environment give us sensory data. From that, we have to form a posterior distribution, i.e., what is the probability of certain features, e.g., $P(ext {tree}| ext {data})$.

The way to solve this problem theoretically and optimally (in terms of information theory) is Bayesian inference, which is based on Bayes' theorem.

![[Non-dual Awareness and Awakening 7-14 screenshot.png]]

The probability of $P(\text{data}|\text{tree})$ is called the likelihood of the data. It specifies the probability of the data if the observed object indeed was a tree.

However, solving this problem is generally intractable, because we can't estimate the normalizing term to make sure that the probabilities sum up to one. To calculate the normalizing term, we would have to consider every single hypothesis of what the object could be.

We can take inspiration from deep neural networks.

![[Non-dual Awareness and Awakening 9-19 screenshot.png]]

We feed in sensory data, e.g., pixels, and eventually, we get a vector of features.

We train such a network by comparing its prediction with ground truth (supervised learning). For example, the network says, "It's a cat," but the ground truth is that it's a dog. That sets up a prediction error, the difference between them. We normally square it to keep it positive and use backpropagation to adjust the neural weights so that the network gets ever so slightly better at recognizing the features of the world.

![[Non-dual Awareness and Awakening 10-51 screenshot.png]]

Supervised learning works great, but there's a problem: there is no supervisor in the brain. Who is telling us the ground truth data? We only have the data. We don't have access to the "ground truth" of the world. We only have our sensory data.

What is the one type of truth that we have access to? The sensory data itself. So, the trick in machine learning and the brain is to put another network on top of the features, which, given features, predicts the sensory data. Then, we compare the predicted data with the actual data we get, giving us the prediction error.

The network that extracts the features given sensory data is called the [[Recognition Model]] (encoder). The network that predicts the sensory data given features is called the [[Generative Model]] (decoder). The representation in the middle is sometimes called "code," e.g., in [[Predictive Coding]].

![[Non-dual Awareness and Awakening 13-16 screenshot.png]]

The recognition model is very difficult to learn. It is highly non-linear. [[Variational Autoencoder]] trains using an extra feature, minimizing the prediction error while being constrained by priors over features coming from higher levels.

![[Non-dual Awareness and Awakening 14-20 screenshot.png]]

So, instead of doing Bayesian inference, we minimize the Free Energy.

![[Non-dual Awareness and Awakening 14-45 screenshot.png]]

The first part is surprise, which roughly speaking is "What is the prediction error?" We want the model (our perception) to fit the data. Then, there's the second term, which says how far away my guess at what's going on is compared to my prior. Roughly speaking, that's minimizing Free Energy.

![[Non-dual Awareness and Awakening 16-43 screenshot.png]]

Minimizing Free Energy, Predictive Processing, and Active Inference are the closest things we have in neuroscience to how the brain works.

In the brain, the generative model doesn't sit on top of feature vectors. It folds back onto the network.

![[Non-dual Awareness and Awakening 17-26 screenshot.png]]

We have feed-forward networks and feed-back connections that go back to where the data comes in. It was always a mystery why there are ten times as many feed-back connections in the brain as there are feed-forward, and the reason is because we are not processing data and then figuring out what is going on. We are guessing at what's going on, having a generative model predicting what's going on, and then the only thing that's passed up—the data is not passed up, surprisingly—is the prediction errors.

We are simulating our experience, and we are only getting errors.

![[Non-dual Awareness and Awakening 19-14 screenshot.png]]

Where do the priors come from? Features have to be constrained by priors. Otherwise, learning would not happen. Priors come from models a layer above, and those priors come from a model a layer above that.

The basic modules of the brain are thought to be a hierarchical predictive processing architecture. The higher-level priors (or beliefs) drive the whole system.

![[Non-dual Awareness and Awakening 20-44 screenshot.png]]

The output of the generative model is the approximate posterior, the inferred features.

The key to the computational neurophenomenological hypothesis is that what we actually see is the output of the generative model.

Hard problem of consciousness: there's an explanatory gap between our first-person perspective, our experience, and our third-person view of what's going on, e.g., neural firings. How do we connect the two?

This computational model allows us to bypass the gap. It is telling us how the algorithms are instantiated in the brain, but it is also telling us, what we would perceive. What we would experience.

The leading theory of how psychedelics work is precisely in this graph here:

![[Non-dual Awareness and Awakening 22-28 screenshot.png]]

How do we weigh the influence of the prior vs. the sensory data? How much should we trust our prior and ignore the data? How much should we trust the data? Especially if they are in conflict, there has to be some balance between them.

The simplification when the distributions are Gaussian is roughly that the prior is weighted depending on what the precision (inverse of the variance) of the distribution is.

When we have a large variance—very spread-out distribution—it is not very precise. In the case above, the posterior is closer to the data than the prior, because the data is more precise.

So, the priors are weighted according to precision weights. These precision weights also weigh the prediction errors going up.

![[Non-dual Awareness and Awakening 24-24 screenshot.png]]

These precision weights can be modulated depending on what's happening. Neuromodulators—dopamine, serotonin, noradrenaline, acetylcholine—these neuromodulators actually impact global priors.

Let's say we are getting a major prediction error with lots of uncertainty around it. Then I get a global signal, noradrenaline, I get stressed, and I say, "Oh! I don't think I know what's going on here. I'd better increase my learning rate." That suddenly downweighs the priors and upweighs the data (attention).

![[Non-dual Awareness and Awakening 25-53 screenshot.png]]

What is the cortical hierarchy through fMRI data? We have a hierarchy of abstraction, conceptualization, and compressing data.

The experience that we are having now is a gestalt.

![[Non-dual Awareness and Awakening 31-1 screenshot.png]]

All these pieces of the hierarchy are organized into a sense of self. This sense of self has many dimensions. The most basic is the subject-object duality.

![[Non-dual Awareness and Awakening 31-16 screenshot.png]]

I am here, seeing a tree over there. Everything is in reference to the self. The most critical/interesting thing about this self model (phenomenal self-model) that we must have is that it's transparent in the sense we can become aware of what we are doing, e.g., looking through a window. We can both do something and be aware that we are doing it. Our self-model is a mental construction.

![[Non-dual Awareness and Awakening 34-41 screenshot 1.png]]

Families of meditation:

- Attentional: Pay attention to given objects, narrow or broad.
- Deconstructive: Deconstruct the experience.
- Constructive: Things like loving-kindness, [[Yidam]] practices—becoming the image of the goddess, etc.

Focused Attention Meditation: paying attention to the breath at the nose, or the lower belly, or any other place.

Paying attention is increasing the precision weighting on the sensory data. The posterior moves closer to the sensory data that we pay the attention to. The experience is dominated by the sensation of the breath at the nose.

![[Non-dual Awareness and Awakening 37-29 screenshot 1.png]]

Everything else fades in the background.

![[Non-dual Awareness and Awakening 37-46 screenshot 1.png]]

Our conscious experience is essentially a weighted average of everything that we are experiencing, and these weights are precision weights.

We are training our attention and our meta attention. We are becoming masters of manipulating our precision weightings. We found our way out of monkey mind, we've quieted the mind.

The next phase of the practice is where we start to deconstruct things.

![[Non-dual Awareness and Awakening 38-59 screenshot 1.png]]

Start to notice all the micro-sensations. See yourself as a sea of burbling micro-sensations. Tune into the object as a whole or just the parts. Say "dog, dog, dog, ..." over and over again, and notice how you disconnect from the concept and start noticing low-level sounds.

If we can do precision modulation in the brain, we can end up deconstructing these constructs carefully constructed by the brain.

![[Non-dual Awareness and Awakening 41-37 screenshot 1.png]]

We are decreasing the precision weighting of these priors. We are downweighing the top-level beliefs, the core beliefs, and go down the cortical hierarchy.

As we start to deconstruct the world, the objectness disappears. We go through a process of de-reification.

When we naively thought we were seeing the tree, that's called [[Naive Realism]]—the tree is really there, absolutely, it's real. Through de-reification, we realize it is just a construction.

When things become de-reified, they become empty. They lack inherent existence. We see that they are just a construction.

![[Non-dual Awareness and Awakening 44-47 screenshot 1.png]]

If we can get our practice to be that good, we can start to recognize the empty space of the phenomenal experience itself.

![[Non-dual Awareness and Awakening 45-22 screenshot 1.png]]

Recognize the awareness itself, except it's not the normal dual awareness of subject and object because they are deconstructed. It is the substrate of the generative model itself.

![[Non-dual Awareness and Awakening 45-53 screenshot 1.png]]

This pure awareness has been the peak of many spiritual traditions. When we come back after recognizing this pure awareness, when things re-arise, we notice that this pure awareness has been there all along.

![[Non-dual Awareness and Awakening 48-24 screenshot 1.png]]

[[Non-Dual Awareness]]

[[Thomas Metzinger]] started studying something he called the [[Minimal Phenomenal Experience]]. That is the pure deep samadhi state of just this non-dual awareness, empty of everything else. What are the features of this space?

- The Epistemic space—it is the space of knowing.
- Presence, pure being.
- Luminous empty openness—the light of consciousness illuminates all objects. It has the capacity to illuminate.
- Inherent reflexivity—it knows itself. In our normal understanding, we have have a subject—"we," the subject, is seeing something. In the non-dual awareness, subject arises within awareness. The subject is not what's observing. It was always the awareness that was aware. Our self-model just usurped that awareness capacity and gave us this illusion of subject-object duality.
- Awakeness—that awareness is awake.
- Spaciousness—there are no boundaries. All boundaries are within this awareness.
- Silent stillness—sounds and motion arise within it.
- Timelessness—occurrences happen within awareness. The flow of time happens within awareness. So, the non-dual awareness is timeless.

![[Non-dual Awareness and Awakening 52-40 screenshot 1.png]]

Plato's allegory of the cave. Awakening is awakening to the nature of our being, of our experience. Awakening is knowing the substrate and the modulations of the generative model itself.

When we wake up to the nature of the generative model—the phenomenal experience is a construction—and that this construction is made of awareness that is essentially non-dual, that is the idea.

![[Non-dual Awareness and Awakening 54-51 screenshot 1.png]]

We have a prior that we will get the reward and when we don't have it, there's a prediction error. I want it, and I don't have it. I need to minimize the prediction error. How do I do that? By acting we minimize the prediction error and reduce free energy. Moving toward the rewards or away from what we don't want, is minimizing free energy.

In physiological terms, moving toward homeostasis is where we want to be, and any prediction error from this homeostatic signal is a discomfort.

We end up with this Free Energy landscape.

![[Non-dual Awareness and Awakening 57-2 screenshot 1.png]]

The lower we are on this surface, the closer to homeostasis we are and the closer to our value function that we are away from high prediction errors. The local minimum is an attractor basin. We have deviations from that minimum caused by surprising fluctuations in the environment. These deviations from being at the minimum are frustrations of our preferences. We want to be at the minimum. We want to be in a good state. We want to be in the state where we are satiated. These deviations are the basis of negative valence. This negative valence is important from an evolutionary perspective because that's what spurs us into action. But, the stochasticity of the environmental fluctuations is inexorable. Therefore, any system with preferences will inevitably be characterized by bouts of negative valence.

![[Non-dual Awareness and Awakening 58-49 screenshot 1.png]]

This argument is, roughly speaking, Buddha's First Noble Truth, rightly so from the evolutionary perspective.

How do we reduce suffering?

From the ground of being, some phenomena—sensations—arise. As soon as a sensation arises, there's a prior associated with it, e.g., "This is how things should be, and this is what I have." And as soon as there's a prior there, there's a prediction error. And the prediction error is dissatisfaction. But that's only the half of it. Then you get mental proliferation, buzzing and burbling, "That shouldn't be the case! Why is this thing happening to me?" and you often go into a spin (_papañca_, conceptual proliferation).

![[Non-dual Awareness and Awakening 60-24 screenshot 1.png]]

Metzinger has four necessary conditions for suffering:

- Negative Valence—the things aren't the way you want them to be.
- Conscious Experience.
- Phenomenal Self Model—"This pain is mine."
- Transparency—it is real. It is really there, we can't see it.

How do we get out of that? Seeing through the transparency into opacity and seeing there was a window. If we do that and make it fully opaque, the entire phenomenal property of experiential selfhood, which is only a construction, will disappear, and suffering will stop. We have the technology for that.

![[Non-dual Awareness and Awakening 1-1-57 screenshot 1.png]]

What happens is that the prediction errors, the priors, and the mental proliferations become empty. There's an emptiness of phenomena and the emptiness of self. They become de-reified. Therefore there's a reduction in mental proliferation, reduction the gripping. That gripping is what drives craving and aversion, the push and pull towards it, the approach behaviour and the avoidance behavior. The frustration of this craving is what's causes suffering and therefore there's a reduction in suffering.

![[Non-dual Awareness and Awakening 1-3-3 screenshot 1.png]]

After deconstructing ourself, we reconstruct ourself. With meditation we are reducing the top-level weighting of our core beliefs, our top-level priors (cf. REBUS model, Relaxed Beliefs Under Psychedelics). And when we reduce those top-level beliefs, we go into a reprogramming mode. We have flattened the Free Energy landscape, the priors are no longer these deep attractor basins in that landscape. What new program do we want to upload?

![[Non-dual Awareness and Awakening 1-3-11 screenshot 1.png]]

![[Non-dual Awareness and Awakening 1-5-15 screenshot 1.png]]

The experience of the world is a construction. It is a constrained construction. It is a constrained hallucination, constrained by our sensory data. It is constrained by our current priors, beliefs, and high-level models. We have this external data, we have a way of looking at it—a lens—and we end up with the experienced world. The world that we experience confirms our prior. But not all priors are like this.

![[Non-dual Awareness and Awakening 1-7-2 screenshot 1.png]]

A stable prior is reinforced by the sensory data, by the experienced world.

![[Non-dual Awareness and Awakening 1-7-55 screenshot 1.png]]

We end up with this landscape of attractor basins that we can choose.

![[Non-dual Awareness and Awakening 1-8-56 screenshot 1.png]]

Awakening vs. liberation. Awakening is waking up to the nature of our reality, to the pure awareness itself, the substrate of existence, of our experience. Liberation is changing our priors into more beautiful and helpful ways of seeing the world. As we awaken, this gives us more ability to enter the reprogramming mode, and we have more room between the stimulus and response. We can start to respond not in the usual habitual ways we have always responded. Then we see the world in new ways, which allows us to go deeper into the awakening, which then leads to more liberation, which then leads to more awakening, and so on.

![[Non-dual Awareness and Awakening 1-10-55 screenshot 1.png]]

![[Non-dual Awareness and Awakening 1-11-9 screenshot 1.png]]

![[Non-dual Awareness and Awakening 1-11-32 screenshot 1.png]]
