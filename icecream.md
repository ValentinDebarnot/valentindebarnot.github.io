---
layout: default
title: 🍦 Icecream
description: 
show_downloads: false
google_analytics:
theme: jekyll-theme-cayman
banner: "./assets/images/band_icecream.png"
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
<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="./icecream/how_to_use.html" class="btn">Next →</a>
</div>

<style>
h1.project-name { color: rgba(139, 125, 199, 1) !important; }
h2.project-tagline { color: rgba(139, 125, 199, 1) !important; }
header a.btn { color: rgba(139, 125, 199, 1) !important; 
border-color: rgba(139, 125, 199, 1) !important; 
background-color: rgba(138, 125, 199, 0.16) !important; }
</style>


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
<p style="text-align: center; font-size: 35px;">
High-Fidelity Equivariant Cryo-Electron Tomography
</p>
<p style="text-align: center; font-size: 18px;">
  <a href="https://scholar.google.fr/citations?user=5cLOfZQAAAAJ&hl=en&oi=ao" target="_blank">
    Vinith Kishore<sup>1</sup>
  </a>,
  <a href="https://sites.google.com/view/debarnot/home" target="_blank">
    Valentin Debarnot<sup>2</sup>
  </a>,
  <a href="https://scholar.google.com/citations?user=otSrWcQAAAAJ&hl=en&oi=ao" target="_blank">
    Ricardo D. Righetto<sup>3</sup>
  </a>,
  <a href="https://www.cellarchlab.com/" target="_blank">
    Benjamin D. Engel<sup>3</sup>
  </a>,
  <a href="hhttps://sada.dmi.unibas.ch/en/people/head-of-sada/ivan-dokmanic" target="_blank">
    Ivan Dokmanić<sup>1</sup>
  </a>.
</p>
<p style="text-align: center; font-size: 18px;">
  <sup>1</sup> Department of Mathematics and Computer Science, University of Basel, <br>
  <sup>2</sup> INSA‐Lyon, Universite Claude Bernard Lyon 1, CNRS, Inserm, CREATIS UMR 5220, U1294, <br>
  <sup>3</sup> Biozentrum, University of Basel.
</p>

* * * 
  
<!-- # Post-processing with Icecream -->
Icecream is a self-supervised framework for cryo-ET (and standard ET) reconstruction that integrates equivariance principles from modern imaging theory into a deep-learning architecture.
This webpage aims at providing reconstruction example and documentation on how to use the code.

# Table of Contents
- [What to expect with Icecream?](#compare)
- [How to use Icecream](./icecream/how_to_use.html)
  - [Installation](./icecream/how_to_use.html#installation)
  - [Generate two tomograms with one tilt-series](./icecream/how_to_use.html#angle-split)
  - [Train Icecream on your data](./icecream/how_to_use.html#train)
  - [Inference with Icecream](./icecream/how_to_use.html#test)
  - [Pre-training: how to avoid training for every new data](./icecream/how_to_use.html#pre-train)
- [Examples of reconstructions](./icecream/examples.html)
  - [Chlamydomonas reinhardtii - tomogram 9](./icecream/examples.html#mosaic1)
  - [Chlamydomonas reinhardtii - tomogram 2](./icecream/examples.html#mosaic2)
  - [Thylakoid membranes](./icecream/examples.html#mosaic3)
  - [HEK293T cells](./icecream/examples.html#mosaic4)
  - [S. cerevisiae](./icecream/examples.html#mosaic5)
  - [T. kivui cells](./icecream/examples.html#mosaic6)
- [Dose vs angle splitting](./icecream/split.html)
- [How to cite](./icecream/reference.html)

* * * 

<h1 id="compare">What to expect with Icecream? </h1>
We illustrate Icecream on our favorite tomogram: T. kivui, an anaerobic bacterium that efficiently fixates carbon.
The interest of T. kivui is that deep learning methods are known to improve a lot compared to standard filtered back-projection. 

In the following figures, we reported Icecream along with:
- [DeepDeWedge](https://www.nature.com/articles/s41467-024-51438-y), conceptually the closest to Icecream. Both implement similar equivariant losses, with the main difference that Icecream treats symmetry in a way consistent with the recent [equivariant imaging framework](https://openaccess.thecvf.com/content/ICCV2021/html/Chen_Equivariant_Imaging_Learning_Beyond_the_Range_Space_ICCV_2021_paper.html). This amounts to applying the trained network twice at inference.
- [CryoLithe](https://arxiv.org/abs/2501.15246), a supervised learning method. The strength of CryoLithe is that **reconstructing such a volume takes 4 minutes**, against 12 hours for Icecream and 24 hours for DeepDeWedge. A strong or not so strong feature is that CryoLithe doesn't require any parameters, only the aligned tilt-series.
- Filtered back-projection, or weighted back projection. This was performed using Imod and the <code>tilt</code> function. 

**About technical details.**
This is *tomo2_L1G1* from [EMPIAR-11058](https://www.ebi.ac.uk/empiar/EMPIAR-11058/).
The pixel size is 14.08Å and the tomogram contains 928 x 928 x 464 pixels. Two tomograms were obtained by spliting the tilt angles.


{% include icecream/figure_tkivui.md %}


<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="./icecream/how_to_use.html" class="btn">Next →</a>
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