---
layout: default
title: 🍦 Icecream
description: High-Fidelity Equivariant Cryo-Electron Tomography
show_downloads: false
google_analytics:
theme: jekyll-theme-cayman
banner: "../assets/images/band_icecream.png"
github: 
  repository_url: https://github.com/swing-research/icecream
  is_project_page: true
arxiv:
  display: true
  link: https://www.biorxiv.org/content/10.1101/2025.10.17.682746v1
  nameJournal: BioArxv
paper:
  display: true
  name: Acta Cryst. D
  link: https://journals.iucr.org/d/issues/2026/04/00/zi5009/index.html
website:
  display: false
  link: https://sites.google.com/view/debarnot/
  name: Valentin Debarnot
---

<style>
h1.project-name { color: rgba(139, 125, 199, 1) !important; }
h2.project-tagline { color: rgba(139, 125, 199, 1) !important; }
header a.btn { color: rgba(139, 125, 199, 1) !important; 
border-color: rgba(139, 125, 199, 1) !important; 
background-color: rgba(138, 125, 199, 0.16) !important; }
</style>


<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="./examples.html" class="btn">← Previous</a>
  <a href="../icecream.html" class="btn">Home</a>
  <a href="./reference.html" class="btn">Next →</a>
</div>

<style>
.btn {
  display: inline-block;
  padding: 8px 16px;
  background-color: rgba(139, 125, 199, 1);
  color: white !important;
  text-decoration: none;
  border-radius: 6px;
  font-weight: bold;
  transition: background-color 0.2s;
}
.btn:hover {
  background-color: rgba(139, 125, 199, 1)
}
</style>

<h1 id="split">Influence of splitting strategy</h1>
Icecream requires two statistically independent tomograms. There are two choices for producing these volumes: either splitting the dose (requires recent cameras) or splitting the tilt angles (leaving less tilt to accurately reconstruct the volumes). In the following, we have quantitatively measured the difference between the two strategies. As already reported in the literature, we observed that splitting the dose produces slightly more denoised tomograms.

We use the dataset of flagella of C. reinhardtii, which is the tutorial dataset used in cryo-CARE and contains 10 raw frames per tilt. This flexibility allows us to compute 4 tomograms that are used by pairs to generate 2 independent results and then compute the FSC. The projections were collected at angles from −65° to +65° with 2° increments; pixel size is 2.36 Å. The tilt-series is further downsampled by a factor of 6, resulting in an effective pixel resolution of 14.16 Å.

* * * 
<h2 id="split-dose">Dose splitting</h2>


<!-- ====================== FIGURE 0 ====================== -->
<div id="custom-figure-0">
  <style>
    #custom-figure-0 .viewer {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 5px;
      justify-items: center;
      align-items: center;
    }
    #custom-figure-0 .img-column {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 5px;
    }
    #custom-figure-0 .img-wrapper {
      position: relative;
      overflow: hidden;
      border: 1px solid #ccc;
      width: 400px;
      height: 400px;
      background: #fff;
    }
    #custom-figure-0 .img-title {
      font-weight: bold;
      font-size: 16px;
      margin-bottom: 0px;
      text-align: center;
      width: 100%;
    }
    #custom-figure-0 img {
      width: 100%;
      height: 100%;
      object-fit: contain;
      transition: transform 0.15s ease;
      transform-origin: center center;
      cursor: crosshair;
    }
    #custom-figure-0 #controls {
      margin-top: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 10px;
    }
    #custom-figure-0 #zoomButtons1 {
      display: flex;
      gap: 10px;
      justify-content: center;
      margin-top: 10px;
    }
  </style>



<div class="viewer">
<div class="img-column">
  <div class="img-title"> </div>
  <div class="img-wrapper">
    <img id="img1" src="/images/icecream/Equivariant_dose.png" alt="Example Image" width="400">
  </div>
</div>
<div class="img-column">
  <div class="img-title">🍦 ICECREAM</div>
  <div class="img-wrapper">
    <img id="img2" src="../images/icecream/png/angle_vs_dose/dose_slice_00026.jpg">
  </div>
</div>
</div>

  
<!-- <p align="center">
  <img src="{{ '/images/icecream/Equivariant_dose.png' | relative_url }}" 
       alt="Example Image" width="400"> 
</p> -->


