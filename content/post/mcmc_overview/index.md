+++
title = "Markov Chain Monte Carlo"
subtitle = ""

# Add a summary to display on homepage (optional).
summary = "A summarised and on-the-go completed list of MCMC methods"

date = 2019-03-22T19:21:12+01:00
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
+++
Markov chain Monte Carlo methods are stochastic (as opposed to deterministic)
approximation schemes which allow us to sample from complicated multi-dimensional
distributions. Briefly put, the main idea is to construct a Markov chain on the
state space whose stationary distribution is the density $p^\*(x)$ we wish to
sample from.

Wait, what? Can you repeat that?

Yep, this general method builds up on a lot of concepts, which I won't have time
(nor space) to explore in one single article. Let's be honest, you wouldn't
read the whole thing anyway.

Sooo, here is the deal. I have been reading a lot (_a lot_ 🤓) of papers on this
issue, and one of the things that really confused me was that I could not order
or organize the different approaches in my head. So this first article is for
those who already have a basic understanding of MCMC and wish to dig deeper but
are, as I still am, often overwhelmed by this micro-field's jargon and creative
mathematical thinking.

* **Metropolis Hastings algorithm**
  * **Metropolis algorithm**: Here, the proposal distribution is symmetric, meaning
  $$q(A|B)=q(B|A)$$ and the acceptance probability simplifies to
  $$
  A_k(z^\*, z^{(\\tau)})=\\min\\Bigg(1,\\frac{\\tilde{p}(z^\*)}{\\tilde{p}(z^{(\\tau)})} \\Bigg)
  $$
  * **Gibbs sampling**: You always accept the new sample: $q\_{k}(z*|z) = p(z^\*\_k|z_{\sim k})$
  The fact that the acceptance rate is 1 does not mean that Gibbs will converge
  rapidly, since it only updates one coordinate at a time.
  * **Random walk Metropolis algorithm**: the proposal distribution is set as a gaussian
  distribution centered on the current state, meaning:
  $q(x’|x) \sim N(x’|x, \Sigma)$
  * **Independence sampler****: the new state is independent of the previous state $q(x’|x) = q(x’)$
  * **Adaptive MCMC**: change the parameters of the proposal as the algorithm is
  running to increase efficiency. This allows one to for example start with a
  broader covariance and hence do large moves through the space until a mode
  is found, where a narrowing of the covariance would ensure careful exploration
  of the region around the mode.
  * **Data-driven MCMC**
* **Slice sampling**
* **Multiple-try Metropolis**
* **Reversible-jump**
* Hamiltonian (or Hybrid) Monte Carlo (HMC)
