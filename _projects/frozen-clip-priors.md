---
layout: page
title: Frozen CLIP Priors for Robust Self-Supervised Poisson Inverse Problems
description: Foundation-driven priors for photon-limited inverse imaging without clean ground truth.
img: assets/img/frozen-clip-priors/method.webp
importance: 1
category: research
related_publications: false
permalink: /projects/frozen-clip-priors/
---

<link rel="stylesheet" href="{{ '/assets/css/frozen-clip-priors.css' | relative_url }}">

<div class="fcp-page">

<div class="fcp-authors">
  <a href="https://orcid.org/0009-0003-9917-9505">Laura C. Diaz-Delgado</a> ·
  <a href="https://orcid.org/0000-0002-6458-4258">Emmanuel Martinez</a> ·
  <a href="https://orcid.org/0000-0002-2202-253X">Henry Arguello</a>
</div>
<div class="fcp-affiliation">Department of Computer Science · Universidad Industrial de Santander · Colombia</div>

<p class="fcp-lede">
A lightweight unrolled solver that turns frozen CLIP representations into robust image priors for Poisson demosaicing and deblurring, while learning directly from corrupted measurements.
</p>

<div class="fcp-actions">
  <a class="fcp-button primary" href="#method">Method</a>
  <a class="fcp-button" href="#results">Results</a>
  <a class="fcp-button" href="#real-data">Real data</a>
  <a class="fcp-button" href="#citation">BibTeX</a>
  <span class="fcp-button disabled" title="Public repository link will be enabled when available">Code · coming soon</span>
</div>

<nav class="fcp-anchor-nav" aria-label="Project sections">
  <a href="#overview">Overview</a>
  <a href="#method">Method</a>
  <a href="#results">Results</a>
  <a href="#efficiency">Efficiency</a>
  <a href="#real-data">Real data</a>
  <a href="#citation">Citation</a>
</nav>

<figure class="fcp-figure fcp-wide">
  <div style="display:flex;gap:0;overflow:hidden;border-radius:14px;background:#fff">
    <img src="{{ '/assets/img/frozen-clip-priors/demosaicing-1.webp' | relative_url }}" alt="Left half of the paper's Poisson demosaicing comparison on BSDS500." loading="eager" style="width:50%;border:0;border-radius:0">
    <img src="{{ '/assets/img/frozen-clip-priors/demosaicing-2.webp' | relative_url }}" alt="Right half of the paper's Poisson demosaicing comparison on BSDS500." loading="eager" style="width:50%;border:0;border-radius:0">
  </div>
  <figcaption>Qualitative Poisson demosaicing comparison from the paper, showing the noisy measurement, baselines, Ours (Self), Ours (Sup), and the reference.</figcaption>
</figure>

<section id="overview" class="fcp-section">
<h2>Why frozen foundation priors?</h2>
<p>
Photon-limited inverse problems are difficult for two coupled reasons: the forward operator destroys information and Poisson noise is signal dependent. Standard learned priors can also become brittle under acquisition or dataset shifts. This work separates those concerns: physics is handled explicitly by data consistency, while image structure is represented by frozen CLIP RN50 features and a compact trainable decoder.
</p>

<div class="fcp-grid-3">
  <div class="fcp-card">
    <h3>Frozen CLIP prior</h3>
    <p>Dense multi-scale RN50 features remain fixed. Only a lightweight decoder is optimized, preserving transferable representations instead of relearning the encoder from limited inverse-problem data.</p>
  </div>
  <div class="fcp-card">
    <h3>Physics-aware unrolling</h3>
    <p>An ADMM-inspired network alternates a closed-form data-consistency step with the learned prior, so CFA sampling or blur remains explicit in every reconstruction iteration.</p>
  </div>
  <div class="fcp-card">
    <h3>Self-supervision</h3>
    <p>GR2R measurement-domain re-corruption is coupled with Equivariant Imaging through virtual acquisitions, providing a training signal without clean ground truth.</p>
  </div>
</div>
</section>

<section id="method" class="fcp-section">
<h2>Method</h2>
<p>
The solver unrolls a small number of ADMM iterations. At iteration <em>t</em>, the data-consistency variable is updated using the known image-formation model; the prior variable is then produced by a decoder operating on frozen CLIP features; finally, the dual variable enforces agreement between both estimates. Decoder weights are shared across iterations.
</p>

<figure class="fcp-figure fcp-wide">
  <img src="{{ '/assets/img/frozen-clip-priors/method.webp' | relative_url }}" alt="Architecture of the proposed ADMM-inspired unrolled reconstruction method with frozen CLIP encoder and trainable decoder." loading="lazy">
  <figcaption>Proposed reconstruction architecture from the paper. A closed-form data-consistency update is alternated with a CLIP-based prior update across the unrolled iterations.</figcaption>
