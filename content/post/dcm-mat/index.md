+++
title = "Analyzing the DCM.mat object"
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
This is what you get if you type `help spm_dcm_estimate(`

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

## DCM for energy
```
% DCM
%    name: name string
%       xY: data   [1x1 struct]
%       xU: design [1x1 struct]
%
%   Sname: cell of source name strings
%       A: {[nr x nr double]  [nr x nr double]  [nr x nr double]}
%       B: {[nr x nr double], ...}   Connection constraints
%       C: [nr x 1 double]
%
%   options.Nmodes       - number of spatial modes
%   options.Tdcm         - [start end] time window in ms
%   options.Fdcm         - [start end] Frequency window in Hz
%   options.D            - time bin decimation       (usually 1 or 2)
%   options.spatial      - 'ECD', 'LFP' or 'IMG'     (see spm_erp_L)
%   options.model        - 'ERP', 'SEP', 'CMC', 'LFP', 'NMM' or 'MFM'
%
% Estimates:
%--------------------------------------------------------------------------
% DCM.dtf                   - directed transfer functions (source space)
% DCM.ccf                   - cross covariance functions (source space)
% DCM.coh                   - cross coherence functions (source space)
% DCM.fsd                   - specific delay functions (source space)
% DCM.pst                   - peristimulus time
% DCM.Hz                    - frequency
%
% DCM.Ep                    - conditional expectation
% DCM.Cp                    - conditional covariance
% DCM.Pp                    - conditional probability
% DCM.Hc                    - conditional responses (y), channel space
% DCM.Rc                    - conditional residuals (y), channel space
% DCM.Hs                    - conditional responses (y), source space
% DCM.Ce                    - eML error covariance
% DCM.F                     - Laplace log evidence
% DCM.ID                    -  data ID
```
