+++
title = "Predicting CSD"
subtitle = ""

# Math mode needs to be cool
markup = "mmark"

# Add a summary to display on homepage (optional).
summary = ""

date = 2019-08-03T19:31:11+02:00
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

## What are CSD??

The cross power spectral density (or cross spectral density) $S_{xy}(\omega)$
between two signals $x(t)$ and $y(t)$ can be defined as the Fourier transform of
these series' cross-correlation function $R\_{xy}(\\tau)$:

$$S_{xy}(\omega)=\int_{-\infty}^{\infty}R_{xy}(\tau)e^{-j \omega\tau}d\tau
= \int_{-\infty}^{\infty} \left[ \int_{-\infty}^{\infty} x(t)^* \cdot y(t+\tau) dt \right] e^{-j \omega t} d\tau$$

When $x(t)=y(t)$, we talk of power spectral densities.

## What's a Volterra series?
A Volterra series is similar to a Taylor series. They differ in that the Taylor series
can model non-linear systems with no memory, whereas the Volterra series can
capture this memory effect.

A continuous time-invariant system with $x(t)$ as input and $y(t)$ as output can be expanded in Volterra series as:

 $$y(t) = h_{0}+\sum_{n=1}^{N}{\int_{a}^{b}\cdots\int_{a}^{b} {h_{n}(\tau_{1},.\,.\,,\tau_{n})\prod^{n}_{j=1}{x(t - \tau_{j}) d\tau_{j}}}}$$

 Looks complicated, but you understand what is going on if you start the expansion yourself:

 $$y(t) = h_{0}+{\int_{a}^{b}{h_{1}(\tau_{1})\cdot{x(t - \tau_{1}) d\tau_{1}}}} + {\int_{a}^{b} \int_{a}^{b} {h_{2}(\tau_{1}, \tau_{2})\cdot{x(t - \tau_{1})\cdot x(t - \tau_{2}) d\tau_{1}d\tau_{2}}}} ...$$

 The function $$h_{n}(\tau_{1},.\,.\,,\tau_{n})$$ is called the $n$-th order Volterra kernel,
 It can be regarded as a higher-order impulse response of the system.

 Issues:
 - By looking at the Volterra series, you don't know the order of your system
 - Individual Volterra operators (H, different from kernels h!) are not independent
