---
layout: page
title: Deep Spectral Band Selection
description: Learning task-relevant wavelengths for hyperspectral classification and material segmentation.
img: assets/img/dsbs.png
importance: 1
category: research
related_publications: true
---

**Deep Spectral Band Selection (DSBS)** connects the optical acquisition model with a downstream neural network in a single end-to-end optimization. A differentiable binary selector learns which spectral bands are most informative for the target task.

{% include figure.liquid loading="eager" path="assets/img/dsbs.png" title="Overview of the DSBS framework" class="img-fluid rounded z-depth-1" %}

The method was evaluated on hyperspectral classification, material segmentation, and a physical cocoa-bean classification testbed. Starting with 301 spectral measurements, the learned system converges to a compact set of 10 wavelengths while retaining competitive task performance and substantially reducing acquisition requirements.

[Paper](https://doi.org/10.1364/AO.586969) · [Code](https://github.com/Enmartz/DSBS)

### publication

{% cite martinez2026dsbs %}
