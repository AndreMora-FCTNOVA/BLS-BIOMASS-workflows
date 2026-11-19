# Below, Litter & Shrub BIOMASS density mapping combining optical, LiDAR and SAR Earth Observation data

This repository contains **transparent, auditable remote sensing workflows** developed and used in the Iberian Peninsula within the ESA-funded **BLS-BIOMASS** project.

The repository has four distinct parts/steps:

1. **Sensor-specific SNAP preprocessing workflows** (`ALOS-2/`, `S1/`, `S2/`): generalizable Jupyter notebooks that expose processing parameters, XML graph generation, and processing decisions.
2. **Sensor-specific and project-specific preprocessing** : research notebooks and SNAP XML graphs covering additional raster preprocessing
3. **Data Preparation step** - Prepare study areas, feature interpolation.
3. **BLS-BIOMASS project final step** (`BLS-BIOMASS/`): research notebooks for biomass mapping, and uncertainty-related summaries.

The focus is on **inspectable research workflows**, not packaged software or a one-click processing system. 

This workflow produces four biomass pools (Abov**eground, Belowground, Litter and Shrub**) for forest areas in several regions of Portugal and Spain, together with their corresponding uncertainty assessments. The areas in **Portugal** are Mafra, Monsanto, Pombal, Serra Lousã, Sintra-Cascais and Vila Pouca de Aguiar; and in **Spain** are Extremadura, Huesca-Zaragoza, Leon and Teruel. 

For each area the dataset includes individual raster maps in **GeoTIFF** format, with 25m resolution, for all extracted parameters, as well as a **Geopackage** dataset containing the same parameters represented as a point cloud. 

The following **statistical parameters** are included: Coefficient of Variation, Interquartile Range, Kurtosis, Mean, Median, Relative Standard Error, Skewness, and Standard Error.

---
## Repository Structure

```text
bls-biomass-workflows/
├── 0-DataPreparation-GeneralPurpose
│   ├── ALOS-2/         # General-purpose ALOS-2 preprocessing workflows
│   ├── S1-GRD/         # General-purpose Sentinel-1 GRD preprocessing workflows
│   └── S1-SLC/         # General-purpose Sentinel-1 SLC preprocessing workflows
│   └── S2/             # General-purpose Sentinel-2 preprocessing workflows
├── 1-DataPreprocessing/
│   ├── ALOS-2/         # Band splitting and mosaicking
│   ├── S1-GRD/         # Band splitting and mosaicking
│   ├── S1-SLC/         # SNAP GPT processing, XML graphs, band splitting, mosaicking
│   ├── S2/             # Band splitting and mosaicking
│   └── 4_GENERIC_NoData.ipynb
├── 2-DatasetPreparation/
│   ├── 10_Generate_StudyAreas_PointFile.ipynb
│   └── 20_Features_Interpolation.ipynb
└── 3-BiomassMapping/
    └── 30_StudyArea_Mapping_Uncertainty.ipynb
```

---
## Scope and Philosophy

This repository is designed around the following principles:

- **Workflow over package**  
  The notebooks are research workflows meant to be read, inspected, adapted, and extended, rather than a Python package or command-line application.

- **SNAP-based, inspectable preprocessing**
  The general purpose sensor-specific workflows use ESA SNAP operators through `gpt`, with XML graphs generated programmatically where needed. The BLS-BIOMASS material additionally includes supplied SNAP XML graphs and Python/GDAL-based processing steps.

- **Reproducibility without abstraction loss**  
  Processing parameters and decisions remain visible in the notebooks and graph definitions. Reusing the workflows requires appropriate input data and environment configuration.

- **Sensor-specific separation**  
  ALOS-2, Sentinel-1, and Sentinel-2 processing steps remain distinguishable; no unified abstraction is imposed on different satellite products.


---
## Computational Environment and Inputs

The general purpose sensor-specific preprocessing workflows assume ESA SNAP installed and accessible via `gpt`, a Jupyter-capable Python environment with the relevant geospatial libraries (including GDAL), and sufficient disk space for intermediate SNAP products. See the corresponding sensor folders for their processing configurations.

The BLS-BIOMASS project-specific notebooks use combinations of **SNAP GPT, GDAL, NumPy, pandas, GeoPandas, SciPy, Shapely, joblib, and XGBoost**, depending on the notebook. The Sentinel-1 SLC workflow also refers to **SNAPHU** and a locally configured processing environment.

**To execute the Jupyter code**, you must follow the order specified in the filename (e.g. 1_, 3_). The sensor-specific workflows can be executed in any order, they only need to be complete before moving to another step (DataPreprocessing, DatasetPreparation and BiomassMapping). 

**Important reuse limitations:**

- The supplied notebooks contain **local Windows filesystem paths** and expect specific directory structures. These must be adapted before execution.
- The dataset-preparation and mapping notebooks depend on **external raster/vector inputs, feature-selection results, and trained regression models**. Those inputs and model files are **not included** in the supplied code package.
- The notebooks have **not been converted into a fully portable or automatically executable pipeline**. Their presence here documents the processing implementations; it does not imply that the published paper can be reproduced from this repository alone.

---
## Provenance and Use Context

The workflows were developed in connection with **Below, Litter & Shrub BIOMASS density mapping combining optical, LiDAR and SAR Earth Observation data (BLS-BIOMASS)**, an ESA-funded research project involving the **Uninova - Instituto de Desenvolvimento de Novas Tecnologias**, **Instituto Superior de Agronomia, Universidade de Lisboa**, and **Norwegian University of Life Sciences**.

The root-level sensor folders provide reusable preprocessing references developed for study plots in Portugal and Spain. The separate `BLS-BIOMASS/` folder contains additional code used for project-specific data preparation and biomass mapping.

### Related Publication

Pereira-Pires, J. E., Guerra-Hernández, J., Anil-Lathika, A., Saarela, S., Silva, J. M. N., Fonseca, J. M., & Mora, A. (2026). **Biomass Prediction Combining Radar, Multispectral and Field Inventory Data**. *The International Archives of the Photogrammetry, Remote Sensing and Spatial Information Sciences*, **XLVIII-M-13-2026**, 41–48. https://doi.org/10.5194/isprs-archives-XLVIII-M-13-2026-41-2026

The publication describes biomass estimation for four components: aboveground biomass density (AGBD), belowground biomass density (BGBD), litter biomass density (LBD), and shrub biomass density (SBD), using satellite and ancillary predictors. This repository provides related processing and mapping code; **it does not currently include the full model-training workflow or all required data**.

---
## License

The repository's existing code is released under the **MIT License**; see [`LICENSE`](LICENSE). Reuse or redistribution of contributed material should follow the applicable permissions and attribution requirements.
