# Steel Frame Seismic Response Dataset

This repository provides a numerical dataset for machine-learning-based seismic response prediction of five-story steel frame structures.

The dataset was generated from nonlinear time-history analyses of a five-story equivalent shear-type steel frame model. Two ground motions are considered: EI and Northridge. The processed dataset contains 2,000 valid samples, including 1,000 samples under the EI ground motion and 1,000 samples under the Northridge ground motion.

## Dataset Scope

This repository is intended to provide data only. Source code is not included in this release.

The dataset contains two levels of data:

1. **Summary data**: one row per analysis case, including structural input parameters and peak seismic response outputs.
2. **Full time-history data**: per-case response histories, including floor displacement, story drift, base shear, and case-level summary files. These files are recommended to be uploaded as GitHub Release assets.

## Recommended Repository Structure

```text
steel-frame-seismic-response-dataset/
│
├── README.md
├── LICENSE
├── CITATION.cff
│
├── data/
│   ├── summary/
│   │   ├── summary_results_all.csv
│   │   ├── summary_results_ei.csv
│   │   └── summary_results_northridge.csv
│   │
│   └── metadata/
│       ├── data_dictionary.csv
│       ├── case_index.csv
│       └── ground_motion_info.csv
│
└── release-assets/
    ├── full_time_histories_ei.zip
    └── full_time_histories_northridge.zip
```

The `release-assets/` folder is only for local preparation. Large ZIP files should be uploaded to the GitHub Release page rather than committed directly to the repository.

## Data Description

Each sample corresponds to one nonlinear time-history analysis case of a five-story equivalent shear-type steel frame.

### Input Variables

The main input variables include:

| Variable | Description | Unit |
|---|---|---|
| `K1_N_per_m`–`K5_N_per_m` | Initial lateral stiffness of stories 1–5 | N/m |
| `Qy1_N`–`Qy5_N` | Yield shear force of stories 1–5 | N |
| `floor_mass_kg` | Lumped floor mass | kg |
| `story_height_m` | Story height | m |
| `damping_ratio` | Target damping ratio | - |
| `alpha_post` | Post-yield stiffness ratio | - |
| `gm_name` | Ground motion name | - |
| `dt` | Ground motion time step | s |
| `n_steps` | Number of analysis steps | - |

### Output Variables

The main output variables include:

| Variable | Description | Unit |
|---|---|---|
| `top_disp_max_m` | Maximum absolute roof displacement | m |
| `max_story_drift` | Maximum absolute interstory drift ratio | - |
| `base_shear_max_N` | Maximum absolute base shear | N |

## Summary Data Files

| File | Description |
|---|---|
| `data/summary/summary_results_all.csv` | Combined dataset of all valid samples |
| `data/summary/summary_results_ei.csv` | Dataset under the EI ground motion |
| `data/summary/summary_results_northridge.csv` | Dataset under the Northridge ground motion |
| `data/metadata/data_dictionary.csv` | Explanation of variables, units, and data types |
| `data/metadata/case_index.csv` | Index table linking each case to its corresponding time-history files |
| `data/metadata/ground_motion_info.csv` | Basic information on ground motion records |

## Full Time-History Data

The full time-history data are provided as release assets:

```text
full_time_histories_ei.zip
full_time_histories_northridge.zip
```

Each case folder contains:

```text
floor_disp.csv
story_drift.csv
base_shear.csv
case_summary.json
```

The recommended internal structure of each ZIP file is:

```text
ei/
  Case0001/
    floor_disp.csv
    story_drift.csv
    base_shear.csv
    case_summary.json
  Case0002/
  ...
```

and

```text
northridge/
  Case0001/
    floor_disp.csv
    story_drift.csv
    base_shear.csv
    case_summary.json
  Case0002/
  ...
```

## Suggested Usage

```python
import pandas as pd

df = pd.read_csv("data/summary/summary_results_all.csv")
print(df.head())
```

## Data Availability Statement

The OpenSees-generated seismic response dataset for the five-story steel frame is publicly available in this repository. The processed summary data are provided in the `data/summary/` folder. The full time-history response data are provided as GitHub Release assets.

## License

This dataset is released under the Creative Commons Attribution 4.0 International License (CC BY 4.0). See the `LICENSE` file for details.

## Citation

If you use this dataset, please cite this repository and the related paper. Citation information is provided in `CITATION.cff`.