</figure>

<div class="fcp-equation">
\[
\mathbf{x}^{t+1} \;\longrightarrow\; \mathbf{z}^{t+1}=\mathcal{G}_{\theta}(\mathcal{E}_{\mathrm{CLIP}}(\mathbf{x}^{t+1}+\mathbf{u}^{t})) \;\longrightarrow\; \mathbf{u}^{t+1}.
\]
</div>

<div class="fcp-note">
<strong>Key design constraint.</strong> The CLIP encoder is frozen. The method therefore uses foundation representations as a prior rather than fine-tuning the full foundation model for each inverse problem.
</div>
</section>

<section id="results" class="fcp-section">
<h2>Poisson inverse problems</h2>
<p>
The method is evaluated on CFA demosaicing and deblurring over BSDS500 and DIV2K, including a dataset shift and two photon regimes. The self-supervised variant remains close to supervised training and becomes particularly competitive under severe Poisson noise.
</p>

<div class="fcp-metrics">
  <div class="fcp-metric"><span class="value">26.98 dB</span><span class="label">Demosaicing · BSDS500 · γ = 0.05 · Ours (Self)</span></div>
  <div class="fcp-metric"><span class="value">0.7579</span><span class="label">SSIM in the same severe demosaicing setting</span></div>
  <div class="fcp-metric"><span class="value">27.45 dB</span><span class="label">Deblurring · BSDS500 · γ = 0.05 · Ours (Self)</span></div>
  <div class="fcp-metric"><span class="value">0.7532</span><span class="label">SSIM in the same severe deblurring setting</span></div>
</div>

<div style="height:1.8rem"></div>
<div class="fcp-result-head"><h3>Poisson demosaicing</h3><span>BSDS500 · γ = 0.01 qualitative comparison</span></div>
<figure class="fcp-figure fcp-wide">
  <div style="display:flex;gap:0;overflow:hidden;border-radius:14px;background:#fff">
    <img src="{{ '/assets/img/frozen-clip-priors/demosaicing-1.webp' | relative_url }}" alt="Left half of the paper's Poisson demosaicing comparison on BSDS500." loading="lazy" style="width:50%;border:0;border-radius:0">
    <img src="{{ '/assets/img/frozen-clip-priors/demosaicing-2.webp' | relative_url }}" alt="Right half of the paper's Poisson demosaicing comparison on BSDS500." loading="lazy" style="width:50%;border:0;border-radius:0">
  </div>
  <figcaption>Paper figure for Poisson demosaicing on BSDS500 at γ = 0.01. Columns show the measurement, baselines, Ours (Self), Ours (Sup), and the reference, with per-image PSNR/SSIM.</figcaption>
</figure>

<div class="fcp-table-wrap">
<table class="fcp-table">
  <thead><tr><th>Severe demosaicing · BSDS500</th><th>PSNR [dB]</th><th>SSIM</th></tr></thead>
  <tbody>
    <tr><td>GSPnP</td><td>26.50</td><td>0.6945</td></tr>
    <tr><td>RAM</td><td>26.17</td><td>0.7178</td></tr>
    <tr class="ours"><td>Ours (Self)</td><td>26.98</td><td>0.7579</td></tr>
    <tr class="ours"><td>Ours (Sup)</td><td>27.04</td><td>0.7522</td></tr>
  </tbody>
</table>
</div>

<div style="height:1.6rem"></div>
<div class="fcp-result-head"><h3>Poisson deblurring</h3><span>BSDS500 · γ = 0.01 qualitative comparison</span></div>
<figure class="fcp-figure fcp-wide">
  <div style="display:flex;gap:0;overflow:hidden;border-radius:14px;background:#fff">
    <img src="{{ '/assets/img/frozen-clip-priors/deblurring-1.webp' | relative_url }}" alt="Left half of the paper's Poisson deblurring comparison on BSDS500." loading="lazy" style="width:50%;border:0;border-radius:0">
    <img src="{{ '/assets/img/frozen-clip-priors/deblurring-2.webp' | relative_url }}" alt="Right half of the paper's Poisson deblurring comparison on BSDS500." loading="lazy" style="width:50%;border:0;border-radius:0">
  </div>
  <figcaption>Paper figure for Poisson deblurring on BSDS500 at γ = 0.01, comparing the measurement, baselines, Ours (Self), Ours (Sup), and the reference.</figcaption>
</figure>