<div id="controls">
    <input type="range" id="sliceSlider0" min="0" max="52" step="1" value="26">
    <span id="sliceValue0">Slice: 26</span>
  </div>

  <div id="zoomButtons1">
    <button id="zoomIn1">🔍 Zoom In</button>
    <button id="zoomOut1">➖ Zoom Out</button>
    <button id="resetZoom1">↩️ Reset</button>
  </div>

  <script>
    (function() {
      const container = document.querySelector('#custom-figure-0');
      const sliceSlider0 = document.getElementById('sliceSlider0');
      const sliceValue0 = document.getElementById('sliceValue0');
      const zoomInBtn = container.querySelector('#zoomIn1');
      const zoomOutBtn = container.querySelector('#zoomOut1');
      const resetZoomBtn = container.querySelector('#resetZoom1');
      const imgs = Array.from(container.querySelectorAll('img'));

      let zoomLevel = 1.0;
      let originX = 50, originY = 50;
      let isDragging = false;

      // Update all 4 images when slider changes
      function updateImages() {
        const index = parseInt(sliceSlider0.value, 10);
        const padded = String(index).padStart(5, '0');
        sliceValue0.textContent = `Slice: ${index}`;
        imgs[0].src = `/images/icecream/Equivariant_dose.png`;
        imgs[1].src = `../images/icecream/png/angle_vs_dose/dose_slice_${padded}.jpg`;
      }

      // Apply zoom to all images
      function applyZoom() {
        const img = imgs[1]
        img.style.transformOrigin = `${originX}% ${originY}%`;
        img.style.transform = `scale(${zoomLevel})`;
      }

      // Track cursor position for zoom origin
      function handleMouseMove(e, wrapper) {
        const rect = wrapper.getBoundingClientRect();
        originX = ((e.clientX - rect.left) / rect.width) * 100;
        originY = ((e.clientY - rect.top) / rect.height) * 100;
        // applyZoom();
      }

      // Handle zoom with mouse wheel
      function handleWheel(e) {
        e.preventDefault();
        zoomLevel *= e.deltaY < 0 ? 1.1 : 0.9;
        zoomLevel = Math.min(Math.max(zoomLevel, 1), 15);
        applyZoom();
      }

      // Event listeners
      container.querySelectorAll('.img-wrapper').forEach(wrapper => {
        wrapper.addEventListener('mousemove', (e) => handleMouseMove(e, wrapper));
        wrapper.addEventListener('wheel', handleWheel, { passive: false });
      });

      sliceSlider0.addEventListener('input', updateImages);
      zoomInBtn.addEventListener('click', () => { zoomLevel *= 1.25; applyZoom(); });
      zoomOutBtn.addEventListener('click', () => { zoomLevel /= 1.25; applyZoom(); });
      resetZoomBtn.addEventListener('click', () => { zoomLevel = 1; originX = originY = 50; applyZoom(); });

      applyZoom();
    })();
  </script>
</div>


<div style="height: 50px;"></div>



* * * 
<h2 id="split-tilt">Tilt splitting</h2>
<!-- <p align="center">
  <img src="{{ '/images/icecream/Equivariant_angle.png' | relative_url }}" 
       alt="Example Image" width="400">
</p> -->



<!-- ====================== FIGURE 0 ====================== -->
<div id="custom-figure-00">
  <style>
    #custom-figure-00 .viewer {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 5px;
      justify-items: center;
      align-items: center;
    }
    #custom-figure-00 .img-column {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 5px;
    }
    #custom-figure-00 .img-wrapper {
      position: relative;
      overflow: hidden;
      border: 1px solid #ccc;
      width: 400px;
      height: 400px;
      background: #fff;
    }
    #custom-figure-00 .img-title {
      font-weight: bold;
      font-size: 16px;
      margin-bottom: 0px;
      text-align: center;
      width: 100%;
    }
    #custom-figure-00 img {
      width: 100%;
      height: 100%;
      object-fit: contain;
      transition: transform 0.15s ease;
      transform-origin: center center;
      cursor: crosshair;
    }
    #custom-figure-00 #controls {
      margin-top: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 10px;
    }
    #custom-figure-00 #zoomButtons11 {
      display: flex;
      gap: 10px;
      justify-content: center;
      margin-top: 10px;
    }
  </style>
<div class="viewer">
<div class="img-column">
  <div class="img-title"> </div>
  <div class="img-wrapper">
    <img id="img1" src="/images/icecream/Equivariant_angle.png" alt="Example Image" width="400">
  </div>
