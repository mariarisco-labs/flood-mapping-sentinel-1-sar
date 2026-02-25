# AI for flood detection

As a result of climate change, extreme hydrometeorological events are becoming increasingly frequent. Flood rapid mapping products play an important role in informing flood emergency response and management. These maps are generated quickly from remote sensing data during or after an event to show the extent of the flooding. They provide important information for emergency response and damage assessment. 

# Major Datasets Used

Multi-source geospatial datasets provided by the [Institute of electrical and Electronics Engineers](https://www.ieee.org/) withing the framework of the 2024 [IEEE GRSS Data Fusion Contest - Flood Rapid Mapping](https://www.grss-ieee.org/community/technical-committees/2024-ieee-grss-data-fusion-contest/). 

Public access to data: [IEEE DataPort](https://ieee-dataport.org/competitions/2024-ieee-grss-data-fusion-contest-flood-rapid-mapping)

Dataset structure: **1061 images** with **6 bands** (`.tif`) + **1061 binary masks** with **1 band** (`.png`):  
- `0` — No Water  
- `1` — Water (positive class)

![Data structure](src/img/Data_structure.png)

- **Copernicus/Sentinel (10 m):** C-band synthetic aperture radar (SAR),  (VV & VH backscattering)
- **Copernicus DEM (30 m):** Digital Surface Model (DSM) representing the Earth’s surface including buildings, infrastructure and vegetation  
  https://dataspace-copernicus-eu.translate.goog/explore-data/data-collections/copernicus-contributing-missions/collections-description/COP-DEM?_x_tr_sl=en&_x_tr_tl=es&_x_tr_hl=es&_x_tr_pto=sc
- **MERIT DEM (90 m):** Digital terrain model widely used in the hydrology community  
  https://hydro.iis.u-tokyo.ac.jp/~yamadai/MERIT_DEM/
- **Global Surface Water Occurrence:** Location and temporal distribution of water surfaces globally over the past 32 years, including extent/change statistics  
  https://global-surface-water.appspot.com/
- **ESA WorldCover (10 m):** Global land cover product  
  https://esa-worldcover.org/en/data-access
- **Labels (training):** Flood extent labeled by the Copernicus Emergency Management Service

# Technical solution (workflows)

![Workflow1](https://github.com/mariarisco/ML_SAR_floods/blob/main/src/img/Workflow1.png)

![Workflow2](https://github.com/mariarisco/ML_SAR_floods/blob/main/src/img/Workflow2.png)

# Reproducibility (quickstart)

1) Create and activate the conda environment:

```bash
conda env create -f environment.yml
conda activate gpu_env
```

2) Open the final notebooks:
- src/results_notebook/Floods_model_Bagging&Boosting.ipynb
- src/results_notebook/Floods_model_MLP.ipynb

# Final notebooks

The definitive results and model development are documented in:

- `src/results_notebook/Floods_model_Bagging&Boosting.ipynb`
- `src/results_notebook/Floods_model_MLP.ipynb`

# Data

This repository includes a lightweight sample under `src/data_sample/`.

To reproduce results with the full dataset:
1. Download the data from [IEEE DataPort](https://ieee-dataport.org/competitions/2024-ieee-grss-data-fusion-contest-flood-rapid-mapping)
2. Place it locally under `src/data/` (recommended)
3. Keep `src/data/` out of git (via `.gitignore`)

# Results (v1)

- Two modelling approaches are provided: **Bagging/Boosting** and an **MLP** baseline.
- Workflows cover multi-source feature stacking, model training, and pixel-wise flood mask prediction.
- Figures (workflow, dataset structure, and outputs) are stored under `src/img/`.

# Repo structure

```text
flood-mapping-sentinel-1-sar/
├── src/
│   ├── data_sample/         # sample data (lightweight)
│   ├── img/                 # figures (workflow, structure, results)
│   ├── models/              # trained models
│   ├── notebooks/           # draft notebooks
│   ├── results_notebook/    # final notebooks (Bagging/Boosting + MLP)
│   └── utils/               # utility scripts
├── .gitignore
├── environment.yml
└── README.md             # Project documentation and setup instructions
```
