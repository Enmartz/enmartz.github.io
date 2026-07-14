---
layout: page
title: DiffCS
description: Conditional diffusion reconstruction with measurement augmentation for compressive imaging.
importance: 2
category: research
related_publications: true
---

Compressive imaging reconstructs a signal from incomplete observations, producing an ill-posed inverse problem whose difficulty depends strongly on the available measurements.

**DiffCS** studies a conditional diffusion model augmented with synthetic measurements. A neural network estimates additional observations from the acquired data; real and synthetic measurements are then combined to strengthen the conditioning of the diffusion reconstruction process.

Computational experiments show that measurement augmentation improves reconstruction over conditioning the model with real measurements alone.

[Paper](https://doi.org/10.1109/ICASSP49660.2025.10889114) · [Explore the code](https://github.com/Enmartz/diffcs)

### related publications

{% cite martinez2025diffcs %}

{% cite gualdron2025measurement %}
