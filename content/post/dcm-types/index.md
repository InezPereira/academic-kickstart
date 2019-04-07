+++
title = "DCM for EEG"
subtitle = "A brief summary of the available models"

# Add a summary to display on homepage (optional).
summary = ""

date = 2019-04-01T12:57:43+02:00
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
The literature surrounding Dynamic Causal Modelling (DCM) can quickly get quite
confusing, and one the of the things that is hard to find is a list of all the
current options one has, when one decides to model EEG or fMRI data with DCM.
Below you'll find a small list of the available DCM models with a brief description
about what distinguished them from other models. I'll also provide references to
papers you might want to check out if you wish to understand the inner workings
of these models.
Oh, and I'll also write down the model acronyms in case you are using SPM, on the
menu in the right-hand side, when opening the SPM GUI for DCM for EEG

<img src="spm_menu.png" style="float: left; margin-right: 10px;"/>

- Neural mass models ('NMM'): nonlinear model based on a first order approximation
('first order' refering to first order statistics).
  - ’NMDA’ is a variant of the ’NMM’ model which also includes a model of NMDA receptor.
  - ’CMC’ and ’CMM’ are canonical microcircuit models. You'll find, in SPM a 'CMC NMDA',
  basically incorporates a canonical microcircuit model with dedicated parameters
  for the NMDA receptor.
The neural mass models used in DCM capture this 6-layer anatomical cortical
 structure by specifying (currently three or four) subpopulations of cell types,
 occupying the granular, supragranular, and infragranular layers.
- Neural field models
- Mean field models (’MFM’): also nonlinear and based on second order approximation.

In the documentation, you'll find:

```
% Type of model (neuronal)
%--------------------------------------------------------------------------
% 'ERP'     - (linear second order NMM slow)
% 'SEP'     - (linear second order NMM fast)
% 'CMC'     - (linear second order NMM Canonical microcircuit)
% 'LFP'     - (linear second order NMM self-inhibition)
% 'NMM'     - (nonlinear second order NMM first-order moments)
% 'MFM'     - (nonlinear second order NMM second-order moments)
% 'CMM'     - (nonlinear second order NMM Canonical microcircuit)
% 'DEM'     - (functional architecture based on a DEM scheme)
% 'NMDA'    - (nonlinear second order NMM first-order moments with NMDA receptors)
% 'CMM_NMDA'- (nonlinear first order Canonical microcircuit with NMDA receptors)
```

"Two broad classes of models have been used in DCM for electrophysiological data, namely, synaptic kernel convolution models (Marten et al., 2009; Valdes-Sosa et al., 2009; Wendling et al., 2000; Jansen and Rit, 1995; Lopes da Silva et al., 1976) and conductance- based models (Marreiros et al., 2009, 2010; Breakspear et al., 2003; Brunel and Wang, 2001). For both model classes, the activity of large neuronal populations is approximated by a probability density (see Deco et al., 2008 for review). In our previous exposition ofDCM for SSR, we used a point mass or density to describe interactions of excitatory and inhibitory interneurons and pyramidal cell populations within a cortical source, a so-called neural-mass model (Deco et al., 2008; Moran et al., 2007, 2008). This model was of the kernel type, where postsynaptic responses result from the convolution of presynaptic input with a postsynaptic kernel. While this type of model offers a parsimonious description of population activity, conductance-based models are more directly related to specific synaptic processes. This is because they model different types of ionic currents explicitly, such as passive leak currents and active voltage and ligand-gated currents."
Consistent spectral predictors for dynamic causal models of steady-state responses, Moran, KES

conductance-based: Marreiros et al. (2009) first described a conductance-based model predicated on the Morris–Lecar (ML) model (Morris and Lecar, 1981).
The ML model was extended to include three cell populations that are interconnected by means of fast glutamatergic and GABAergic synapses, forming a plausible cortical source.
