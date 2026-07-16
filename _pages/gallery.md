---
layout: page
permalink: /gallery/
title: Gallery
nav: true
nav_order: 9
---

<style>
  .gallery-grid { display: grid; gap: 24px; margin-top: 1rem; }
  .gallery-item { border: 1px solid var(--global-divider-color); border-radius: 8px; padding: 16px; box-shadow: 0 2px 8px rgba(0,0,0,0.05); background: var(--global-card-bg-color); }
  .gallery-item h3 { margin-top: 0; margin-bottom: 12px; }
  .gallery-item img { width: 100%; height: auto; border-radius: 8px; display: block; background: #fff; }
</style>

<div class="gallery-grid">
  <div class="gallery-item">
    <h3>Graduation Photo</h3>
    <div>
      <img src="{{ '/assets/team/Graduation.jpg' | relative_url }}" alt="Graduation Photo" loading="lazy">
    </div>
  </div>

  <div class="gallery-item">
    <h3>CVPR2026</h3>
    <div>
      <img src="{{ '/assets/team/wangxinshun_cvpr.jpg' | relative_url }}" alt="CVPR2026 photo" loading="lazy">
    </div>
  </div>

  <div class="gallery-item">
    <h3>ICRA2026</h3>
    <div>
      <img src="{{ '/assets/team/zhangyutian_icra.jpg' | relative_url }}" alt="ICRA2026 photo" loading="lazy">
    </div>
  </div>

  <div class="gallery-item">
    <h3>NeurIPS2023</h3>
    <div>
      <img src="{{ '/assets/team/fangzhongbin_neurips23.jpg' | relative_url }}" alt="NeurIPS2023 photo" loading="lazy">
    </div>
  </div>
</div>
