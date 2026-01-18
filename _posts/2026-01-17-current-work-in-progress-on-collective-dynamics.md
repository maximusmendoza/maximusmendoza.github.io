---
layout: post
title: "Current Work in Progress on Collective Dynamics"
date: 2026-01-17
categories: ai-safety
---

<script>
  MathJax = {
    tex: {
      inlineMath: [['$', '$'], ['\\(', '\\)']]
    }
  };
</script>
<script id="MathJax-script" async
  src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js">
</script>

Truthfully, I'm only putting this out there for my PIBBSS application. What follows is an incomplete blog post that scratches the surface on an even more incomplete framework aimed at making sense of multi-agent dynamics. I believe further mathematical generalization is necessary to adequately describe real-world forms of collective intelligence. For the mathematically inclined reader, one might mentally replace "graph Laplacian" with its more powerful brother, the sheaf laplacian. 

## The unreasonable robustness of life 

When you think about it, multicellular organisms are pretty fucking wild. You are made of trillions of individual cells coordinating with one another across vast and complex networks to form a single cohesive entity. They make man-made organizational structures look small and brittle. After only a few thousands people, organizations tend to become weighed down by their own internal bureaucratic structure. In contrast, the human body, with orders of magnitude more moving parts, operates like a well oiled machine (most of the time). Even larger human institutions like the stock market still only consist of millions of agents, orders of magnitude less than your body. And for human organizations, once you get to that scale, steerability of the system goes out the window. 

Not only that, but the adaptability of multicellular organisms is incredible. Think about the human brain, which can rewire itself on the fly. In blind individuals, the visual cortex is repurposed to process auditory, spatial, and tactile information. In extreme cases of pediatric epilepsy, surgeons may remove an entire hemisphere of the brain. The remaining hemisphere can often reorganize to take over motor control for both sides of the body and even support language function that was previously lateralized to the removed side.

Or take your bones, which are piezoelectric. When you apply mechanical load, it generates a transient electrical dipole. Osteocytes (bone cells) sense these electrical signals and direct osteoblasts to build new bone density exactly along the lines of stress. This is why, for example, a professional tennis player’s dominant arm bones are significantly denser and thicker than their non-dominant arm. There's a reason "life finds a way" is a saying. 

So how does life do it? Further, is there a way we can take the principles life leverages in growing adaptive collective intelligences to design human (and AI) institutions that are more robust and aligned?

Well if we had the full answer medicine, biology, economics, governance, and many other fields would probably look a lot different than they do today. Nonetheless, the study of collective intelligence has gone a long way in recent years and provides much insight into understanding how collections of information processing agents interact to form intelligent systems. 

## Graphs as a minimal but sufficiently general mathematical toolkit for collective intelligence 

One of the primary issues with the existing science of collective intelligence is its fractured nature. There exists a plethora of partial theories: active inference, game theory, network science, etc. The question is then, what mathematical structures sit at the intersection of these theories, and how may they be abstracted upon? We argue that graphs are (to first approximation) a sufficiently general means for capturing the underlying dynamics of the systems these theories describe. Any theory of collective intelligence must answer certain basic questions: Which agents can influence which other agents? How strongly? Through what pathways? Graphs offer a straightforward way of representing agents and their relationships while also providing a rich toolkit of mathematics to work with.  

Now of course saying that graphs are a useful way to represent relationships isn't very insightful. That statement in and of itself is pretty obvious. Perhaps a less trivial assertion that we are making is that spectral graph theory can itself be used as a means of studying collective behavior.

To see how, let's look at a collection of agents. We can model this as a graph $G = (V, E, w)$, Where the set of nodes $V$ corresponds to agents and the set of weighted edges $E$ correspond to coupling strengths between them. 

Why are graphs the correct abstraction here? If we strip away the specific terminologies of game theory, network science, or active inference, we find that all these describe systems composed of distinct entities that interact to process information. Whether these are neurons firing via synapses or market makers trading via fiber optics, the fundamental unit of analysis is the interaction between agents. Graphs provide the minimal sufficient statistic for this structure—some way to formalize "who listens to whom" without over-committing to specific dynamical laws just yet.

## A short detour into Bayesian mechanics 

