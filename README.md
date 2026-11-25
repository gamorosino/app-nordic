# app-nordic

<!-- brainlife-app:begin (generated from the App manifest; edit the manifest, not this block) -->

> **Denoises BOLD fMRI from magnitude and phase data with NORDIC (locally low-rank PCA) using the NORDIC-python translation, and outputs the denoised magnitude BOLD.**

Runs run_nordic.py from NORDIC-python, which estimates g-factor noise maps with an MPPCA pass and applies locally low-rank denoising. Use it on raw complex-valued BOLD before other preprocessing. Needs matching magnitude and phase series. NORDIC is licensed for non-profit research and educational use only.

| | |
|---|---|
| 📥 **Inputs** | `neuro/func/task` ×2 |
| 📤 **Outputs** | `neuro/func/task` |
| 🐳 **Container** | `gamorosino/app-nordic:1.0` |
| ⚙️ **Resources** | 32 GB memory · 4 h walltime |
| 🔗 **Run it** | [doi.org/10.25663/brainlife.app.982](https://doi.org/10.25663/brainlife.app.982) |

#### 📥 Inputs

| Input | Datatype | Required | Description |
|---|---|---|---|
| `mag` | `neuro/func/task` | yes | Magnitude BOLD time series. |
| `phase` | `neuro/func/task` (phase) | yes | Phase BOLD time series matching the magnitude. |

#### 📤 Outputs

| Output | Datatype | Description |
|---|---|---|
| `denoised` | `neuro/func/task` | NORDIC-denoised BOLD (magnitude). |

<details>
<summary><b>⚙️ Parameters</b> (2)</summary>

| Parameter | Type | Default | Description |
|---|---|---|---|
| `temporal_phase` | integer | `1` | Temporal phase correction mode (see upstream docs). |
| `phase_filter_width` | integer | `10` | Phase filter width (see upstream docs). |

</details>

<!-- brainlife-app:end -->

Brainlife.io app wrapping **NORDIC** (NOise reduction with DIstribution Corrected PCA) denoising, using the Python translation [NORDIC-python](https://github.com/JimJam07/NORDIC-python) of the original MATLAB [NORDIC_Raw](https://github.com/SteenMoeller/NORDIC_Raw).

**For documentation, parameters and method details, always refer to the original repository: https://github.com/JimJam07/NORDIC-python**

- Inputs: magnitude and phase BOLD (`neuro/func/task`; phase tagged `phase`)
- Output: denoised magnitude BOLD (`neuro/func/task`, tag `nordic`)
- Container: `docker://gamorosino/app-nordic:1.0` (to be built)

**License:** see `LICENSE`. NORDIC is copyrighted by the Regents of the University of Minnesota (US 10,768,260), licensed for educational and research use by non-profit institutions and US government agencies only; contact umotc@umn.edu for other uses.

---
Upstream README follows.

# NORDIC

## Overview
NORDIC is a locally low-rank denoising algorithm. It uses g-factor maps estimated from the data by running an initial MPPCA pass on a temporal subset of the images to measure the spatially varying noise variance.

This repository is the Python translation of the original MATLAB pipeline - [NORDIC](https://github.com/SteenMoeller/NORDIC_Raw)

## Installation Guide

Clone this repository and set up a Python virtual environment to keep dependencies isolated. Once your environment is active, install the required packages.

```bash
# 1. Clone the repository
git clone https://github.com/JimJam07/NORDIC-python.git
cd NORDIC-python

# 2. Create and activate a virtual environment (recommended)
python -m venv venv
source venv/bin/activate  # On Windows use: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt
```

## Usage Guide

The pipeline is primarily driven through `nordic.py`, which houses the core Nordic processing class.

To run the denoising pipeline, initialize the Nordic class with 3 parameters
1. The file path to the magnitude NIfTI data.
2. The file path to the phase NIfTI data.
3. A dictionary of custom configuration arguments (`Args`).

You can use the `main.py` file as a reference file to run the `Nordic.py`

### `Args`
You must provide a custom `Args` dictionary, and it is strictly required to include the `FN_OUT` key, which defines the base filename for your output files.

All other configurable parameters—such as patch overlap, temporal phase filtering methods, and MPPCA toggles—inherit their default values from the `base_nordic` class located in `base_class.py`. You only need to include parameters in your custom Args dictionary if you want to override these defaults.

## Licensing
 PLEASE NOTE BEFORE DOWNLOADING: THIS SOFTWARE HAS BEEN LICENSED TO NOUS IMAGING, INC. ON A COMMERCIAL NON-EXCLUSIVE BASIS.  
 IF YOU DOWNLOAD THIS SOFTWARE, NOUS WILL HAVE ACCESS TO YOUR NAME, EMAIL ADDRESS, AND OTHER INFORMATION WHICH YOU PROVIDE TO GITHUB AND NOUS MAY CONTACT YOU REGARDING THEIR PRODUCTS AND SERVICES



 
## Copyright and License information

© 2021 Regents of the University of Minnesota

NORDIC and NIFTI_NORDIC is copyrighted by Regents of the University of Minnesota and covered by US 10,768,260. Regents of the University of Minnesota will license the use of NORDIC and NIFTI_NORDIC solely for educational and research purposes by non-profit institutions and US government agencies only. For other proposed uses, contact umotc@umn.edu. The software may not be sold or redistributed without prior approval. One may make copies of the software for their use provided that the copies, are not sold or distributed, are used under the same terms and conditions. As unestablished research software, this code is provided on an "as is'' basis without warranty of any kind, either expressed or implied. The downloading, or executing any part of this software constitutes an implicit agreement to these terms. These terms and conditions are subject to change at any time without prior notice.

---
