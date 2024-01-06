# Part 1

<iframe width="560" height="315" src="https://www.youtube.com/embed/H5AolqFl2Nw?si=mcsQtLseuB8hmr3p" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

Active Inference, as formulated in terms of partially observable decision processes, is a particular discrete-space generative model. It doesn't require knowing many things people discuss more broadly concerning the Free Energy Principle. It appeals to Free Energy and Expected Free Energy as more or less cost functions for figuring out the best choice. We can see the Active Inference models, at least the MDP formulation, as a particular flavor of model-based reinforcement learning.

It allows for a fully unified Bayesian way of doing RL. We do that by, instead of calling something a reward per se, we define a probability distribution over observations, which is called a preference distribution. The reward then becomes a probabilistic preference to observe some things over others. An agent is driven to make decisions to get it to observe what it prefers. This preference distribution is a way of specifying what is rewarding to the agent.

Making decisions based on minimizing the Free Energy doesn't just try to maximize the reward. It also simultaneously tries to maximize the information gain.

Say an agent starts in a dark room, which means it doesn't know where anything is. It means there is a lot of uncertainty over what state it's in. Let's say simultaneously, in another room, there's a fridge with some food. Then, there will be two different drives there: the epistemic drive to do whatever it thinks will give the agent the most information, e.g., turn on the light, and that's not reward per se. The agent tries to choose the action that maximizes the information it gets. The other drive is to maximize the preferred outcomes, so the agent will also be driven to leave the room and go to the fridge to observe himself eating the food.

The agent is not trying to maximize the reward directly. It will choose the action to help it figure out where it is so that it is more confident regarding what to do to get the reward later.

These models are a fully Bayesian way to integrate perception, learning, and decision-making, where decision-making is driven to maximize information gain and reward.

Papers comparing Active Inference and RL:

- https://pubmed.ncbi.nlm.nih.gov/33400903/
- https://direct.mit.edu/neco/article/35/5/807/115249/Reward-Maximization-Through-Discrete-Active

Informal tutorials:

- https://medium.com/@solopchuk

Active Inference framework, specifically the POMDP instantiation of Active Inference, is a corollary or a derivative of the Free Energy Principle.

Karl Friston's [[Statistical Parametric Mapping]] (SPM) software was the original way of doing fMRI—analyzing functional neuroimaging data. Karl Friston also invented Dynamic Causal Modeling (DCM), a particular neuroimaging approach.

Take a particular behavioral task. We have to determine the right generative model for that task. Once we have the generative model set up, we can run simulations. The simulations generate observations and expected actions. Then, we need data from a participant performing that task where we know on each trial what the participant observed—what the task stimuli were—and what action the participant chose. Then, we do a parameter estimation—find the set of parameter values in the model that generates behavior most similar to what the participant did.

# Part 2

<iframe width="560" height="315" src="https://www.youtube.com/embed/bDJbEofbvyk?si=WqIqscuJvzRLkTLj" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Perception as Bayesian Inference

We see this two-dimensional image. We are trying to infer, based on prior expectations, whether, three-dimensionally, it is a concave or convex shape.

![[ActInf ModelStream 001.2 A Step-by-Step Tutorial on Active Inference 20-54 screenshot.png]]

For simple problems, we can do that exactly by solving Bayes' theorem, but in most cases, it is intractable.

In Active Inference, we define the expected free energy $F$, which is more or less a measure of the accuracy of predictions minus the accuracy of beliefs combined with the complexity of those beliefs. How much do we have to change our beliefs to get a model that's accurate?

While finding a set of beliefs that minimize the expected free energy—beliefs that are accurate while changing as little as possible—we get as close as possible to the true answer that Bayes' theorem would give us.

![[ActInf ModelStream 001.2 A Step-by-Step Tutorial on Active Inference 21-43 screenshot.png]]

## Generative Process vs. Generative Model

We have some true generative process going on in the world—true states and the observations that they generate—while the brain has a model: "What state must I be in, given this observation?" The brain is trying to come up with a representation that best matches what's going on in the generative process. $\pi$ is the policy. What's the most likely action I ought to choose given that the world is this way and given that I prefer some observations over others?

![[ActInf ModelStream 001.2 A Step-by-Step Tutorial on Active Inference 22-50 screenshot.png]]

## Setting Up a Generative Model