However, structure alone does not explain intelligence. We must also consider the objective.
One influential framing here is the Free Energy Principle. Roughly, if a system reliably persists, it must keep itself within a limited range of sensory states over time. Under additional assumptions (a stable statistical boundary separating internal from external variables, and a steady-state distribution), this corresponds to low expected surprise of its sensory observations, or equivalently low sensory entropy in the long run. But directly evaluating surprisal, $-\log p(o)$, is generally intractable.
Instead, the theory introduces variational free energy, $F$, which upper-bounds surprisal:
$$
F(q,o)= -\log p(o) + \mathrm{KL}(q(s),|,p(s\mid o)).
$$
This identity makes the tradeoff precise. Free energy equals surprisal plus a divergence between an approximate posterior $q(s)$ and the true posterior $p(s\mid o)$ implied by the system’s generative model. Minimizing $F$ with respect to $q$ reduces that divergence to the extent the variational family can represent the true posterior. In active inference, action can also reduce $F$ by changing observations (so you are not only fitting beliefs to data, you can also seek data that makes your beliefs self-consistent). On this view, a system’s internal dynamics can be interpreted as approximate Bayesian (variational) inference and control under an implicit generative model. That interpretive step is stronger than the variational identity alone, but it is the sense in which “self-maintenance” can be linked to inference.
Separately, the Conant-Ashby Good Regulator theorem sharpens the intuition: effective regulation requires an internal organization that captures the relevant regularities of the environment, in the minimal sense needed for control. Put together, these viewpoints motivate the idea that surviving collectives must encode, distribute, and update something model-like, even if it is only approximate and only defined relative to the task of staying viable.

## Collective dynamics 

This raises the practical question: how does a collection of agents perform anything resembling a unified inference? At minimum, they have to couple their internal states. The coupling functions in biological neural networks or transformer attention heads can be highly non-linear, but a first-order approximation of “influence” is simple diffusion. If we posit that agents update their beliefs by local error correction, moving their state toward the states of their neighbors, then we can model coupling between the individual and the collective using the toolkit of graph signal processing. If we treat agent beliefs as signals on a graph, we can use spectral methods to decompose complex collective behaviors into fundamental modes, giving us a rigorous way to analyze how information diffuses, integrates, and creates consensus.
To make this rigorous, we turn to graph signal processing. In classical signal processing, we analyze time-series data by decomposing it into sine waves of varying frequencies using the Fourier transform. We can apply the exact same logic to our collective intelligence. Here, the "signal" is not a voltage over time, but the distribution of beliefs across the network.

We assign to each agent $i$ a belief vector $x_i \in \mathbb{R}^d$. The global state of the system, $X \in \mathbb{R}^{n \times d}$, is simply the stack of these belief vectors for all $n$ agents. This is a graph signal.
If we assume the most fundamental interaction—that agents update their beliefs by minimizing surprise relative to their neighbors—they will effectively move toward the local average. This dynamic is governed by:

$$\frac{dx_i}{dt} = \sum_{j \in N_i} w_{ij}(x_j - x_i)$$

This is basic diffusion. In the language of GSP, this process acts as a low-pass filter. Just as the heat equation smoothes out temperature differences in a metal rod, this equation smoothes out belief differences across the graph edges. We can express this globally using the graph's Laplacian, $L$:

$$\frac{dX}{dt} = -LX$$

where $L = D - W$ (the degree matrix minus the weighted adjacency matrix). The Laplacian here plays the exact same role as the second derivative operator ($-\nabla^2$) in physics. Its eigenvectors define the "frequencies" of the graph: low eigenvalues correspond to smooth patterns where connected agents agree, while high eigenvalues correspond to jagged patterns of sharp disagreement.

## Leveraging spectral graph theory 

The power of this formulation lies in the spectrum of the Laplacian. Just as a prism splits white light into its constituent colors, the Laplacian decomposes the complex, messy dynamics of the collective system into independent, manageable modes of behavior. This is achieved through eigendecomposition. Since the Laplacian $L$ is a symmetric matrix, we can decompose it as:

$$L = \sum_{k=1}^n \lambda_k v_k v_k^\top$$

Here, $0 = \lambda_1 \leq \lambda_2 \leq \cdots \leq \lambda_n$ are the Laplacian's eigenvalues, and $v_1, \ldots, v_n$ are the corresponding orthonormal eigenvectors. In the context of Graph Signal Processing, these eigenvectors form the "Graph Fourier Basis." Each eigenvector $v_k$ represents a specific "standing wave" or spatial pattern of belief distribution across the network. The first eigenvector, $v_1$, is particularly special: if the graph is connected, it corresponds to the eigenvalue $\lambda_1 = 0$ and is a constant vector where every element is identical ($v_1 = \frac{1}{\sqrt{n}}\mathbf{1}$). This represents the state of perfect consensus.

The eigenvalues $\lambda_k$ tell us how "energetic" these patterns are. A small eigenvalue implies that the pattern varies slowly across the graph; neighboring agents have similar values. A large eigenvalue indicates a high-frequency pattern where connected agents hold sharply opposing beliefs. Crucially, the eigenvalue determines the decay rate of that specific pattern. When we solve the differential equation $\frac{dX}{dt} = -LX$, the solution takes the form of a matrix exponential, $X(t) = e^{-Lt}X(0)$. Because the eigenmodes are orthogonal, they decouple, allowing us to track the evolution of each pattern independently:

$$\alpha_k(t) = e^{-\lambda_k t}\alpha_k(0), \quad \text{where } \alpha_k = X^\top v_k \in \mathbb{R}^d$$

