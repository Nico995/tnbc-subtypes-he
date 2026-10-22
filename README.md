# Deep learning prediction of triple-negative breast cancer molecular subtypes and tumor microenvironment features from H&E slides

> 🚧 **Code coming soon.** This repository will host the code accompanying our manuscript, which is currently in preparation. The full pipeline will be released here once the paper is published.

---

## Overview

Triple-negative breast cancer is molecularly heterogeneous. Transcriptomic classifications divide it into subtypes, such as basal-like (BL), immunomodulatory (IM), luminal androgen receptor (LAR), mesenchymal (M) and mesenchymal stem-like (MSL), that differ in biology, prognosis and response to treatment. Assigning these subtypes currently requires gene expression profiling, which is not part of routine clinical practice.

This project predicts TNBC molecular subtypes and tumor microenvironment features directly from routine H&E-stained whole-slide images (WSIs), using deep learning on top of pathology foundation models.

## Approach

- **Tile embeddings from pathology foundation models.** Slides are tiled at 20× magnification and each tile is encoded with a pretrained foundation model (UNI v2, CONCH v1.5, Virchow2, Prov-GigaPath, CTransPath).
- **Attention-based multiple instance learning.** A CLAM-style attention MIL model aggregates tile embeddings into a slide-level representation. Instead of predicting a single class, the model **regresses continuous subtype scores**, preserving the heterogeneity of tumours that fall between subtypes.
- **Interpretability.** Attention maps highlight the tissue regions that drive each prediction.
- **Virtual biopsies.** The model is also evaluated on biopsy-sized regions sampled from resection slides, to assess how predictions hold up on the smaller tissue samples available at diagnosis.
- **External validation.** Models are trained with cross-validation and evaluated on independent cohorts, including public datasets such as TCGA and CPTAC.

## Planned repository contents

| Component | Description |
|---|---|
| `src/` | Model definitions, training and evaluation entry points |
| `configs/` | [Hydra](https://hydra.cc/) configuration for data, embeddings, models and experiments |
| `scripts/` | Cross-validation, grid search and external validation launchers |
| `notebooks/` | Data preparation, virtual biopsy generation, results and attention analysis |

Training is built on PyTorch Lightning, with tile feature extraction handled by [TRIDENT](https://github.com/mahmoodlab/TRIDENT).

## Data availability

No patient data are included in this repository. Information on how to obtain the cohorts used in the study will be provided with the publication, subject to the access conditions of each dataset.

## Citation

A citation will be added once the manuscript is published.

## Acknowledgements

This work was carried out at the Breast Cancer Translational Research Laboratory (BCTL), Institut Jules Bordet, Université Libre de Bruxelles. The MIL framework builds on [CLAM](https://github.com/mahmoodlab/CLAM) (Lu et al., *Nature Biomedical Engineering*, 2021).

## License

Released under the MIT License (license file to be added with the code release).
