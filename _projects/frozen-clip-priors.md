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
<div class="fcp-authors"><a href="https://orcid.org/0009-0003-9917-9505">Laura C. Diaz-Delgado</a> · <a href="https://orcid.org/0000-0002-6458-4258">Emmanuel Martinez</a> · <a href="https://orcid.org/0000-0002-2202-253X">Henry Arguello</a></div>
<div class="fcp-affiliation">Department of Computer Science · Universidad Industrial de Santander · Colombia</div>
<p class="fcp-lede">A lightweight unrolled solver that turns frozen CLIP representations into robust image priors for Poisson demosaicing and deblurring, while learning directly from corrupted measurements.</p>
<div class="fcp-actions"><a class="fcp-button primary" href="#method">Method</a><a class="fcp-button" href="#results">Results</a><a class="fcp-button" href="#real-data">Real data</a><a class="fcp-button" href="#citation">BibTeX</a><span class="fcp-button disabled">Code · coming soon</span></div>
<nav class="fcp-anchor-nav" aria-label="Project sections"><a href="#overview">Overview</a><a href="#method">Method</a><a href="#results">Results</a><a href="#efficiency">Efficiency</a><a href="#real-data">Real data</a><a href="#citation">Citation</a></nav>

<figure class="fcp-figure"><img src="{{ '/assets/img/frozen-clip-priors/demosaicing-hi.webp' | relative_url }}" alt="Original Poisson demosaicing comparison from the paper on BSDS500." width="5100" height="1970" loading="eager" fetchpriority="high" decoding="async"><figcaption>Qualitative Poisson demosaicing comparison from the paper.</figcaption></figure>

<section id="overview" class="fcp-section"><h2>Why frozen foundation priors?</h2><p>Photon-limited inverse problems combine an information-losing forward operator with signal-dependent Poisson noise. This work keeps physics explicit through data consistency while using frozen CLIP RN50 features and a compact trainable decoder as an image prior.</p><div class="fcp-grid-3"><div class="fcp-card"><h3>Frozen CLIP prior</h3><p>Dense multi-scale RN50 features remain fixed; only the decoder is optimized.</p></div><div class="fcp-card"><h3>Physics-aware unrolling</h3><p>An ADMM-inspired network alternates data consistency with the learned prior.</p></div><div class="fcp-card"><h3>Self-supervision</h3><p>GR2R re-corruption is coupled with Equivariant Imaging without clean ground truth.</p></div></div></section>

<section id="method" class="fcp-section"><h2>Method</h2><p>The solver unrolls ADMM iterations while sharing decoder weights across iterations.</p><figure class="fcp-figure"><img src="{{ '/assets/img/frozen-clip-priors/method.webp' | relative_url }}" alt="Original method figure from the paper." width="5100" height="1768" loading="lazy" decoding="async"><figcaption>Original reconstruction architecture from the paper.</figcaption></figure><div class="fcp-equation">\[\mathbf{x}^{t+1} \;\longrightarrow\; \mathbf{z}^{t+1}=\mathcal{G}_{\theta}(\mathcal{E}_{\mathrm{CLIP}}(\mathbf{x}^{t+1}+\mathbf{u}^{t})) \;\longrightarrow\; \mathbf{u}^{t+1}.\]</div></section>

