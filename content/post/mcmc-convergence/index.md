+++
title = "Monitoring MCMC Convergence"
subtitle = ""

# Add a summary to display on homepage (optional).
summary = ""

date = 2019-03-28T13:44:37+01:00
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

### An overview from multiple sources

## Chapter 6 from the Handbook of Markov Chain Monte Carlo

* Burn-in: Gelman and Shirley write that they discard the first half of the samples.
* "Simulate three or more chains in parallel. We typically obtain starting points by adding random perturbations to crude estimates based on a simpler model or approximation."
* Check convergence by discarding the first part of the simulations—we discard the first half, although that may be overly conservative—and using within-chain analysis to monitor stationarity and between/within chains comparisons to monitor mixing.
    * What type of analysis?
    * What do they mean by mixing?? You can't just sum everything and then compute probabilities... otherwise you might double or triple the probability of a mode that is more often discovered than another.
    * Be aware that chain mixing does not necessarily mean convergence is reached.
* Once you have reached approximate convergence, mix all the simulations from the second halves of the chains together to summarize the target distribution. For most purposes there is no longer any need to worry about autocorrelations in the chains.
* Adaptive MCMC

Toolbox available online: [for documentation on the convergence diagnostics implemented](https://research.cs.aalto.fi/pml/software/mcmcdiag/)
Also available as an external toolbox in [TAPS](https://github.com/translationalneuromodeling/tapas/tree/master/mpdcm/external/mcmcdiag)