We have states $s$, and the observations $o$, initial prior expectations $D$, beliefs about state transitions $B$. In Active Inference, policies $\pi$, the different action sequences that we may choose, are modeled as things that entail different transitions between states. The choice of policy depends on the expected free energy $G$, which depends on $C$, which encodes preferences.

We are trying to find a policy that corresponds to state transitions that will generate the observations over time that are going to be as consistent as possible with our preferences, which corresponds to the lowest expected free energy $G$.

We can add habits, $E$, which give us additional priors over policies and precision parameters $\beta$, and $\gamma$, which say how precise or how reliable the model expects the expected free energy estimates to be.

![[ActInf ModelStream 001.2 A Step-by-Step Tutorial on Active Inference 25-26 screenshot.png]]

When we specify the model, we specify what the observations $o$ are, we specify the likelihoods $A$, what states generate what observations with what probability, priors over initial states $D$ and beliefs about state transitions $B$, policies $\pi$ which tell us the different possible state transitions we can choose, and agent's preferences $C$, what observations it wants to get over others.

# Part 3

<iframe width="560" height="315" src="https://www.youtube.com/embed/vacR2gYgOxk?si=Av3gx03E8l8tuK_a" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

## Neural Process Theory

![[ActInf ModelStream 001.3 A Step-by-Step Tutorial on Active Inference 7-48 screenshot.png]]

Focusing on the full generative model on the bottom-right, we have a particular set of observations over time, $o_1$, $o_2$, $o_3$, and particular hidden states—beliefs about what's going on out in the world, outside the brain—$s_1$, $s_2$, $s_3$, corresponding to beliefs at time 1, at time 2, and at time 3.

The $A$ matrix encodes the likelihood mapping—the belief about what outcomes will be present if particular states out in the world are the case.

The $B$ matrix encodes the beliefs about how, if we are in a particular state at time 1, it's going to transition to state $s_2$ at time 2, and so forth.

The vector $D$ encodes the initial prior about which state we are going to be at time 1. Then, we have policies $\pi$, which allow the agent to control some of the transitions between states.

Policies are selected based on the expected free energy $G$, which is a function of preferences $C$—the outcomes we prefer over others. Policies that transition between states that generate observations that are as close to preferences as possible are selected. Policies are also controlled by $E$, which encodes prior over policies (habits).

$\gamma$ is a dynamically updated temperature parameter that controls how much the expected free energy contributes to policy selection. $\gamma$ is updated through a hyper-parameter $\beta$.

We infer states based on observations through a set of equations that correspond to approximate Bayesian inference through minimizing free energy and expected free energy.

The main idea is how a system settles on posterior beliefs about states through free energy minimization.

Free energy can be decomposed into complexity term minus accuracy term, where accuracy means how close the predicted outcomes are to observed outcomes, and complexity corresponds to how much we have to move our beliefs from prior beliefs to posterior beliefs. In this interpretation, minimizing free energy means changing out beliefs as little as possible while also maximizing accuracy.

![[ActInf ModelStream 001.3 A Step-by-Step Tutorial on Active Inference 14-49 screenshot.png]]

![[ActInf ModelStream 001.3 A Step-by-Step Tutorial on Active Inference 15-56 screenshot.png]]

Inference corresponds to changing the activity levels, while learning corresponds to changing synaptic strengths.

Three levels of hypotheses to test:

1. At the computational level, does the brain minimize the free energy and the expected free energy, or at least is it helpful to describe it as doing that?
2. Given the above is true, which of several different algorithms is the brain using?
3. Given that the brain is using a specific algorithm, how is the brain set up to implement that algorithm?

ERP — Event-Related Potential

## Hierarchical Models

We take the exact same model as before, but now we put a layer below it, so the observations are not the actual outcomes; the observations are whatever the beliefs over states are at the lower level. The observations for the second level are the posteriors over states at the first level.

We can now select policies at the higher level and also at the lower level. States at level 2 generate states at level 1, and states at level 1 act as the observations for level 2. Level 2 operates at a slower timescale.

![[ActInf ModelStream 001.3 A Step-by-Step Tutorial on Active Inference 1-29-8 screenshot.png]]

Deep Active Inference may refer to using deep neural networks to parameterize the $A$ and $B$ matrices, or the policies, or hierarchical (deep temporal) models.

# Part 4

<iframe width="560" height="315" src="https://www.youtube.com/embed/QRGaGmT-VFM?si=OVIDptCwmCcRJCT5" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>