</div>
<div class="img-column">
  <div class="img-title">🍦 ICECREAM</div>
  <div class="img-wrapper">
    <img id="img2" src="../images/icecream/png/angle_vs_dose/angle_slice_00026.jpg">
  </div>
</div>
</div>

  

<div id="controls">
    <input type="range" id="sliceSlider00" min="0" max="52" step="1" value="26">
    <span id="sliceValue00">Slice: 26</span>
  </div>

  <div id="zoomButtons11">
    <button id="zoomIn11">🔍 Zoom In</button>
    <button id="zoomOut11">➖ Zoom Out</button>
    <button id="resetZoom11">↩️ Reset</button>
  </div>

  <script>
    (function() {
      const container = document.querySelector('#custom-figure-00');
      const sliceSlider0 = document.getElementById('sliceSlider00');
      const sliceValue0 = document.getElementById('sliceValue00');
      const zoomInBtn = container.querySelector('#zoomIn11');
      const zoomOutBtn = container.querySelector('#zoomOut11');
      const resetZoomBtn = container.querySelector('#resetZoom11');
      const imgs = Array.from(container.querySelectorAll('img'));

      let zoomLevel = 1.0;
      let originX = 50, originY = 50;
      let isDragging = false;

      // Update all 4 images when slider changes
      function updateImages() {
        const index = parseInt(sliceSlider0.value, 10);
        const padded = String(index).padStart(5, '0');
        sliceValue0.textContent = `Slice: ${index}`;
        imgs[0].src = `/images/icecream/Equivariant_angle.png`;
        imgs[1].src = `../images/icecream/png/angle_vs_dose/angle_slice_${padded}.jpg`;
      }

      // Apply zoom to all images
      function applyZoom() {
        const img = imgs[1]
        img.style.transformOrigin = `${originX}% ${originY}%`;
        img.style.transform = `scale(${zoomLevel})`;
      }

      // Track cursor position for zoom origin
      function handleMouseMove(e, wrapper) {
        const rect = wrapper.getBoundingClientRect();
        originX = ((e.clientX - rect.left) / rect.width) * 100;
        originY = ((e.clientY - rect.top) / rect.height) * 100;
        // applyZoom();
      }

      // Handle zoom with mouse wheel
      function handleWheel(e) {
        e.preventDefault();
        zoomLevel *= e.deltaY < 0 ? 1.1 : 0.9;
        zoomLevel = Math.min(Math.max(zoomLevel, 1), 15);
        applyZoom();
      }

      // Event listeners
      container.querySelectorAll('.img-wrapper').forEach(wrapper => {
        wrapper.addEventListener('mousemove', (e) => handleMouseMove(e, wrapper));
        wrapper.addEventListener('wheel', handleWheel, { passive: false });
      });

      sliceSlider0.addEventListener('input', updateImages);
      zoomInBtn.addEventListener('click', () => { zoomLevel *= 1.25; applyZoom(); });
      zoomOutBtn.addEventListener('click', () => { zoomLevel /= 1.25; applyZoom(); });
      resetZoomBtn.addEventListener('click', () => { zoomLevel = 1; originX = originY = 50; applyZoom(); });

      applyZoom();
    })();
  </script>
</div>


<div style="height: 50px;"></div>

* * * 
<h2 id="split-tilt">Tilt vs angle splitting</h2>
We display the FSC of Icecream depending on the splitting scheme, and we observe that the difference is only marginal in this example.

<p align="center">
  <img src="{{ '/images/icecream/Equivariant_compare.png' | relative_url }}" 
       alt="Example Image" width="400"> 
</p>





<!-- ====================== FIGURE 0 ====================== -->
<div id="custom-figure-000">
  <style>
    #custom-figure-000 .viewer {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 5px;
      justify-items: center;
      align-items: center;
    }
    #custom-figure-000 .img-column {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 5px;
    }
    #custom-figure-000 .img-wrapper {
      position: relative;
      overflow: hidden;
      border: 1px solid #ccc;
      width: 400px;
      height: 400px;
      background: #fff;
    }
    #custom-figure-000 .img-title {
      font-weight: bold;
      font-size: 16px;
      margin-bottom: 0px;
      text-align: center;
      width: 100%;
    }
    #custom-figure-000 img {
      width: 100%;
      height: 100%;
      object-fit: contain;
      transition: transform 0.15s ease;
      transform-origin: center center;
      cursor: crosshair;
    }
    #custom-figure-000 #controls {
      margin-top: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 10px;
    }
    #custom-figure-000 #zoomButtons111 {
      display: flex;
      gap: 10px;
      justify-content: center;
      margin-top: 10px;
    }
  </style>
