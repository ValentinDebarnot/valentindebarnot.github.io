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
  <a href="../cryolithe.html" class="btn">← Previous</a>
  <a href="../cryolithe.html" class="btn">Home</a>
  <a href="./examples.html" class="btn">Next →</a>
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

<h1 id="practical">How to use Icecream</h1>
  - [Installation](#instal)
  - [Generate two tomograms with one tilt-series](#angle-split)
  - [Train Icecream on your data](#train)
  - [Inference with Icecream](#test)
  - [Pre-training: how to avoid training for every new data](#pre-train)

* * *

<h2 id="installation">Rapid installation, usage and reconstruction</h2>

<p>
The first goal of CryoLithe is to be ultra-fast. Thus, we have made the installation and usage as simple as possible.
For custom usage, please see the details on the <a href="https://github.com/swing-research/CryoLithe" target="_blank">Github page</a>. 
</p>

**Installation**
```bash
conda create -n CryoLithe python=3.9
conda activate CryoLithe
pip3 install torch torchvision torchaudio
pip install git+https://github.com:swing-research/CryoLithe.git
```

**Download the trained models**
```bash
cryolithe download
```

**Reconstruction**
```bash
cryolithe reconstruct \ 
    --proj-file path_projections \
    --angle-file path_angles \
    --save-dir ./CryoLithe_results/ \
    --save-name output_volume.mrc \
    --device 0 \
    --n3 256 \ 
    --batch-size 100000  # Depends on the memory of your GPU
```
where `path_projections` and `path_angles` are the paths to the projection (mrc or st file) and angle files (tlt or txt) of your tilt-series.



<h2 id="allign">How to obtained aligned tilt-series</h2>
<strong>CryoLithe</strong> requires aligned tilt-series to perform reconstruction. Raw tilt-series come unaligned, and it can be challenging to perform such alignment in general. We provide a simple approach relying on [AreTomo 3](https://github.com/czimaginginstitute/AreTomo3){:target="_blank"}. This method should provide decent results for most common dataset. 
We assume that AreTomo has been installed, see the [dedicated webpage](https://github.com/czimaginginstitute/AreTomo3){:target="_blank"} if needed.
We also assume that Imod is available, see the [dedicated webpage](https://bio3d.colorado.edu/imod/){:target="_blank"}.


Get data to test on. We take the first tilt-series from [EMPIAR 11830](https://www.ebi.ac.uk/empiar/EMPIAR-11830/){:target="_blank"}, but feel free to use your own data. 
```bash
mkdir data
wget https://ftp.ebi.ac.uk/empiar/world_availability/11830/data/chlamy_visual_proteomics/01082023_BrnoKrios_Arctis_WebUI_Position_1/01082023_BrnoKrios_Arctis_WebUI_Position_1.st -P ./data/
wget https://ftp.ebi.ac.uk/empiar/world_availability/11830/data/chlamy_visual_proteomics/01082023_BrnoKrios_Arctis_WebUI_Position_1/01082023_BrnoKrios_Arctis_WebUI_Position_1.rawtlt -P ./data/
```


Align using AreTomo 3
```bash
mkdir data/AreTomo
AreTomo3 -InPrefix data/01082023_BrnoKrios_Arctis_WebUI_Position_1 -InSuffix st -OutDir ./data/AreTomo/ -Cmd 0 -VolZ 0 -AlignZ 256 -AtBin 4 -Gpu 0 -CorrCTF 1 -PixSize 1.9 -Kv 300 -Cs 2.7 -Serial 1  -DarkTol 0  -TiltCor 1 -FlipVol 0 -OutImod 3
```

Align back. This requires the [`cryoet-alignment` package](https://pypi.org/project/cryoet-alignment/){:target="_blank"} that can be installed using pip.
```bash
pip install cryoet-alignment
cryolithe AreTomoToImod --aln-path ./data/AreTomo/01082023_BrnoKrios_Arctis_WebUI_Position_1.aln --output-path ./data/01082023_BrnoKrios_Arctis_WebUI_Position_1
newstack -input data/01082023_BrnoKrios_Arctis_WebUI_Position_1.st -output data/01082023_BrnoKrios_Arctis_WebUI_Position_1_aligned.st -xf ./data/01082023_BrnoKrios_Arctis_WebUI_Position_1.xf -bin 4
```

Finally, CryoLithe's reconstruction can be obtained:
```bash
cryolithe reconstruct --proj-file data/01082023_BrnoKrios_Arctis_WebUI_Position_1_aligned.st --angle-file data/01082023_BrnoKrios_Arctis_WebUI_Position_1.rawtlt --save-dir ./data/ --save-name 01082023_BrnoKrios_Arctis_WebUI_Position_1_CryoLithe.mrc  --device 0 --n3 256 --batch-size 100000  --pixel 0# Depends on the memory of your GPU
```


* * * 
<h2 id="pre-train">Re-train on your own data</h2>
<p>
Precise procedure cooming soon! 
</p>


* * * 
<h2 id="yaml-params">Parameters of the config file</h2>
The default config file can be found [here](https://github.com/swing-research/CryoLithe/blob/main/src/CryoLithe/defaults.yaml). The different possible parameters are reported below with a brief description.

|    | | **data** |
| Key        | Default           | Description                                                                                                            |
| ---------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `model_dir`    | `null`              | Path to trained model directory.                                      |
| `proj_file`    | `null`              | Path to projections .mrc/.mrcs file.                                               |
| `angle_file` | `null` | Path to tilt-angle file.                                                                 |
| `save_dir`     | `null`            | Directory to write reconstruction.  |
| `save_name` | `null`            | Output volume filename.                                                                         |

<div style="height: 50px;"></div>

|    | | **train_params** |
| Key                             | Default    | Description                                                                                 |
| ------------------------------- | ---------- | ------------------------------------------------------------------------------------------- |
| `patch_scale`                        | `1`        | Override model patch scale. The only parameter that will influence the reconstruction quality. Default is 1. Greater than one means that effective field of the patch increases, and lower than one means that it decreases.                        |
| `device`                        | `0`        | GPU number or device name.                       |
| `downsample_projections`                | `False`    | Whether to downsample the input projections for reconstruction. If true, the projections will be downsampled by the specified factor.                                                       |
| `downsample_factor`                    | `0.25`       | Factor by which to downsample the input projections if downsample_projections is true. |
| `anti_alias`                         | `true`      |Whether to apply an anti-aliasing filter to the projections before downsampling. This can help reduce artifacts in the reconstruction when downsampling.             |
| `N3`                    | `256`        | Volume size along z-axis, after downsampling.                              |
| `batch_size`                          | `100000`       | Batch size for point inference. Reduce if memory issue.                                                           |
| `num_workers`                       | `0`    | Number of worker processes for data loading. Set to 0 to use the main process.                                    |
| `model_variant`                   | `cryolithe`    | Use cryolithe-pixel (longer, slighlty better quality) or cryolithe (faster)..                          |

<div style="height: 50px;"></div>



<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="../cryolithe.html" class="btn">← Previous</a>
  <a href="../cryolithe.html" class="btn">Home</a>
  <a href="./examples.html" class="btn">Next →</a>
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