<!-- ====================== FIGURE 11 ====================== -->
<div id="custom-figure-11">
  <style>
    #custom-figure-11 .viewer {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 5px;
      justify-items: center;
      align-items: center;
    }
    #custom-figure-11 .img-wrapper {
      position: relative;
      overflow: hidden;
      border: 1px solid #ccc;
      width: 400px;
      height: 400px;
      background: #fff;
    }
    #custom-figure-11 .img-title {
      font-weight: bold;
      font-size: 16px;
      margin-bottom: 0px;
      text-align: center;
      width: 100%;
    }
    #custom-figure-11 img {
      width: 100%;
      height: 100%;
      object-fit: contain;
      transition: transform 0.15s ease;
      transform-origin: center center;
      cursor: crosshair;
    }
    #custom-figure-11 #controls {
      margin-top: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 10px;
    }
    #custom-figure-11 #zoomButtons1 {
      display: flex;
      gap: 10px;
      justify-content: center;
      margin-top: 10px;
    }
  </style>
  <div class="viewer">
    <div class="img-column">
      <div class="img-title">❄️ CryoLithe</div>
      <div class="img-wrapper">
        <img id="img1" src="../images/cryolithe/png/figure_6/cryolithe_noctf/slice_00035.jpg">
      </div>
    </div>
    <div class="img-column">
      <div class="img-title">CTF correction + ❄️ CryoLithe</div>
      <div class="img-wrapper">
        <img id="img1_ctf" src="../images/cryolithe/png/figure_6/cryolithe_ctf/slice_00035.jpg">
      </div>
    </div>
    <div class="img-column">
      <div class="img-title">IsoNet</div>
      <div class="img-wrapper">
        <img id="img2" src="../images/cryolithe/png/figure_6/vol_crc_isonet_noctf/slice_00035.jpg">
      </div>
    </div>
    <div class="img-column">
      <div class="img-title">CTF correction + IsoNet</div>
      <div class="img-wrapper">
        <img id="img2_ctf" src="../images/cryolithe/png/figure_6/vol_crc_isonet_ctf/slice_00035.jpg">
      </div>
    </div>
    <div class="img-column">
      <div class="img-title">FBP </div>
      <div class="img-wrapper">
        <img id="img3" src="../images/cryolithe/png/figure_6/vol_fbp_noCTF/slice_00035.jpg">
      </div>
    </div>
    <div class="img-column">
      <div class="img-title">CTF correction + FBP </div>
      <div class="img-wrapper">
        <img id="img3_ctf" src="../images/cryolithe/png/figure_6/vol_fbp_CTF/slice_00035.jpg">
      </div>
    </div>
  </div>

  <div id="controls">
    <input type="range" id="sliceSlider11" min="0" max="77" step="1" value="35">
    <span id="sliceValue11">Slice: 35</span>
  </div>
  <div id="zoomButtons1">
    <button id="zoomIn1">🔍 Zoom In</button>
    <button id="zoomOut1">➖ Zoom Out</button>
    <button id="resetZoom1">↩️ Reset</button>
  </div>

  <script>
    (function() {
      const container = document.querySelector('#custom-figure-11');
      const img1 = container.querySelector('#img1');
      const img2 = container.querySelector('#img2');
      const img3 = container.querySelector('#img3');
      const img1_ctf = container.querySelector('#img1_ctf');
      const img2_ctf = container.querySelector('#img2_ctf');
      const img3_ctf = container.querySelector('#img3_ctf');
      const sliceSlider11 = document.getElementById('sliceSlider11');
      const sliceValue11 = document.getElementById('sliceValue11');
      const zoomInBtn = container.querySelector('#zoomIn1');
      const zoomOutBtn = container.querySelector('#zoomOut1');
      const resetZoomBtn = container.querySelector('#resetZoom1');

      let zoomLevel = 1.0;
      let originX = 50, originY = 50;

      // Update slice images
      function updateImages11() {
        const index = parseInt(sliceSlider11.value, 10);
        const padded = String(index).padStart(5, '0');
        sliceValue11.textContent = `Slice: ${index}`;
        img1.src = `../images/cryolithe/png/figure_6/cryolithe_noctf/slice_${padded}.jpg`;
        img2.src = `../images/cryolithe/png/figure_6/vol_crc_isonet_noctf/slice_${padded}.jpg`;
        img3.src = `../images/cryolithe/png/figure_6/vol_fbp_noCTF/slice_${padded}.jpg`;
        img1_ctf.src = `../images/cryolithe/png/figure_6/cryolithe_ctf/slice_${padded}.jpg`;
        img2_ctf.src = `../images/cryolithe/png/figure_6/vol_crc_isonet_ctf/slice_${padded}.jpg`;
        img3_ctf.src = `../images/cryolithe/png/figure_6/vol_fbp_CTF/slice_${padded}.jpg`;
      }

      function applyZoom() {
        [img1, img2, img3, img1_ctf, img2_ctf, img3_ctf].forEach(img => {
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
      sliceSlider11.addEventListener('input', updateImages11);

      zoomInBtn.addEventListener('click', () => { zoomLevel *= 1.25; applyZoom(); });
      zoomOutBtn.addEventListener('click', () => { zoomLevel /= 1.25; applyZoom(); });
      resetZoomBtn.addEventListener('click', () => { zoomLevel = 1; originX = originY = 50; applyZoom(); });

      applyZoom();
    })();
  </script>
</div>

<div style="height: 50px;"></div>

