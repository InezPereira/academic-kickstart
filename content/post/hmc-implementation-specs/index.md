+++
title = "Hamiltonian Monte Carlo Implementation specifics"
subtitle = ""

# Add a summary to display on homepage (optional).
summary = ""

date = 2019-03-24T12:53:19+01:00
draft = true

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = []

# Is this a featured post? (true/false)
featured = false

# Tags and categories
# For example, use `tags = []` for no tags, or the form `tags = ["A Tag", "Another Tag"]` for one or more tags.
tags = []
categories = []

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["deep-learning"]` references
#   `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
# projects = ["internal-project"]

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
[image]
  # Caption (optional)
  caption = ""

  # Focal point (optional)
  # Options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
  focal_point = ""

# references
links = [{name="Read more in", url="http://www.mcmchandbook.net/HandbookChapter5.pdf"}]

+++
Hamiltonian Monte Carlo is a variant of MCMC first presented under the name of
"hybrid Monte Carlo" in the 1987 paper by Duane, Kennedy, Pendleton and Roweth.

It scales better with higher dimensionality than simpler Metropolis methods, and
the main reason for that is that it avoids performing a simple random walk
exploration of the state space.

The following definitions and tips follow the notation and were taken mainly from
Radford M. Neal's chapter ["MCMC Using Hamiltonian Dynamics"](http://mcmchandbook.net/HandbookChapter5.pdf),
from the book _Handbook of Markov Chain Monte Carlo_ from Brooks _et al._
If you're looking for more detailed information on HMC, be sure to check it out, along with
Michael Betancourt's [conceptual introduction to HMC](https://arxiv.org/abs/1701.02434).
They amount to more than 100 pages, but they are very worth your time, if you're
looking to take a deep dive into the matter.

In HMC, we define the Hamiltonian as follows:
$$H(q,p) = U(q) + K(p)$$
where $q$ is a $d$-dimensional **position** vector and $p$ a $d$-dimensional
**momentum** vector. $U(q)$ is defined as the **potential energy** and equal to
the negative log probability density of $q$, plus a constant. $K(p)$ is the
**kinetic energy** and defined as:
$$K(p)=\frac{p^TM^{-1}p}{2}$$
where $M$ is a symmetric, positive-definite "mass matrix". $M$ is typically a
diagonal matrix, often a scalar multiple of the identity matrix. The above form
for the kinetic energy function is actually the negative log probability density
of a zero-mean Gaussian with covariance matrix $M$.

**First of all, when _can't_ you use HMC?**

* When you have discrete variables.
* When the derivatives of the potential energy with respect to some of the
variables are expensive or impossible to compute.

A few tricks and good practises to get your hamiltonian Monte Carlo sampler to work:

* **Doing several runs with different random starting states is advisable** (for both preliminary
and final runs), so that problems with isolated modes can be detected. Note that HMC is no less (or more) vulnerable to problems with isolated modes than other MCMC methods that make local changes to the state. If isolated modes are found to exist, something needs to be done to solve this problem—just combining runs that are each confined to a single mode is not valid. A modification of HMC with “tempering” along a trajectory (Section 5.5.7) can sometimes help with multiple modes.

* **Tuning $\epsilon$ and $L$**: "It is possible that the best choices of ε and L for reaching equilibrium are different from the best choices once equilibrium is reached, and even at equilibrium, it is possible that the best choices vary from one place to another. If necessary, at each iteration of HMC, ε and L can be chosen randomly from a selection of values that are appropriate for". Ouch, Neal.
  * One rule of thumb could be to make $\epsilon$ proportional to $d^{-1/4}$ to maintain a reasonable acceptance rate.

* **Randomize your choice of $\epsilon$ and/or $L$**: when applying the leapfrog
algorithm, you can for example sample $\epsilon$ and/or $L$ uniformly from a
small interval.
   * **Why?**: to avoid non-ergodicity. If you solutions are periodic and $L\epsilon$
   approximates the value of the period, you might actually get stuck or take
   a very long time to explore the full state space.
* **If you suppose q has approximately a Gaussian distribution and you have an
estimate of the covariance matrix $\Sigma$**:
  * **Transform the variables so that their covariance matrix is the identity**:
  meaning, compute the Cholesky decomposition of $\Sigma = LL^T$ and define $q'=L^{-1}q$.
  Define the Hamiltonian using $q'$ and retrieve $P(q)$ by observing:
  $$ P'(q')=\frac{P(q)}{|\text{det}(L^{-1})|}=\frac{P(Lq')}{|\text{det}(L^{-1})|}$$

To make things easier, you can define $M$ as the identity matrix, which will
simplify the kinetic energy to: $K(p)=p^Tp/2$.

  * **You can also keep the original $q$ variables and redefine the kinetic energy
  function** as: $K(p)=p^T\Sigma p/2$. In this setting, the momentum variable
  hence have $\Sigma^{-1}$ for a covariance matrix.
  This type of kinetic energy function has been used to compensate for correlated
  position variables. However, in higher dimensions, the computational cost
  incurred because of the matrix operations might limit its usefulness.

* **Combine HMC with other MCMC variants**: "When both HMC and other updates are used, it may be best to use shorter trajectories
for HMC than would be used if only HMC were being done. This allows the other updates to be done more often, which presumably helps sampling. Finding the optimal tradeoff is likely to be difficult, however.Avariation onHMC that reduces the need for such a tradeoff is described below in Section 5.5.3."
