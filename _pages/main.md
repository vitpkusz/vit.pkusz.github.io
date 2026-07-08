---
layout: page
permalink: /
title: Lab
description:

carousel_autoplay_delay: 3500

highlighted_projects:
  - teaser_img: /assets/teaser/wangziyi_unimotion.png
    caption:
    title: "UniMotion: A Unified Framework for Motion-Text-Vision Understanding and Generation"
    link: /publications/
  - teaser_img: /assets/teaser/linjiaying_dap.png
    caption:
    title: "DAP: Doppler-aware Point Network for Heterogeneous mmWave Action Recognition"
    link: /publications/
  - teaser_img: /assets/teaser/wangziyi_skeletonllm.png
    caption:
    title: "Universal Skeleton Understanding via Differentiable Rendering and MLLMs"
    link: /publications/
  - teaser_img: /assets/teaser/wangxinshun_superman.png
    caption:
    title: "Superman: Unifying Skeleton and Vision for Human Motion Perception and Generation"
    link: /publications/
---

<style>
  .header-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 2rem;
    margin-top: 1rem;
  }

  .logo-container {
    display: flex;
    align-items: center;
    gap: 1rem;
  }

  .logo-container img {
    height: 72px;
    width: auto;
    object-fit: contain;
  }

  .lab-title {
    font-size: 2rem;
    font-weight: bold;
    color: var(--global-text-color);
    text-align: right;
  }

  @media (max-width: 576px) {
    .header-container {
      align-items: flex-start;
      flex-direction: column;
      gap: 1rem;
    }

    .lab-title {
      text-align: left;
    }
  }
</style>

<div class="header-container">
  <div class="logo-container">
    <img src="{{ '/assets/img/vit-pkusz/logo.png' | relative_url }}" alt="Visual Intelligence Team logo">
  </div>
  <div class="lab-title">Visual Intelligence Team</div>
</div>

<!-- ============================================ -->
<div class="clearfix"></div>
<!-- ============================================ -->

<!-- ============================================ -->
<!-- Swiper CSS -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.css">

<!-- Swiper Styles -->
<style>
  .swiper {
    width: 100%;
    height: 500px;
    margin-bottom: 2rem;
  }

  .swiper-slide {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background: var(--global-card-bg-color);
    text-align: center;
    font-size: 18px;
  }

  .swiper-button-next::after,
  .swiper-button-prev::after {
    color: var(--global-theme-color);
    font-size: 24px;
  }

  .swiper-pagination-bullet-active {
    background: var(--global-theme-color);
  }

  .swiper-slide video,
  .swiper-slide img {
    width: 100%;
    height: 100%;
    max-height: 400px;
    object-fit: contain;
    border-radius: 12px;
    background: #fff;
    box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15);
    overflow: hidden;
  }

  .slide-title {
    margin-top: 0.5rem;
    font-weight: bold;
    font-size: 1.1rem;
    color: var(--global-text-color);
  }
</style>

<!-- Swiper Markup -->
<div class="swiper mySwiper">
  <div class="swiper-wrapper">
    {% for item in page.highlighted_projects %}
      <div class="swiper-slide">
        {% if item.link %}
          <a href="{{ item.link | relative_url }}" style="text-decoration: none; color: inherit;">
        {% endif %}

        {% if item.teaser_video %}
          <video src="{{ item.teaser_video | relative_url }}" autoplay muted loop playsinline poster="{{ item.teaser_img | relative_url }}"></video>
        {% elsif item.teaser_img %}
          <img src="{{ item.teaser_img | relative_url }}" alt="{{ item.title }}">
        {% endif %}

        {% if item.title %}
          <div class="slide-title">{{ item.title }}</div>
        {% endif %}

        {% if item.link %}
          </a>
        {% endif %}
      </div>
    {% endfor %}
  </div>

  <div class="swiper-button-next"></div>
  <div class="swiper-button-prev"></div>
  <div class="swiper-pagination"></div>
</div>

<!-- Swiper JS -->
<script src="https://cdn.jsdelivr.net/npm/swiper@11/swiper-bundle.min.js"></script>

<!-- Swiper Initialization -->
<script>
  var swiper = new Swiper(".mySwiper", {
    spaceBetween: 30,
    centeredSlides: true,
    loop: false,
    watchSlidesProgress: true,
    speed: 1000,
    effect: "fade",
    fadeEffect: {
      crossFade: true,
    },
    autoplay: {
      delay: {{ page.carousel_autoplay_delay | default: 3500 }},
      disableOnInteraction: false,
      reverseDirection: false,
      stopOnLastSlide: false,
    },
    pagination: {
      el: ".swiper-pagination",
      clickable: true,
      dynamicBullets: false,
      type: "bullets",
    },
    navigation: {
      nextEl: ".swiper-button-next",
      prevEl: ".swiper-button-prev",
    },
    on: {
      slideChangeTransitionStart: function () {
        const activeSlide = this.slides[this.activeIndex];
        const activeVideo = activeSlide.querySelector("video");
        if (activeVideo) {
          activeVideo.currentTime = 0;
          activeVideo.play();
        }
      },
      slideChangeTransitionEnd: function () {
        const videos = document.querySelectorAll(".swiper-slide video");
        videos.forEach((video, index) => {
          if (index !== this.activeIndex) {
            video.pause();
            video.currentTime = 0;
          }
        });
      },
      init: function () {
        const firstVideo = this.slides[0].querySelector("video");
        if (firstVideo) {
          firstVideo.currentTime = 0;
          firstVideo.play();
        }
      },
      reachEnd: function () {
        setTimeout(() => {
          this.slideTo(0);
        }, {{ page.carousel_autoplay_delay | default: 3500 }});
      },
    },
  });
