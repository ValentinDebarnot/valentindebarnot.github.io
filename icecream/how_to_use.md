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
  <a href="../icecream.html" class="btn">← Previous</a>
  <a href="../icecream.html" class="btn">Home</a>
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

<h2 id="installation">Installation</h2>
<!-- Latest version is always on github: https://github.com/swing-research/icecream
Safest is to use git to get the latest version.
First installation: use git clone https://github.com/swing-research/icecream + get procedure from github
Update to latest version: git pull in the Icecream repository
It's ready to use.  -->

<p>
The latest version of <strong>Icecream</strong> is always available on GitHub:
<a href="https://github.com/swing-research/icecream" target="_blank">https://github.com/swing-research/icecream</a>.
We recommend using <code>git</code> to clone the repository, ensuring that you can easily update it later.
</p>

<p><strong>First use of Icecream.</strong> </p>
Clone the repository:
<pre><code>git clone https://github.com/swing-research/icecream.git
cd icecream
</code></pre>

<p>Create and activate a Python environment (Python ≥ 3.11 recommended):</p>
<pre><code>conda create -n icecream python=3.11 -y
conda activate icecream
</code></pre>

<p>
Next, install a CUDA-enabled version of PyTorch that matches your system configuration.
For example, for Linux with CUDA 12.8:
</p>
<pre><code>pip install torch --index-url https://download.pytorch.org/whl/cu128
</code></pre>
*Notice that we observed a significant slowdown with PyTorch version 3.9 instead of 3.8. Results of the paper were obtained with version 3.8.*

<p>Install Icecream and its dependencies:</p>
<pre><code>pip install -e .
</code></pre>

<p>Test your installation:</p>
<pre><code>icecream --help
</code></pre>

<p>
You should see Icecream’s main commands listed: <code>train</code> and <code>predict</code>.  
You are now ready to use Icecream.
</p>

<p><strong>Already a user or Icecream.</strong> </p>
Make sure to get the latest version, run the following command in the folder of the project
<pre><code>git pull
</code></pre>