In this equation, $\alpha_k$ represents the magnitude of the $k$-th eigenmode in the system's current state. Notice that the decay term is $e^{-\lambda_k t}$. This is the mathematical mechanism of the low-pass filter. High-frequency modes (those with large $\lambda_k$) decay extremely fast; the disagreements they represent are smoothed out almost instantly. Low-frequency modes (small $\lambda_k$) decay much more slowly, persisting for a time proportional to $\frac{1}{\lambda_k}$. The zero-frequency mode (consensus) has a decay rate of zero, meaning it never disappears. Over time, all the "noise" of disagreement filters out, leaving only the "signal" of the average consensus.

## Variance of beliefs as an energy 

We can now reconstruct the full collective state of the system by summing these independent behaviors. The total signal $X \in \mathbb{R}^{n \times d}$ is simply the superposition of all its eigenmodes:

$$X = \sum_{k=1}^n v_k \alpha_k^\top$$

This decomposition gives us a new way to think about the "disagreement" in the system. Classically, we define the total variance of the system as the sum of the squared deviations of individual agents from the population mean $\bar{x}$. However, using Parseval's identity—which essentially states that the energy of a signal is conserved whether you measure it in the standard basis or the Fourier basis—we can rewrite this variance entirely in terms of the spectral modes. Since the first mode $v_1$ represents the mean (perfect agreement), the variance is simply the sum of the energies of all the remaining non-constant modes:

$$\mathrm{Var}(X)=\frac{1}{n}\sum_{i=1}^n |x_i-\bar{x}|^2=\frac{1}{n}\sum_{k=2}^n |\alpha_k|^2$$

Hence, from a physical interpretation variance is akin to energy. In this context, the graph structure defines an energy landscape where "disagreement" corresponds to potential energy. High-frequency modes—those complex patterns where neighbors disagree strongly—carry a high energy cost. The graph Laplacian effectively measures the "tension" in the network, and because the system seeks to minimize this energy via diffusion, these high-tension patterns are unstable and decay rapidly.

We can see this clearly by looking at how the variance evolves over time. Substituting our decay solution into the variance equation, we get:

$$\mathrm{Var}(X(t))=\frac{1}{n}\sum_{k=2}^n e^{-2\lambda_k t}|\alpha_k(0)|^2$$

The total amount of disagreement in the collective at any time $t$ is a weighted sum of the initial disagreements projected onto the graph's eigenmodes. The eigenvalues $\lambda_k$ act as the "cost" of maintaining those disagreements. Patterns that run against the grain of the graph's connectivity (large $\lambda$) are "expensive" and burn out quickly. Patterns that align with the graph's natural geometry (small $\lambda$) are "cheap" and persist for a long time. Thus, the ​​Laplacian spectrum effectively dictates which disagreements are transient noise and which are durable features of the collective state.


## Generalisation in science: Future Research 

Our core premise is that the dynamics of a collective intelligence—how individual actions combine to form the collective and how the collective constrains individual actions—is governed by the relationships between agents. Graphs offer an easy way to model these relationships while also lending itself to the computational tractability of linear algebra, but it's far from the only viable mathematical structure. In particular, we believe applied category theory (which is all about objects and their relationships) offers the most natural setting to study collective intelligence. Perhaps future work involves translating this framework based on spectral graph theory into a categorical lens (pun intended for the category theorists). 

This is of course, not to undersell the power of GSP and spectral graph theory. The Laplacian is a powerful tool that is useful in describing a wide array of dynamical systems. In particular, its generalized cousin, the sheaf laplacian plays an important role in governing multi-agent coordination and consensus dynamics. If you think about the signal over a graph as agents dancing on a stage, the Laplacian tends to act as the choreographer. 

We would argue that this principle of relationships governing dynamics applies to many real world systems. All forms of intelligence are collective intelligence, whether that be neurons in the brain, people in a company, or layers in a neural network. Further, the set of systems that are conventionally considered to be intelligent is much too narrow. Humans and their specific cognitive abilities are but a small sliver of the space of intelligent systems. It is only when relaxing our assumptions, focusing less on the specific capabilities a system has and more on the way in which information flows throughout the system do we start to properly frame the notions of intelligence and agency. 

Given a common language to discuss collective intelligence, does this suggest that we may be able to "grow" our own organizations, the way organisms grow? Just as in embryogenesis where a single cell can develop into a fully functional complex organism, is it possible to “organically” (whatever that means) steer the development of multi-agent systems to create more desirable forms of collective intelligence? Instead of taking a reductionist approach and trying to control the actions of each individual agent, perhaps we can instead outline the high level characteristics we want our collective system to have. From there, we can observe how agents naturally interact, where they form distinct boundaries, or when emergent phenomena appear, and by solely acting on the relationships between agents rather than the internals of the agents themselves, guide the collective toward desirable attractors and away from undesirable ones.