</script>

<!-- ============================================ -->
<!-- News -->
<h2>News</h2>
{% include news.liquid %}
<!-- ============================================ -->

<!-- ============================================ -->
<!-- Research Directions -->
<h2>Research Directions</h2>

<style>
  .rd-grid { display: grid; gap: 20px; grid-template-columns: 1fr; }
  @media (min-width: 900px) { .rd-grid { grid-template-columns: 1fr 1fr; } }
  .rd-card { background: var(--global-card-bg-color); border: 1px solid var(--global-divider-color); border-radius: 8px; padding: 18px; box-shadow: 0 4px 20px rgba(0,0,0,0.06); }
  .rd-card h3 { margin-top: 0; }
  .rd-subgrid { display: grid; gap: 18px; grid-template-columns: 1fr; margin-top: 18px; }
  .rd-item { display: grid; gap: 8px; }
  .rd-item img { width: 100%; aspect-ratio: 16 / 9; object-fit: cover; border-radius: 8px; display: block; background: #fff; }
  .rd-item h4 { margin: 0; font-size: 1.02rem; line-height: 1.3; }
  .rd-item p { margin: 0; color: var(--global-text-color); font-size: 0.95rem; line-height: 1.5; }
</style>

<div class="rd-grid">
  <div class="rd-card">
    <h3>Research Direction 1: Open-world Human and Object Search</h3>
    <p>This direction focuses on enabling intelligent agents to perceive, search for, and understand humans and objects in complex open-world environments. It emphasizes long-term memory, privacy-aware human sensing, language-guided search, and open-vocabulary perception, allowing AI systems and embodied agents to identify targets beyond predefined categories and operate reliably in dynamic real-world scenarios.</p>

    <div class="rd-subgrid" style="margin-top:12px;">
      <div class="rd-item">
        <h4>Ultra-long Video Memory Update and Retrieval</h4>
        <img src="{{ '/assets/img/ResearchDirections/ultra-long-video-memory.png' | relative_url }}" alt="Ultra-long Video Memory Update and Retrieval" loading="lazy">
        <p>This sub-direction studies how AI systems can continuously build, update, and retrieve memories from ultra-long video streams. By modeling long-term temporal context, hierarchical memory structures, and efficient retrieval mechanisms, agents can recall relevant events, understand long-duration activities, and reason over extended visual histories.</p>
      </div>

      <div class="rd-item">
        <h4>Privacy-Preserving Human Sensing</h4>
        <img src="{{ '/assets/img/ResearchDirections/privacy-preserving-human-sensing.png' | relative_url }}" alt="Privacy-Preserving Human Sensing" loading="lazy">
        <p>This sub-direction aims to perceive human behaviors, activities, and states while protecting personal privacy. Instead of relying on identity-sensitive raw visual information, it explores privacy-friendly representations such as skeleton poses, depth silhouettes, thermal maps, point clouds, and anonymized features for reliable human understanding.</p>
      </div>

      <div class="rd-item">
        <h4>Text-based Novel Object Search</h4>
        <img src="{{ '/assets/img/ResearchDirections/text-based-novel-object-search.png' | relative_url }}" alt="Text-based Novel Object Search" loading="lazy">
        <p>This sub-direction explores how embodied agents can search for unknown or unseen objects based on natural language descriptions. By combining vision-language grounding, open-vocabulary perception, semantic attribute reasoning, and active exploration, robots can locate novel objects in complex environments even when the object category has not been predefined.</p>
      </div>
    </div>
  </div>

  <div class="rd-card">
    <h3>Research Direction 2: Generalizable Embodied Manipulation</h3>
    <p>This direction focuses on developing embodied agents that can flexibly manipulate diverse objects and accomplish novel tasks across different environments. It emphasizes 3D affordance understanding, task generalization, skill composition, and continual learning from demonstrations, enabling robots to adapt their manipulation policies to unseen objects, scenes, and task requirements.</p>

    <div class="rd-subgrid" style="margin-top:12px;">
      <div class="rd-item">
        <h4>3D Affordance Estimation for Unknown Objects</h4>
        <img src="{{ '/assets/img/ResearchDirections/3d-affordance-estimation.png' | relative_url }}" alt="3D Affordance Estimation" loading="lazy">
        <p>This sub-direction studies how robots can infer actionable functional regions of unknown objects from 3D observations. By understanding geometric structures and object affordances such as grasping, pouring, supporting, opening, and containing, robots can interact with unfamiliar objects without relying on fixed category labels or prior object models.</p>
      </div>

      <div class="rd-item">
        <h4>Embodied Manipulation for Generalizable Tasks</h4>
        <img src="{{ '/assets/img/ResearchDirections/embodied-manipulation-generalizable-tasks.png' | relative_url }}" alt="Embodied Manipulation for Generalizable Tasks" loading="lazy">
        <p>This sub-direction aims to build manipulation policies that generalize across objects, scenes, and task goals. Through multimodal perception, language-conditioned task understanding, skill composition, and long-horizon planning, robots can perform diverse manipulation tasks in unseen environments with improved robustness and flexibility.</p>
      </div>

      <div class="rd-item">
        <h4>Incremental Manipulation from Human Demonstrations</h4>
        <img src="{{ '/assets/img/ResearchDirections/incremental-manipulation-human-demonstrations.png' | relative_url }}" alt="Incremental Manipulation from Human Demonstrations" loading="lazy">
        <p>This sub-direction investigates how robots can continuously improve their manipulation abilities by learning from human demonstrations. Instead of relying on a fixed training dataset, robots incrementally acquire new skills, update policies, mitigate forgetting, and improve task performance over time through demonstration-driven and human-in-the-loop learning.</p>
      </div>
    </div>
  </div>
</div>
