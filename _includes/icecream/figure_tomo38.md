<!-- ====================== FIGURE 5 ====================== -->
<div id="custom-figure-5">
  <style>
    #custom-figure-5 .viewer {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 20px;
    }
    #custom-figure-5 .img-wrapper {
      position: relative;
      overflow: hidden;
      border: 1px solid #ccc;
      width: 400px;
      height: 400px;
      background: #fff;
    }
    #custom-figure-5 .img-title {
      font-weight: bold;
      font-size: 16px;
      margin-bottom: 5px;
      text-align: center;
      width: 100%;
    }
    #custom-figure-5 img {
      width: 100%;
      height: 100%;
      object-fit: contain;
      transition: transform 0.15s ease;
      transform-origin: center center;
      cursor: crosshair;
    }
    #custom-figure-5 #controls {
      margin-top: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 10px;
    }
    #custom-figure-5 #zoomButtons1 {
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
        <img id="imgEq1" src="../images/icecream/png/tomo_038_eq/slice_00032.jpg">
      </div>
    </div>
    <div class="img-column">
      <div class="img-title">DeepDeWedge</div>
      <div class="img-wrapper">
        <img id="imgDdw1" src="../images/icecream/png/tomo_038_ddw/slice_00032.jpg">
      </div>
    </div>
  </div>

  <div id="controls">
    <input type="range" id="sliceSlider5" min="0" max="65" step="1" value="32">
    <span id="sliceValue5">Slice: 32</span>
  </div>
  <div id="zoomButtons1">
    <button id="zoomIn1">🔍 Zoom In</button>
    <button id="zoomOut1">➖ Zoom Out</button>
    <button id="resetZoom1">↩️ Reset</button>
  </div>

  <script>
    (function() {
      const container = document.querySelector('#custom-figure-5');
      const imgEq = container.querySelector('#imgEq1');
      const imgDdw = container.querySelector('#imgDdw1');
      const sliceSlider5 = document.getElementById('sliceSlider5');
      const sliceValue5 = document.getElementById('sliceValue5');
      const zoomInBtn = container.querySelector('#zoomIn1');
      const zoomOutBtn = container.querySelector('#zoomOut1');
      const resetZoomBtn = container.querySelector('#resetZoom1');

      let zoomLevel = 1.0;
      let originX = 50, originY = 50;

      // Update slice images
      function updateImages5() {
        const index = parseInt(sliceSlider5.value, 10);
        const padded = String(index).padStart(5, '0');
        sliceValue5.textContent = `Slice: ${index}`;
        imgEq.src = `../images/icecream/png/tomo_038_eq/slice_${padded}.jpg`;
        imgDdw.src = `../images/icecream/png/tomo_038_ddw/slice_${padded}.jpg`;
      }

      function applyZoom() {
        [imgEq, imgDdw].forEach(img => {
          img.style.transformOrigin = `${originX}% ${originY}%`;
          img.style.transform = `scale(${zoomLevel})`;
        });
      }

      function handleMouseMove(e, wrapper) {
        const rect = wrapper.getBoundingClientRect();
        originX = ((e.clientX - rect.left) / rect.width) * 100;
        originY = ((e.clientY - rect.top) / rect.height) * 100;
      }

      function handleWheel(e) {
        e.preventDefault();
        zoomLevel *= e.deltaY < 0 ? 1.1 : 0.9;
        zoomLevel = Math.min(Math.max(zoomLevel, 1), 15);
        applyZoom();
      }

      container.querySelectorAll('.img-wrapper').forEach(wrapper => {
        wrapper.addEventListener('mousemove', (e) => handleMouseMove(e, wrapper));
        wrapper.addEventListener('wheel', handleWheel, { passive: false });
      });

      // Slice slider event
      sliceSlider5.addEventListener('input', updateImages5);

      zoomInBtn.addEventListener('click', () => { zoomLevel *= 1.25; applyZoom(); });
      zoomOutBtn.addEventListener('click', () => { zoomLevel /= 1.25; applyZoom(); });
      resetZoomBtn.addEventListener('click', () => { zoomLevel = 1; originX = originY = 50; applyZoom(); });

      applyZoom();
    })();
  </script>
</div>

<div style="height: 50px;"></div>


<!-- ====================== FIGURE 6 ====================== -->
<div id="custom-figure-6">
  <style>
    #custom-figure-6 .viewer {
      display: flex;
      justify-content: center;
      align-items: center;
      gap: 20px;
    }
    #custom-figure-6 .img-wrapper {
      position: relative;
      overflow: hidden;
      border: 2px dashed #666;
      width: 400px;
      height: 200px;
      background: #f5f5f5;
    }
    #custom-figure-6 .img-title {
      font-weight: bold;
      font-size: 14px;
      margin-bottom: 5px;
      text-align: center;
      width: 100%;
      color: #444;
    }
    #custom-figure-6 img {
      width: 100%;
      height: 100%;
      object-fit: contain;
      transition: transform 0.15s ease;
      transform-origin: center center;
      cursor: zoom-in;
    }
    #custom-figure-6 #zoomButtons2 {
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
        <img id="imgEq2" src="../images/icecream/png/tomo_038_eq/FT.png">
      </div>
    </div>
    <div class="img-column">
      <div class="img-title">DeepDeWedge</div>
      <div class="img-wrapper">
        <img id="imgDdw2" src="../images/icecream/png/tomo_038_ddw/FT.png">
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
      const container = document.querySelector('#custom-figure-6');
      const imgEq = container.querySelector('#imgEq2');
      const imgDdw = container.querySelector('#imgDdw2');
      const zoomInBtn = container.querySelector('#zoomIn2');
      const zoomOutBtn = container.querySelector('#zoomOut2');
      const resetZoomBtn = container.querySelector('#resetZoom2');

      let zoomLevel = 1.0;
      let originX = 50, originY = 50;

      function applyZoom() {
        [imgEq, imgDdw].forEach(img => {
          img.style.transformOrigin = `${originX}% ${originY}%`;
          img.style.transform = `scale(${zoomLevel})`;
        });
      }

      function handleMouseMove(e, wrapper) {
        const rect = wrapper.getBoundingClientRect();
        originX = ((e.clientX - rect.left) / rect.width) * 100;
        originY = ((e.clientY - rect.top) / rect.height) * 100;
      }

      function handleWheel(e) {
        e.preventDefault();
        zoomLevel *= e.deltaY < 0 ? 1.1 : 0.9;
        zoomLevel = Math.min(Math.max(zoomLevel, 1), 15);
        applyZoom();
      }

      container.querySelectorAll('.img-wrapper').forEach(wrapper => {
        wrapper.addEventListener('mousemove', (e) => handleMouseMove(e, wrapper));
        wrapper.addEventListener('wheel', handleWheel, { passive: false });
      });

      zoomInBtn.addEventListener('click', () => { originX = originY = 50; zoomLevel *= 1.25; applyZoom(); });
      zoomOutBtn.addEventListener('click', () => { originX = originY = 50; zoomLevel /= 1.25; applyZoom(); });
      resetZoomBtn.addEventListener('click', () => { zoomLevel = 1; originX = originY = 50; applyZoom(); });

      applyZoom();
    })();
  </script>
</div>