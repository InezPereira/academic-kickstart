+++
title = "Adaboost"
subtitle = ""

# Add a summary to display on homepage (optional).
summary = "Mostly based on MIT OpenCourseware material!"

date = 2019-07-17T10:40:22+02:00
draft = true

# Authors. Comma separated list, e.g. `["Bob Smith", "David Jones"]`.
authors = ["Inês Pereira"]

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

## Adaboost: algorithm steps

Define it better. Say that's is really good in terms of overfitting!

A few key ideas:

- You combine weak learners to make an ensemble classifier which performs well
- Some learners have more say in classification than others
- Each new best weak learner takes the errors from the previous classifiers into account.

The idea here is to make a classifier $H(x)$ made of weak classifiers $h_i(x)$
using the following rule:

$H(x)=\sum_i \alpha_i \cdot h_i(x)$, where $\alpha_i$ is the so-called voting
power for classifier $i$.

Imagine you have a dataset with $N$ observations and start of with a set of classifiers.

How do you define these classifiers?? One way to is look at how many features you have.
Then figure out if they are categorical or numerical.
For categorical, it's easy: just yes or no. For numerical, you'll have to test different
boundaries.

In each round, you basically:

- pick the "best" weak classifier
- assign it some voting power $\alpha$
- append $\alpha_i h_i(x)$ to $H(x)$

1. Initialize weights: $w_i = \frac{1}{N}$
You usually assign each training point equal weight.

### The nitty gritty details:

2. Calculate error rate for each $h_i$:

$$\epsilon = \sum_{wrong}w_i$$

So you sum the weights of the misclassified points for each classifier.

3. Pick the best weak classifier $h$. This is will be equal to $\max|1-epsilon|$.
This means you avoid classifier which are as bad a random flip of a coin, and also
take into account information from classifier which sistematically get things wrong.
Basically, if a classifier is nearly always wrong and it says "1", then you just assume
the right answer is "0".

4. Calculate voting power for $h$ (the best weak classifier):
$\alpha = \frac{1}{2}\ln(\frac{1-\epsilon}{\epsilon})$

5. Check if we are finished! When are we finished?
  - $H(x)$ is good enough
  - We have reached a maximum number of rounds
  - There is no good classifier left: best $h$ has $\epsilon=\frac{1}{2}$.

6. If we are finished, well, finish it.
If not: update the weights to emphasize the points which were misclassified.

$$w_{new}= \frac{1}{2}\cdot \frac{1}{1-\epsilon} \cdot w_i$$

if point was correctly classified.

$$w_{new}= \frac{1}{2}\cdot \frac{1}{\epsilon} \cdot w_i$$

if a point was wrongly classified.

Then go back to step 2!!

Notice that when your best classifier has an error rate $\epsilon=\frac{1}{2}$,
you get back the old weights! That's why you stop there 😉.



📚 Thank you [MIT OpenCourseware](https://www.youtube.com/watch?v=UHBmv7qCey4)
and [Jessica Noss](https://www.youtube.com/watch?v=lHemIUX2tmM&list=PLxymR0ZPfMmV-vGtvhvTeWHIcnh-bTjDI)
for posting this material for others to watch for free!
A huge thanks to [Josh Starmer](https://www.youtube.com/watch?v=LsK-xG1cLYA) for
his awesome videos on Stats and wonderful mathy sense of humor!
