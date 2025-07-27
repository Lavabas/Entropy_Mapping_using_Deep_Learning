# Urban Morphological Entropy Mapping using Deep Learning in Colombo
This project extends deep learning-based road morphology classification to compute and map urban morphological entropy in Colombo, Sri Lanka,using a pretrained ResNet-34 model and CRHD (City Road Hierarchy Descriptor) images. The goal is to identify spatial zones with ambiguous, mixed, or transitional road patterns through entropy analysis of deep learning model outputs.

While most urban morphology studies assign a fixed class to each region (e.g., "Organic", "Gridiron"), our approach leverages softmax probabilities from a deep learning model to measure uncertainty and diversity of street patterns within each grid cell. This is done via Shannon entropy, creating a new spatial layer that:
- Highlights ambiguous or transitional urban forms
- Detects informal development or planning inconsistencies
- Enables comparative spatial analysis of urban form complexity

#### Novelty: Classical methods provide only rigid classifications. This deep learning pipeline quantifies how mixed the morphological identity of a place is, a concept not feasible without access to full probability vectors from a deep model.

## Background
This work builds upon:

Chen et al. (2024) – Global urban road network patterns: Unveiling multiscale planning paradigms of 144 cities with a novel deep learning approach.
Landscape and Urban Planning, 241, 104901.
https://doi.org/10.1016/j.landurbplan.2024.104901

The original study introduced CRHD and trained a ResNet-34 model to classify 1 km road network images into 6 categories: Gridiron, Linear, Nopattern, Organic, Radial, Tributary. This project applies entropy-based post-processing to enrich the analysis.


## Workflow Summary
#### Phase 1: Road Pattern Classification
- Generate CRHD images for Colombo via crhd_generator_v2.py.
- Classify using pretrained ResNet-34 (6-class) to produce per-grid probability vectors.
- Save predictions to colombo_road_patterns.csv.

#### Phase 2: Entropy Mapping (this repo)
- Load CSV with predicted probabilities
- Compute Shannon entropy per grid
        <img width="892" height="110" alt="image" src="https://github.com/user-attachments/assets/fa30378f-88b0-4314-9697-44aa3ac02d71" />
- Merge entropy scores with Colombo grid shapefile
- Visualize results with basemap using contextily


## Tools & Libraries
| Library           | Purpose                                   |
| ----------------- | ----------------------------------------- |
| `tensorflow`      | Deep learning (ResNet-34 model inference) |
| `pandas`, `numpy` | Data manipulation and entropy computation |
| `geopandas`       | Spatial shapefile handling                |
| `contextily`      | Add basemap to plots                      |
| `matplotlib`      | Visualization                             |

<img width="977" height="1390" alt="image" src="https://github.com/user-attachments/assets/749fbc16-fdb9-4382-b8e3-f3e305e17a80" />


## Interpretation of the Entropy Map
Each grid cell represents a ~1 km² area, and entropy quantifies morphological diversity:
| Entropy Value          | Interpretation                                                                                                                                              |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Low** (≈ 0)          | Dominated by a **single road pattern** (e.g., purely organic or gridiron). Indicates **uniform planning** or traditional morphologies.                      |
| **Medium** (\~0.8–1.5) | Mixture of 2–3 road types. Could represent **transition zones** (e.g., urban expansion, commercial/residential blends).                                     |
| **High** (>1.8)        | Strongly **mixed morphology**. Indicates **heterogeneous development**, e.g., informal settlements, peri-urban areas, or zones with design inconsistencies. |

Observations from Colombo Map:
1. Northern port/industrial areas show high entropy — could reflect fragmented planning or mixed functional use.
2. Central and southern areas show more uniform morphology — possibly reflecting planned residential zones.
3. Eastern edge (near Kelani River) shows medium entropy — maybe a transition zone.

## Why This Matters
| Classical Morphology         | Deep Learning Morphology       |
| ---------------------------- | ------------------------------ |
| Single label per grid        | Probability per class          |
| No info on ambiguity         | Entropy quantifies uncertainty |
| Manual mapping               | Automated inference            |
| No detection of hybrid areas | Mixed zones are highlighted    |

Morphological entropy is a novel urban indicator that complements hard classification with insights into complexity and irregularity, especially relevant for fast-changing or informally developed cities.

## Citation
If using this approach, cite the original research paper:
@article{chen2024global,
  title={Global urban road network patterns: Unveiling multiscale planning paradigms of 144 cities with a novel deep learning approach},
  author={Chen, Wangyang and Huang, Huiming and Liao, Shunyi and Gao, Feng and Biljecki, Filip},
  journal={Landscape and Urban Planning},
  volume={241},
  pages={104901},
  year={2024},
  publisher={Elsevier}
}








