---
layout: default
title: ❄️ CryoLithe
description: CryoLithe - Rapid Cryo-ET Reconstruction via Transform-Localized Deep Learning
show_downloads: false
google_analytics:
theme: jekyll-theme-cayman
banner: "./assets/images/band_cryolithe.png"
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
<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="./cryolithe/how_to_use.html" class="btn">Next →</a>
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
CryoLithe: Rapid Cryo-ET Reconstruction via Transform-Localized Deep Learning
</p>
<p style="text-align: center; font-size: 18px;">
  <a href="https://scholar.google.fr/citations?user=5cLOfZQAAAAJ&hl=en&oi=ao" target="_blank">
    Vinith Kishore<sup>1</sup>
  </a>,
  <a href="https://sites.google.com/view/debarnot/home" target="_blank">
    Valentin Debarnot<sup>2</sup>
  </a>,
  <a href="https://amirehsan95.github.io/" target="_blank">
    Amir Khorashadizadeh<sup>1</sup>
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
CryoLithe a supervised learning method. The strength of CryoLithe is that **reconstructing such a volume takes 4 minutes**, against 12 hours for Icecream and 24 hours for DeepDeWedge. A strong or not so strong feature is that CryoLithe doesn't require any parameters, only the aligned tilt-series.
This webpage aims at providing reconstruction example and documentation on how to use the code.



# Table of Contents
- [What to expect with CryoLithe?](#compare)
- [How to use CryoLithe](./cryolithe/how_to_use.html)
  - [Installation](./cryolithe/how_to_use.html#installation)
- [Examples of reconstructions](./cryolithe/examples.html)
  - [Outside of the training dataset](./cryolithe/examples.html#expl1)
  - [Quantitative analysis](./cryolithe/examples.html#expl2)
  - [Impact of CTF](./cryolithe/examples.html#expl3)
- [Training CryoLithe on your data](./cryolithe/train.html)
- [How to cite?](./cryolithe/reference.html)

* * * 

<h1 id="compare">What to expect with CryoLithe? </h1>
We illustrate CryoLithe on a tomogram from the test dataset (EMPIAR-11830).

In the following figures, we reported CryoLithe along with:
- [Icecream](https://www.biorxiv.org/content/10.1101/2025.10.17.682746v1), a self-supervised framework for cryo-ET reconstruction that integrates equivariance principles from modern imaging theory into a deep-learning architecture. This is probably state-of-the-art reconstruction in term of quality for most tomograms.

- [Topaz-Denoise](https://www.nature.com/articles/s41467-020-18952-1), a deep learning method for rapid denoising of cryoEM images and cryoET tomogram. 

- Filtered back-projection, or weighted back projection. This was performed using Imod and the <code>tilt</code> function. 

**About technical details.**
The pixel size is 7.84Å and the tomogram contains 1024 x 1024 x 512 pixels.


{% include cryolithe/figure_11058.md %}


<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="./cryolithe/how_to_use.html" class="btn">Next →</a>
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
