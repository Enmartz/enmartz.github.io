---
layout: page
title: Generative Spectral Imaging
description: Learning compact representations for spectral image generation and RGB-guided synthesis.
importance: 3
category: research
related_publications: true
---

Spectral datasets are expensive to acquire and often much smaller than conventional image collections. This research line studies generative models that learn useful spectral distributions from compact representations or readily available RGB imagery.

**LD-GAN** trains a generative adversarial network in the regularized latent space of a spectral autoencoder. The generated latent samples are mapped back into the spectral domain and used as data augmentation for reconstruction, super-resolution, and RGB-to-spectral tasks.

The **RGB-guided spectral generation** work extends this direction by learning spectral structure with guidance from RGB datasets, reducing dependence on large paired spectral collections and complex optical acquisition setups.

### publications

{% cite martinez2023ldgan %}

{% cite martinez2024rgbguided %}
