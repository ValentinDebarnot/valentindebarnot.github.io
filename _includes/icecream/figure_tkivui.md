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
      <div class="img-title">🍦 ICECREAM</div>
      <div class="img-wrapper">
        <img id="img1" src="images/icecream/png/tkviu_eq/slice_00032.jpg">
      </div>
    </div>
    <div class="img-column">
      <div class="img-title">DeepDeWedge</div>
      <div class="img-wrapper">
        <img id="img2" src="images/icecream/png/tkviu_ddw/slice_00032.jpg">
      </div>
    </div>
    <div class="img-column">
      <div class="img-title">CryoLithe</div>
      <div class="img-wrapper">
        <img id="img3" src="images/icecream/png/tkviui_cryolithe/slice_00032.jpg">
      </div>
    </div>
    <div class="img-column">
      <div class="img-title">FBP</div>
      <div class="img-wrapper">
        <img id="img4" src="images/icecream/png/tomo2_L1G1-dose_filt-bin4_EVN/slice_00032.jpg">
      </div>
    </div>
  </div>

  <div id="controls">
    <input type="range" id="sliceSlider0" min="0" max="65" step="1" value="32">
    <span id="sliceValue0">Slice: 32  </span>
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
        imgs[0].src = `images/icecream/png/tkviu_eq/slice_${padded}.jpg`;
        imgs[1].src = `images/icecream/png/tkviu_ddw/slice_${padded}.jpg`;
        imgs[2].src = `images/icecream/png/tkviui_cryolithe/slice_${padded}.jpg`;
        imgs[3].src = `images/icecream/png/tomo2_L1G1-dose_filt-bin4_EVN/slice_${padded}.jpg`;
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


<div style="height: 50px;"></div>


<!-- ====================== FIGURE 2 ====================== -->
<div id="custom-figure-02">
  <style>
    #custom-figure-02 .viewer {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 5px;
      justify-items: center;
      align-items: center;
    }
    #custom-figure-02 .img-column {
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 5px;
    }
    #custom-figure-02 .img-wrapper {
      position: relative;
      overflow: hidden;
      border: 2px dashed #666;
      width: 400px;
      height: 200px;
      background: #f5f5f5;
    }
    #custom-figure-02 .img-title {
      font-weight: bold;
      font-size: 14px;
      margin-bottom: 5px;
      text-align: center;
      width: 100%;
      color: #444;
    }
    #custom-figure-02 img {
      width: 100%;
      height: 100%;
      object-fit: contain;
      transition: transform 0.15s ease;
      transform-origin: center center;
      cursor: zoom-in;
    }
    #custom-figure-02 #zoomButtons2 {
      display: flex;
      gap: 10px;
      justify-content: center;
      margin-top: 10px;
    }
  </style>

  <div class="viewer">
    <div class="img-column">
      <div class="img-title">🍦 ICECREAM</div>
      <div class="img-wrapper">
        <img id="img1_2" src="images/icecream/png/tkviu_eq/FT.png" alt="ICECREAM Tomo 1">
      </div>
    </div>
    <div class="img-column">
      <div class="img-title">DeepDeWedge</div>
      <div class="img-wrapper">
        <img id="img2_2" src="images/icecream/png/tkviu_ddw/FT.png" alt="DeepDeWedge Tomo 1">
      </div>
    </div>
    <div class="img-column">
      <div class="img-title">🍦 CryoLithe</div>
      <div class="img-wrapper">
        <img id="img3_2" src="images/icecream/png/tkviui_cryolithe/FT.png" alt="ICECREAM Tomo 2">
      </div>
    </div>
    <div class="img-column">
      <div class="img-title">FBP</div>
      <div class="img-wrapper">
        <img id="img4_2" src="images/icecream/png/tomo2_L1G1-dose_filt-bin4_EVN/FT.png" alt="DeepDeWedge Tomo 2">
      </div>
    </div>
  </div>

  <div id="zoomButtons2">
    <button id="zoomIn2">🔍 Zoom In</button>
    <button id="zoomOut2">➖ Zoom Out</button>
    <button id="resetZoom2">↩️ Reset</button>
  </div>

  <script>
    (function() {
      const container = document.querySelector('#custom-figure-02');
      const zoomInBtn = container.querySelector('#zoomIn2');
      const zoomOutBtn = container.querySelector('#zoomOut2');
      const resetZoomBtn = container.querySelector('#resetZoom2');
      const imgs = Array.from(container.querySelectorAll('img'));

      let zoomLevel = 1.0;
      let originX = 50, originY = 50;

      // Apply zoom to all 4 images
      function applyZoom() {
        imgs.forEach(img => {
          img.style.transformOrigin = `${originX}% ${originY}%`;
          img.style.transform = `scale(${zoomLevel})`;
        });
      }

      // Update zoom center based on cursor
      function handleMouseMove(e, wrapper) {
        const rect = wrapper.getBoundingClientRect();
        originX = ((e.clientX - rect.left) / rect.width) * 100;
        originY = ((e.clientY - rect.top) / rect.height) * 100;
      }

      // Zoom in/out with mouse wheel
      function handleWheel(e) {
        e.preventDefault();
        zoomLevel *= e.deltaY < 0 ? 1.1 : 0.9;
        zoomLevel = Math.min(Math.max(zoomLevel, 1), 15);
        applyZoom();
      }

      // Attach listeners to all image wrappers
      container.querySelectorAll('.img-wrapper').forEach(wrapper => {
        wrapper.addEventListener('mousemove', (e) => handleMouseMove(e, wrapper));
        wrapper.addEventListener('wheel', handleWheel, { passive: false });
      });

      // Zoom control buttons
      zoomInBtn.addEventListener('click', () => { originX = originY = 50; zoomLevel = Math.min(zoomLevel * 1.25, 15); applyZoom(); });
      zoomOutBtn.addEventListener('click', () => { originX = originY = 50; zoomLevel = Math.max(zoomLevel / 1.25, 1); applyZoom(); });
      resetZoomBtn.addEventListener('click', () => { zoomLevel = 1; originX = originY = 50; applyZoom(); });

      applyZoom();
    })();
  </script>
</div>