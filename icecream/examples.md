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
  <a href="./how_to_use.html" class="btn">← Previous</a>
  <a href="../icecream.html" class="btn">Home</a>
  <a href="./split.html" class="btn">Next →</a>
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


<h1 id="mosaic">Examples of reconstructions </h1>

  - [Chlamydomonas reinhardtii](#mosaic12)
    - [Tomogram 9](#mosaic1)
    - [Tomogram 2](#mosaic2)
  - [Thylakoid membranes](#mosaic3)
  - [HEK293T cells](#mosaic4)
  - [S. cerevisiae](#mosaic5)
  - [T. kivui cells](#mosaic6)

* * * 


<h2 id="mosaic12">EMPIAR 11830 - Chlamydomonas reinhardtii prepared using cryo-plasmaFIB milling</h2>
The pixel size is 7.84Å and the tomogram contains 1024 x 1024 x 512 pixels. Two tomograms were obtained by spliting the dose.
Below we display both Icecream and DeepDeWedge reconstruction, as well as the stretched amplitude of their Fourier transform on the XZ plane.

*Tips: Use the mouse wheel to zoom in and out at specific locations. The buttons below allows to zoom in and out from the central pixel. The slice slider allows you to chose the z-slice to visualize.*

* * * 
<h3 id="mosaic1">Tomogram 9 from EMPIAR-11830</h3>
{% include icecream/figure_tomo1.md %}

* * *
<h3 id="mosaic2">Tomogram 2 from EMPIAR-11830</h3>
{% include icecream/figure_tomo2.md %}

* * * 
<h2 id="mosaic3">EMPIAR 12612 - Molecular architecture of thylakoid membranes within intact spinach chloroplasts </h2>
The pixel size is 14.08Å and the tomogram contains 928 x 928 x 464 pixels. Two tomograms were obtained by spliting the dose.
This is tomogram 38 from [EMPIAR-12612](https://www.ebi.ac.uk/empiar/EMPIAR-12612/).

{% include icecream/figure_tomo38.md %}


* * * 
<h2 id="mosaic4">EMPIAR 11538 - HEK293T cells </h2>
The pixel size is 4Å and the tomogram contains 1024 x 1024 x 512 pixels. Two tomograms were obtained by spliting the tilt angles.
This is tomogram 1435 from [EMPIAR-11538](https://www.ebi.ac.uk/empiar/EMPIAR-11538/).

{% include icecream/figure_tomo5.md %}

* * * 
<h2 id="mosaic5">EMPIAR 11658 - S. cerevisiae prepared using cryo-plasmaFIB milling </h2>
The pixel size is 7.84Å and the tomogram contains 1024 x 1024 x 512 pixels. Two tomograms were obtained by spliting the tilt angles.
This is tomogram 1 from [EMPIAR-11658](https://www.ebi.ac.uk/empiar/EMPIAR-11658/).

{% include icecream/figure_tomo7.md %}

* * * 
<h2 id="mosaic6">EMPIAR 11058 - T. kivui cells</h2>
The pixel size is 14.08Å and the tomogram contains 928 x 928 x 464 pixels. Two tomograms were obtained by spliting the tilt angles.
This is tomogram 3 from [EMPIAR-11058](https://www.ebi.ac.uk/empiar/EMPIAR-11058/).

{% include icecream/figure_tomo4.md %}



<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="./how_to_use.html" class="btn">← Previous</a>
  <a href="../icecream.html" class="btn">Home</a>
  <a href="./split.html" class="btn">Next →</a>
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