<div class="viewer">
<div class="img-column">
  <div class="img-title"> Dose splitting </div>
  <div class="img-wrapper">
    <img id="img1" src="../images/icecream/png/angle_vs_dose/dose_slice_00026.jpg">
  </div>
</div>
<div class="img-column">
  <div class="img-title">Angle splitting </div>
  <div class="img-wrapper">
    <img id="img2" src="../images/icecream/png/angle_vs_dose/angle_slice_00026.jpg">
  </div>
</div>
</div>

  

<div id="controls">
    <input type="range" id="sliceSlider000" min="0" max="52" step="1" value="26">
    <span id="sliceValue000">Slice: 26</span>
  </div>

  <div id="zoomButtons111">
    <button id="zoomIn111">🔍 Zoom In</button>
    <button id="zoomOut111">➖ Zoom Out</button>
    <button id="resetZoom111">↩️ Reset</button>
  </div>

  <script>
    (function() {
      const container = document.querySelector('#custom-figure-000');
      const sliceSlider0 = document.getElementById('sliceSlider000');
      const sliceValue0 = document.getElementById('sliceValue000');
      const zoomInBtn = container.querySelector('#zoomIn111');
      const zoomOutBtn = container.querySelector('#zoomOut111');
      const resetZoomBtn = container.querySelector('#resetZoom111');
      const imgs = Array.from(container.querySelectorAll('img'));

      let zoomLevel = 1.0;
      let originX = 50, originY = 50;
      let isDragging = false;

      // Update all 4 images when slider changes
      function updateImages() {
        const index = parseInt(sliceSlider0.value, 10);
        const padded = String(index).padStart(5, '0');
        sliceValue0.textContent = `Slice: ${index}`;
        imgs[0].src = `../images/icecream/png/angle_vs_dose/dose_slice_${padded}.jpg`;
        imgs[1].src = `../images/icecream/png/angle_vs_dose/angle_slice_${padded}.jpg`;
      }

      // Apply zoom to all images
      function applyZoom() {
        imgs.forEach(img => {
          img.style.transformOrigin = `${originX}% ${originY}%`;
          img.style.transform = `scale(${zoomLevel})`;
        });
      }

      // Track cursor position for zoom origin
      function handleMouseMove(e, wrapper) {
        const rect = wrapper.getBoundingClientRect();
        originX = ((e.clientX - rect.left) / rect.width) * 100;
        originY = ((e.clientY - rect.top) / rect.height) * 100;
        // applyZoom();
      }

      // Handle zoom with mouse wheel
      function handleWheel(e) {
        e.preventDefault();
        zoomLevel *= e.deltaY < 0 ? 1.1 : 0.9;
        zoomLevel = Math.min(Math.max(zoomLevel, 1), 15);
        applyZoom();
      }

      // Event listeners
      container.querySelectorAll('.img-wrapper').forEach(wrapper => {
        wrapper.addEventListener('mousemove', (e) => handleMouseMove(e, wrapper));
        wrapper.addEventListener('wheel', handleWheel, { passive: false });
      });

      sliceSlider0.addEventListener('input', updateImages);
      zoomInBtn.addEventListener('click', () => { zoomLevel *= 1.25; applyZoom(); });
      zoomOutBtn.addEventListener('click', () => { zoomLevel /= 1.25; applyZoom(); });
      resetZoomBtn.addEventListener('click', () => { zoomLevel = 1; originX = originY = 50; applyZoom(); });

      applyZoom();
    })();
  </script>
</div>







<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="./examples.html" class="btn">← Previous</a>
  <a href="../icecream.html" class="btn">Home</a>
  <a href="./reference.html" class="btn">Next →</a>
</div>

<style>
.btn {
  display: inline-block;
  padding: 8px 16px;
  background-color: rgba(139, 125, 199, 1);
  color: white !important;
  text-decoration: none;
  border-radius: 6px;
  font-weight: bold;
  transition: background-color 0.2s;
}
.btn:hover {
  background-color: rgba(139, 125, 199, 1)
}
</style>


<!-- [Projects home](./index.html) -->