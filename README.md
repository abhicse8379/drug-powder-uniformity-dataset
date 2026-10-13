# Pharmaceutical Powder Mixing Uniformity Dataset

## Overview
This repository contains microscopic images of pharmaceutical powder samples for research into automated mixing uniformity classification using computer vision and deep learning.

## Classification
- **Mixed:** Samples labelled as adequately mixed according to the study's defined reference criteria.
- **Not_Mixed:** Samples labelled as inadequately mixed according to the study's defined reference criteria.

These labels represent the study's operational criteria and do not independently establish pharmaceutical content uniformity.

## Dataset Details
- **Total images:** [Insert verified count]
- **Number of classes:** 2
- **Classes:** Mixed, Not_Mixed
- **Image format:** [Insert actual format]
- **Image dimensions:** [Insert actual dimensions]
- **Microscope magnification:** [Insert actual magnification]
- **Ground-truth method:** [Describe the laboratory reference procedure]

## Repository Structure
- `images/Mixed/` — images labelled Mixed
- `images/Not_Mixed/` — images labelled Not_Mixed
- `metadata.csv` — image-level metadata
- `DATASET_CARD.md` — detailed dataset documentation

## Intended Use
The dataset is intended for academic research on pharmaceutical powder mixing uniformity, image classification, deep learning, multi-colour-space feature fusion, and explainable AI.

## Limitations
Results obtained using this dataset may not generalize to other formulations, laboratories, or imaging conditions without independent validation. Model predictions are not a substitute for validated pharmaceutical quality-control procedures.

## Citation
Please cite this repository using its recommended GitHub citation information. A DOI-based citation may be added if the dataset is subsequently archived in a DOI-issuing repository.

## License
See the `LICENSE` file for the applicable reuse terms.
