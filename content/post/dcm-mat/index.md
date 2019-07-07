+++
title = "DCM struct cheat sheet"
subtitle = ""

# Add a summary to display on homepage (optional).
summary = ""

date = 2019-04-02T06:34:20+02:00
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
## DCM for fMRI

What is inside the DCM.mat struct for fMRI?
This is what you get if you type `help spm_dcm_estimate`

```
Expects
 --------------------------------------------------------------------------
  DCM.a                              % switch on endogenous connections
  DCM.b                              % switch on bilinear modulations
  DCM.c                              % switch on exogenous connections
  DCM.d                              % switch on nonlinear modulations
  DCM.U                              % exogenous inputs
  DCM.Y.y                            % responses
  DCM.Y.X0                           % confounds
  DCM.Y.Q                            % array of precision components
  DCM.n                              % number of regions
  DCM.v                              % number of scans

Options
--------------------------------------------------------------------------
 DCM.options.two_state              % two regional populations (E and I)
 DCM.options.stochastic             % fluctuations on hidden states
 DCM.options.centre                 % mean-centre inputs
 DCM.options.nonlinear              % interactions among hidden states
 DCM.options.nograph                % graphical display
 DCM.options.induced                % switch for CSD data features
 DCM.options.P                      % starting estimates for parameters
 DCM.options.hidden                 % indices of hidden regions
 DCM.options.maxnodes               % maximum number of (effective) nodes
 DCM.options.maxit                  % maximum number of iterations
 DCM.options.hE                     % expected precision of the noise
 DCM.options.hC                     % variance of noise expectation

 Evaluates:
--------------------------------------------------------------------------
 DCM.M                              % Model structure
 DCM.Ep                             % Condition means (parameter structure)
 DCM.Cp                             % Conditional covariances
 DCM.Vp                             % Conditional variances
 DCM.Pp                             % Conditional probabilities
 DCM.H1                             % 1st order hemodynamic kernels
 DCM.H2                             % 2nd order hemodynamic kernels
 DCM.K1                             % 1st order neuronal kernels
 DCM.K2                             % 2nd order neuronal kernels
 DCM.R                              % residuals
 DCM.y                              % predicted data
 DCM.T                              % Threshold for Posterior inference
 DCM.Ce                             % Error variance for each region
 DCM.F                              % Free-energy bound on log evidence
 DCM.ID                             % Data ID
 DCM.AIC                            % Akaike Information criterion
 DCM.BIC                            % Bayesian Information criterion

```
