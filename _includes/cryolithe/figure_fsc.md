
<!-- ====================== FIGURE 0 ====================== -->
<div id="custom-figure-1">
  <style>
    #custom-figure-1 .viewer {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 5px;
      justify-items: center;
      align-items: center;
    }
    #custom-figure-1 .img-column {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 5px;
    }
    #custom-figure-1 .img-wrapper {
      position: relative;
      overflow: hidden;
      border: 1px solid #ccc;
      width: 400px;
      height: 400px;
      background: #fff;
    }
    #custom-figure-1 .img-title {
      font-weight: bold;
      font-size: 16px;
      margin-bottom: 0px;
      text-align: center;
      width: 100%;
    }
    #custom-figure-1 img {
      width: 100%;
      height: 100%;
      object-fit: contain;
      transition: transform 0.15s ease;
      transform-origin: center center;
      cursor: crosshair;
    }
    #custom-figure-1 #controls {
      margin-top: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 10px;
    }
    #custom-figure-1 #zoomButtons1 {
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
    <img id="img1" src="../images/cryolithe/png/figure_3/FSC_fig3.png" alt="Example Image" width="400">
  </div>
</div>
<div class="img-column">
  <div class="img-title">❄️ CryoLithe</div>
  <div class="img-wrapper">
    <img id="img2" src="../images/cryolithe/png/figure_3/cryolithe_wavlet_icecream_train/slice_00035.jpg">
  </div>
</div>
<div class="img-column">
  <div class="img-title">🍦 ICECREAM</div>
  <div class="img-wrapper">
    <img id="img2" src="../images/cryolithe/png/figure_3/vol_EVN_fbp_vol_ODD_fbp_ei/slice_00035.jpg">
  </div>
</div>
<div class="img-column">
  <div class="img-title"> FBP </div>
  <div class="img-wrapper">
    <img id="img2" src="../images/cryolithe/png/figure_3/fbp/slice_00035.jpg">
  </div>
</div>
</div>

  
<!-- <p align="center">
  <img src="{{ '../images/icecream/Equivariant_dose.png' | relative_url }}" 
       alt="Example Image" width="400"> 
</p> -->


<div id="controls">
    <input type="range" id="sliceSlider1" min="0" max="77" step="1" value="35">
    <span id="sliceValue1">Slice: 35</span>
  </div>

  <div id="zoomButtons1">
    <button id="zoomIn1">🔍 Zoom In</button>
    <button id="zoomOut1">➖ Zoom Out</button>
    <button id="resetZoom1">↩️ Reset</button>
  </div>

  <script>
    (function() {
      const container = document.querySelector('#custom-figure-1');
      const sliceSlider1 = document.getElementById('sliceSlider1');
      const sliceValue1 = document.getElementById('sliceValue1');
      const zoomInBtn = container.querySelector('#zoomIn1');
      const zoomOutBtn = container.querySelector('#zoomOut1');
      const resetZoomBtn = container.querySelector('#resetZoom1');
      const imgs = Array.from(container.querySelectorAll('img'));

      let zoomLevel = 1.0;
      let originX = 50, originY = 50;
      let isDragging = false;

      // Update all 4 images when slider changes
      function updateImages() {
        const index = parseInt(sliceSlider1.value, 10);
        const padded = String(index).padStart(5, '0');
        sliceValue1.textContent = `Slice: ${index}`;
        imgs[1].src = `../images/cryolithe/png/figure_3/cryolithe_wavlet_icecream_train/slice_${padded}.jpg`;
        imgs[2].src = `../images/cryolithe/png/figure_3/vol_EVN_fbp_vol_ODD_fbp_ei/slice_${padded}.jpg`;
        imgs[3].src = `../images/cryolithe/png/figure_3/fbp/slice_${padded}.jpg`;
      }

      // Apply zoom to all images
      function applyZoom() {
        const img = imgs[1]
        img.style.transformOrigin = `${originX}% ${originY}%`;
        img.style.transform = `scale(${zoomLevel})`;
        const img2 = imgs[2]
        img2.style.transformOrigin = `${originX}% ${originY}%`;
        img2.style.transform = `scale(${zoomLevel})`;
        const img3 = imgs[3]
        img3.style.transformOrigin = `${originX}% ${originY}%`;
        img3.style.transform = `scale(${zoomLevel})`;
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

      sliceSlider1.addEventListener('input', updateImages);
      zoomInBtn.addEventListener('click', () => { zoomLevel *= 1.25; applyZoom(); });
      zoomOutBtn.addEventListener('click', () => { zoomLevel /= 1.25; applyZoom(); });
      resetZoomBtn.addEventListener('click', () => { zoomLevel = 1; originX = originY = 50; applyZoom(); });

      applyZoom();
    })();
  </script>
</div>


<div style="height: 50px;"></div>