<div class="fcp-table-wrap">
<table class="fcp-table">
  <thead><tr><th>Severe deblurring · BSDS500</th><th>PSNR [dB]</th><th>SSIM</th></tr></thead>
  <tbody>
    <tr><td>DPIR</td><td>26.72</td><td>0.7113</td></tr>
    <tr><td>GSPnP</td><td>27.03</td><td>0.7227</td></tr>
    <tr class="ours"><td>Ours (Self)</td><td>27.45</td><td>0.7532</td></tr>
    <tr class="ours"><td>Ours (Sup)</td><td>27.58</td><td>0.7613</td></tr>
  </tbody>
</table>
</div>
</section>

<section id="efficiency" class="fcp-section">
<h2>Efficiency</h2>
<p>
Keeping the foundation encoder frozen and sharing the compact prior across unrolled iterations yields a markedly lighter reconstruction pipeline. Runtime was measured on an NVIDIA RTX 4070 for a 3 × 256 × 256 input.
</p>

<div class="fcp-metrics">
  <div class="fcp-metric"><span class="value">0.09</span><span class="label">TFLOPs · Ours</span></div>
  <div class="fcp-metric"><span class="value">0.0242 s</span><span class="label">Inference time · Ours</span></div>
  <div class="fcp-metric"><span class="value">≈102×</span><span class="label">Faster than Transfer CLIP in this benchmark</span></div>
  <div class="fcp-metric"><span class="value">10.99 M</span><span class="label">Trainable parameters</span></div>
</div>

<div class="fcp-table-wrap">
<table class="fcp-table">
  <thead><tr><th>Method</th><th>Params [M]</th><th>TFLOPs</th><th>Time [s]</th></tr></thead>
  <tbody>
    <tr><td>DPIR</td><td>32.64</td><td>11.49</td><td>0.5193</td></tr>
    <tr><td>Transfer CLIP</td><td>10.99</td><td>9.00</td><td>2.4683</td></tr>
    <tr><td>GSPnP</td><td>17.01</td><td>9.12</td><td>0.9247</td></tr>
    <tr><td>RAM</td><td>34.13</td><td>0.32</td><td>0.8026</td></tr>
    <tr class="ours"><td>Ours</td><td>10.99</td><td>0.09</td><td>0.0242</td></tr>
  </tbody>
</table>
</div>
</section>

<section id="real-data" class="fcp-section">
<h2>Real photon-limited data</h2>
<p>
Beyond synthetic Poisson simulations, the framework is tested on a real low-light image from the SID dataset using zero-shot self-supervised adaptation. One 512 × 512 patch is held out for testing and no clean target is used to optimize the self-supervised model.
</p>

<figure class="fcp-figure fcp-wide">
  <img src="{{ '/assets/img/frozen-clip-priors/sid.webp' | relative_url }}" alt="Real photon-limited SID experiment from the paper, comparing raw mosaic input, Ours Self, Ours Sup, and the reference." loading="lazy">
  <figcaption>Real SID data: the self-supervised reconstruction improves from 14.95 dB / 0.1731 at the raw input to 26.37 dB / 0.6482 without clean-target supervision.</figcaption>
</figure>
</section>

<section id="ablation" class="fcp-section">
<h2>What drives the gain?</h2>
<div class="fcp-grid-2">
  <div class="fcp-card">
    <h3>Pretraining matters</h3>
    <p>An untrained CLIP backbone reaches only 21.91 dB / 0.7064 under supervised training in the reported ablation. Frozen pretrained representations provide a substantially stronger prior.</p>
  </div>
  <div class="fcp-card">
    <h3>Self-supervision closes the gap</h3>
    <p>With the proposed loss, Ours (Self) reaches 30.53 dB / 0.8609 versus 30.75 dB / 0.8703 for Ours (Sup) on Poisson demosaicing at γ = 0.01.</p>
  </div>
</div>
</section>

<section id="citation" class="fcp-section">
<h2>Citation</h2>
<p>The manuscript is currently represented here as a project/preprint citation; replace this entry with the final venue or arXiv metadata once available.</p>

<div class="fcp-code"><pre><code>@misc{diazdelgado2026frozenclip,
  title  = {Frozen CLIP Priors for Robust Self-Supervised Poisson Inverse Problems},
  author = {Diaz-Delgado, Laura C. and Martinez, Emmanuel and Arguello, Henry},
  year   = {2026},
  note   = {Manuscript}
}</code></pre></div>
</section>

<section class="fcp-section">
<h2>Acknowledgements</h2>
<p>
The authors acknowledge the VIE of Universidad Industrial de Santander for support through “Apoyo a Semilleros de Investigación – Diseño de Codificación para el Muestreo Compresivo de Señales Multidimensionales Utilizando Técnicas Basadas en Aprendizaje Profundo”, Project 4765.
</p>
</section>

</div>