<section id="results" class="fcp-section"><h2>Poisson inverse problems</h2><div class="fcp-metrics"><div class="fcp-metric"><span class="value">26.98 dB</span><span class="label">Demosaicing · BSDS500 · γ = 0.05 · Ours (Self)</span></div><div class="fcp-metric"><span class="value">0.7579</span><span class="label">SSIM</span></div><div class="fcp-metric"><span class="value">27.45 dB</span><span class="label">Deblurring · BSDS500 · γ = 0.05 · Ours (Self)</span></div><div class="fcp-metric"><span class="value">0.7532</span><span class="label">SSIM</span></div></div><div style="height:1.8rem"></div><div class="fcp-result-head"><h3>Poisson demosaicing</h3><span>BSDS500 · γ = 0.01 qualitative comparison</span></div><figure class="fcp-figure"><img src="{{ '/assets/img/frozen-clip-priors/demosaicing-hi.webp' | relative_url }}" alt="Original demosaicing figure from the paper." width="5100" height="1970" loading="lazy" decoding="async"><figcaption>Original paper figure for Poisson demosaicing at γ = 0.01.</figcaption></figure><div class="fcp-table-wrap"><table class="fcp-table"><thead><tr><th>Severe demosaicing · BSDS500</th><th>PSNR [dB]</th><th>SSIM</th></tr></thead><tbody><tr><td>GSPnP</td><td>26.50</td><td>0.6945</td></tr><tr><td>RAM</td><td>26.17</td><td>0.7178</td></tr><tr class="ours"><td>Ours (Self)</td><td>26.98</td><td>0.7579</td></tr><tr class="ours"><td>Ours (Sup)</td><td>27.04</td><td>0.7522</td></tr></tbody></table></div><div style="height:1.6rem"></div><div class="fcp-result-head"><h3>Poisson deblurring</h3><span>BSDS500 · γ = 0.01 qualitative comparison</span></div><figure class="fcp-figure"><img src="{{ '/assets/img/frozen-clip-priors/deblurring-hi.webp' | relative_url }}" alt="Original deblurring figure from the paper." width="5100" height="1970" loading="lazy" decoding="async"><figcaption>Original paper figure for Poisson deblurring at γ = 0.01.</figcaption></figure><div class="fcp-table-wrap"><table class="fcp-table"><thead><tr><th>Severe deblurring · BSDS500</th><th>PSNR [dB]</th><th>SSIM</th></tr></thead><tbody><tr><td>DPIR</td><td>26.72</td><td>0.7113</td></tr><tr><td>GSPnP</td><td>27.03</td><td>0.7227</td></tr><tr class="ours"><td>Ours (Self)</td><td>27.45</td><td>0.7532</td></tr><tr class="ours"><td>Ours (Sup)</td><td>27.58</td><td>0.7613</td></tr></tbody></table></div></section>

<section id="efficiency" class="fcp-section"><h2>Efficiency</h2><div class="fcp-metrics"><div class="fcp-metric"><span class="value">0.09</span><span class="label">TFLOPs · Ours</span></div><div class="fcp-metric"><span class="value">0.0242 s</span><span class="label">Inference time · Ours</span></div><div class="fcp-metric"><span class="value">≈102×</span><span class="label">Faster than Transfer CLIP</span></div><div class="fcp-metric"><span class="value">10.99 M</span><span class="label">Trainable parameters</span></div></div></section>

<section id="real-data" class="fcp-section"><h2>Real photon-limited data</h2><figure class="fcp-figure"><img src="{{ '/assets/img/frozen-clip-priors/sid.webp' | relative_url }}" alt="Original SID experiment figure from the paper." width="5100" height="1280" loading="lazy" decoding="async"><figcaption>Original SID experiment from the paper: 14.95 dB / 0.1731 input → 26.37 dB / 0.6482 Ours (Self).</figcaption></figure></section>

<section id="ablation" class="fcp-section"><h2>What drives the gain?</h2><div class="fcp-grid-2"><div class="fcp-card"><h3>Pretraining matters</h3><p>An untrained CLIP backbone reaches 21.91 dB / 0.7064 in the reported ablation.</p></div><div class="fcp-card"><h3>Self-supervision closes the gap</h3><p>Ours (Self) reaches 30.53 dB / 0.8609 versus 30.75 dB / 0.8703 for Ours (Sup) at γ = 0.01.</p></div></div></section>

<section id="citation" class="fcp-section"><h2>Citation</h2><div class="fcp-code"><pre><code>@misc{diazdelgado2026frozenclip,
  title  = {Frozen CLIP Priors for Robust Self-Supervised Poisson Inverse Problems},
  author = {Diaz-Delgado, Laura C. and Martinez, Emmanuel and Arguello, Henry},
  year   = {2026},
  note   = {Manuscript}
}</code></pre></div></section>
</div>
