---
layout: default
title: ❄️ CryoLithe
description: CryoLithe - Rapid Cryo-ET Reconstruction via Transform-Localized Deep Learning
show_downloads: false
google_analytics:
theme: jekyll-theme-cayman
banner: "../assets/images/band_cryolithe.png"
github: 
  repository_url: https://github.com/swing-research/CryoLithe
  is_project_page: true
arxiv:
  display: true
  link: https://arxiv.org/abs/2501.15246
  nameJournal: Arxiv
paper:
  display: false
  name: Preprint  
  link: https://arxiv.org/abs/2501.15246
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
  <a href="../cryolithe.html" class="btn">Home</a>
  <a href="./train.html" class="btn">Next →</a>
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

  - [Outside of the training dataset](./cryolithe/examples.html#expl1)
  - [Quantitative analysis](./cryolithe/examples.html#expl2)
  - [Impact of CTF](./cryolithe/examples.html#expl3)

* * * 


<h2 id="expl1"> Outside of the training dataset - EMPIAR 12262 </h2>
CryoLithe is a pre-trained model and yet it produces accurate reconstruction on new unseen dataset. Here, we apply CryoLithe to tilt-series from EMPIAR-12262, which contains non-infected cos-7 cells sampled at 5.525 Å/pixel.
Crowded cellular environments are challenging to reconstruct accurately, a lot of overlapping features are projected onto the
tilt series, and it becomes difficult to disentangle them.

*Tips: Use the mouse wheel to zoom in and out at specific locations. The buttons below allows to zoom in and out from the central pixel. The slice slider allows you to chose the z-slice to visualize.*

{% include cryolithe/figure_ood.md %}


<h2 id="expl2"> Quantitative analysis - EMPIAR 11830 </h2>
We quantitatively validate the performance of CryoLithe on tilt series not seen during training, but obtained from the same dataset (EMPIAR 11830).
These test tilt series were specifically selected to ensure strong performance of the baseline pipeline (Icecream).
CryoLithe achieves this performance with a significant speed advantage, up to 75x faster, and without any parameter tuning.


{% include cryolithe/figure_fsc.md %}


<h2 id="expl3"> Impact of CTF - EMPIAR-11830 </h2>
To evaluate the impact of CTF correction on tomographic reconstruction, we use a tomogram of Chlamydomonas reinhardtii thylakoid membranes obtained from EMPIAR-11830 (test dataset).
CryoLithe performs similarly when given the CTF corrected tilt series and the non-CTF corrected tilt series.

{% include cryolithe/figure_ctf.md %}


<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="./how_to_use.html" class="btn">← Previous</a>
  <a href="../cryolithe.html" class="btn">Home</a>
  <a href="./train.html" class="btn">Next →</a>
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




<!-- [Projects home](../index.html) -->