* * *
<h2 id="angle-split">Generate two tomograms with one tilt-series</h2>
Icecream requires two statistically indepdent tomograms as input.
The recommended workflow, similar to [Cryo-CARE](https://ieeexplore.ieee.org/abstract/document/8759519), is to <strong>split the dose</strong> of your tilt-series and reconstruct two independent tomograms.
If that’s not possible, you can instead <strong>split the tilt-series by angle range</strong>.
Icecream provides a dedicated command for this:


<pre><code>icecream split-tilt-series --input path/to/tilt-series.mrc --angles path/to/angles.tlt
</code></pre>

<p>
Alternatively, you can specify the angular range manually using <code>--min-angle</code> and <code>--max-angle</code> (default values are -60 and +60).
The command generates two new tilt-series in the same directory as the original one, named with <code>_split1</code> and <code>_split2</code> suffixes.
</p>

<p>
You can then reconstruct each tomogram using your preferred software.
For instance, with <strong>IMOD</strong>:
</p>

<pre><code>tilt -input /path/to/tilt-series_split1.mrc -output /path/to/tomogram_FBP_split1.mrc \
     -TILTFILE /path/to/angles_angles1.tlt -THICKNESS 512 -UseGPU 0
</code></pre>

<p>
After reconstruction, you will have two tomograms ready to be used for Icecream training.
</p>

* * * 
<h2 id="train">Train Icecream on your data</h2>
<!-- Follow what is describe on the github of the project -->

<p>
Training Icecream can be done either via a configuration file or by specifying parameters directly from the command line.
During training, Icecream automatically reconstructs a volume after each training cycle.
</p>

<h3 id="train_cli">The simplest: command line interface</h3>

<p>You can train providing minimal information with the command-line arguments:</p>
<pre><code>icecream train \
  --tomo0 /path/to/tomogram_0.mrc \
  --tomo1 /path/to/tomogram_1.mrc \
  --angles /path/to/angles.tlt \
  --save-dir /path/to/save/dir \
  --iterations 10000 \
  --batch_size 8
</code></pre>

<p>
To see the full list of available training options, run:
</p>

<pre><code>icecream train --help
</code></pre>


<p>
This command trains Icecream using two tomograms (<code>tomogram_0</code> and <code>tomogram_1</code>).
Outputs, including reconstructions, configuration (<code>config.json</code>), and model checkpoints, are stored in <code>/path/to/save/dir</code>.
The batch size is set to 8 but should be adjusted depending on the GPU memory available.
</p>

<h3 id="train_config">More options: config file</h3>

<p>The command-line interface provides only few parameters. To get access to a wide range of additional parameters for training control and customization, you need to use config files.
We recommand copying the default config file that is located in 'src/icecream/defaults.yaml' of the icecream folder and name it after you experiment. Run Icecream can be done simply with:
</p>

<pre><code>icecream train --config /path/to/config/file.yaml
</code></pre>

Please refere to [the dedicated paragraph](#yaml-params) to know more about the role of each parameter.

* * * 
<h2 id="test">Inference with Icecream</h2>
<!-- Follow what is describe on the github of the project -->
<p>
After training, Icecream can perform inference (reconstruction) using a trained model checkpoint.

<h3 id="predict-cli">Inference with command line interface</h3>
This can be done with the <code>predict</code> command:
</p>

<pre><code>icecream predict \
  --tomo0 /path/to/tomogram_0.mrc \
  --tomo1 /path/to/tomogram_1.mrc \
  --angles /path/to/angles.tlt \
  --save_dir /path/to/output_dir \
  --iter_load -1
</code></pre>

<p>
If <code>--iter_load</code> is not provided or set to -1, Icecream will use the latest available checkpoint.

<h3 id="predict-config">Config file</h3>
You may also use a YAML configuration file instead of JSON.
<pre><code>icecream predict \
  --config /path/to/config/file.yaml 
</code></pre>
</p>

* * * 
<h2 id="pre-train">Pre-training: how to avoid training for every new data</h2>
<p>
Precise procedure cooming soon! 
</p>

* * *

<h2 id="yaml-params">Parameters of the config file</h2>
The default config file can be found [here](https://github.com/swing-research/icecream/blob/main/src/icecream/defaults.yaml). The different possible parameters are reported below with a brief description.

|    | | **data** |
| Key        | Default           | Description                                                                                                            |
| ---------- | ----------------- | ---------------------------------------------------------------------------------------------------------------------- |
| `tomo0`    | `[]`              | Path(s) to the first set of tomograms. Must be ordered consistently with `tomo1`.                                      |
| `tomo1`    | `[]`              | Path(s) to the second set of tomograms. Must match the order of `tomo0`.                                               |
| `save_dir` | `"runs/default/"` | Path where results and training information are saved.                                                                 |
| `mask`     | `null`            | Path to mask on the spatial domain, e.g. using slabify.  |
| `tilt_max` | `60.0`            | Maximum tilt angle in degrees. Default is +60.                                                                         |
| `tilt_min` | `-60.0`           | Minimum tilt angle in degrees. Default is -60.                                                                         |
| `angles`   | `null`            | Path to the tilt-angle file (`.txt` or `.tlt`).                                                                        |

<div style="height: 50px;"></div>

|    | | **train_params** |
| Key                             | Default    | Description                                                                                 |
| ------------------------------- | ---------- | ------------------------------------------------------------------------------------------- |
| `device`                        | `0`        | GPU number or device name. Only a single GPU is supported currently.                        |
| `crop_size`                     | `72`       | Size of cubic sub-tomograms used for training.                                              |
| `iterations`                    | `50000`    | Total number of training iterations.                                                        |
| `eq_weight`                         | `2.0`      |Equivariant regularization weight. Increase to get more regularization.             |
| `batch_size`                    | `8`        | Training batch size. Reduce if you run into GPU memory issues.                              |
| `seed`                          | `42`       | Random seed for reproducibility.                                                            |
| `compile`                       | `false`    | Use `torch.compile` to speed up training (experimental).                                    |
| `use_fourier`                   | `false`    | Compute loss in Fourier space if true; in spatial domain if false.                          |
| `use_spherical_support`         | `true`     | Enforce Fourier-space support within a spherical region matching subtomogram size.          |
| `wedge_low_support`             | `0`        | Percentage of low frequencies to *keep* in the input model (not part of the missing wedge). |
| `ref_wedge_support`             | `1`        | Percentage of low frequencies to *keep* in the reference tomogram.                          |
| `wedge_double_size`             | `true`     | Define the missing wedge over a doubled subtomogram size if true.                           |
| `save_n_iterations`             | `5000`     | Save model weights every N iterations.                                                      |
| `save_tomo_n_iterations`        | `0`        | Reconstruct tomogram every N iterations (0 disables reconstruction during training).        |
| `compute_avg_loss_n_iterations` | `1000`     | Compute and log average loss every N iterations.                                            |
| `use_flips`                     | `true`     | Include flip operators in the equivariance loss.                                            |
| `normalize_crops`               | `false`    | Normalize each subtomogram before feeding it to the network.                                |
| `use_inp_wedge`                 | `false`    | Use reconstructed wedge in the equivariance loss (false in the paper’s setting).            |
| `learning_rate`                 | `1e-4`     | Learning rate for the optimizer. Lower it if training becomes unstable.                     |
| `use_mixed_precision`           | `true`     | Use mixed precision (AMP) to accelerate training with minor numerical loss.                 |
| `no_window`                     | `false`    | If true, use the entire tomogram for training; otherwise, only the central region.          |
| `view_as_real`                  | `true`     | Discard imaginary part after inverse Fourier transform if true.                             |
| `upsample_volume`               | `false`    | Upsample the reconstructed volume by a factor of 2.                                         |
| `eq_use_direct`                 | `false`    | If false, the rotated wedge is masked out of the loss computation.                          |
| `min_distance`                  | `0.5`      | Minimum relative difference between rotated and unrotated wedges.                           |
| `window_type`                   | `"boxcar"` | Shape of the cropping window.                                                               |
| `load_device`                   | `false`    | Load all the full tomograms on the device. Will be faster but requires more memory.                                                              |
| `num_workers`                   | `8` |       Number of workers available for the dataloader.                                                               |
| `pretrain_params.use_pretrain`  | `false`    | If true, load pretrained model weights before training.                                     |
| `pretrain_params.model_path`    | `None`     | Path to pretrained model weights file.                                                      |


<div style="height: 50px;"></div>

| | | **predict_params** |
| Key            | Default | Description                                                                    |
| -------------- | ------- | ------------------------------------------------------------------------------ |
| `save_dir_reconstructions`   | same as data.save_dir     | Path where to save the reconstructions. Default is same as data.save_dir. |
| `batch_size`   | `5`     | Inference batch size. Reduce if memory is limited.                             |
| `stride`       | `36`    | Step size (in voxels) between reconstructed subtomograms. Overlap is averaged. |
| `pre_pad`      | `true`  | Pad input tomogram with zeros before inference.                                |
| `pre_pad_size` | `null`  | Size of zero-padding to apply to the tomogram before inference.                |
| `avg_pool`     | `false` | Apply average pooling to smooth the input tomogram.                            |
| `iter_load`     | `-1` | Iteration of the model to load, -1 is the latest.                            |


<div style="height: 50px;"></div>


| | | **model_params** |
| Key            | Default       | Description                                                                                      |
| -------------- | ------------- | ------------------------------------------------------------------------------------------------ |
| `name`         | `"unet3d_bf"` | Model architecture name. Currently only `"unet3d_bf"` is supported.                              |
| `num_levels`   | `4`           | Number of U-Net levels (depth of the model).                                                     |
| `upsample`     | `"default"`   | Upsampling method used in the U-Net decoder.                                                     |
| `layer_order`  | `"cr"`        | Order of operations inside convolutional blocks (`c` = conv, `r` = ReLU, etc.).                  |
| `use_bias`     | `false`       | Whether to include bias terms in the convolutional layers. Setting to false improves robustness. |
| `padding_mode` | `"zeros"`     | Padding mode for convolutions.                                                                   |
| `pool_type`    | `"max"`       | Pooling operation type used in the U-Net.                                                        |
| `dropout_prob` | `0.1`         | Dropout probability during training (fraction of weights randomly disabled).                     |

<div style="height: 50px;"></div>


| | | **mask_params** |
| Key         | Default | Description                                            |
| ----------- | ------- | ------------------------------------------------------ |
| `use_mask`  | `true`  | Apply the missing wedge mask to the input tomograms.   |
| `mask_frac` | `0.5`   | Fractional threshold applied when generating the mask. |
| `mask_tomo_side` | `5`   |   |
| `mask_tomo_density_perc` | `50`   |   |
| `mask_tomo_std_perc` | `50`   |  |

<div style="height: 50px;"></div>

| | | **debug** |
| Key            | Default | Description                                             |
| -------------- | ------- | ------------------------------------------------------- |
| `use_pretrain` | `false` | If true, load pretrained model weights before training. |
| `model_path`   | `None`  | Path to pretrained model weights file.                  |

<div style="height: 50px;"></div>



<h3>💡 Tips</h3>
<ol>
  <li>
    <strong>Tilt-angle handling:</strong>  
    Icecream only requires the minimum and maximum tilt angles to generate a Fourier mask that accounts for the missing wedge.  
    If no tilt-angle file (<code>.tlt</code>) is available, you can specify the angular range directly using 
    <code>--tilt-min</code> and <code>--tilt-max</code>.  
    The default values are <code>-60</code> and <code>+60</code>.
  </li>

  <li>
    <strong>GPU memory optimization:</strong>  
    GPU memory is often the main bottleneck during training.  
    You can control memory usage with the <code>--batch-size</code> parameter.  
    In general, use the largest batch size that fits in your GPU memory for optimal efficiency.
  </li>

  <li>
    <strong>Equivariance strength (<code>--eq_weight</code>):</strong>  
    The <code>eq_weight</code> parameter determines how strongly the equivariance prior is enforced.  
    Larger values produce stronger smoothing and denoising, while smaller values preserve details closer to the raw tomograms.
  </li>

  <li>
    <strong>Training duration (<code>--iteration</code>):</strong>  
    The <code>iteration</code> parameter sets the total number of training iterations.  
    On a modern GPU, running <code>--iteration 50000</code> typically takes around <strong>6 hours</strong> on our GPU and provides good reconstruction quality.
  </li>
</ol>


<div style="display: flex; justify-content: space-between; margin-top: 2em;">
  <a href="../icecream.html" class="btn">← Previous</a>
  <a href="../icecream.html" class="btn">Home</a>
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