# Hi-C Chromatin Contact Map Analysis

## Overview
This project implements a core Hi-C data analysis workflow using the Cooler ecosystem, applied to the landmark Rao et al. (2014) GM12878 lymphoblastoid cell Hi-C dataset. It covers raw contact matrix visualization, P(s) distance-decay analysis, and Observed/Expected normalization to reveal A/B compartment structure.

## Biological Question
How is chromatin organized in three-dimensional space within the nucleus, and what large-scale structural features (A/B compartments) can be identified from genome-wide contact frequency data?

Hi-C measures the frequency of physical contact between all pairs of genomic loci simultaneously, providing a genome-wide map of chromatin organization that is invisible to linear sequence analysis.

## Data
- **Rao et al. (2014) GM12878 Hi-C dataset**, 1 Mb resolution, MboI enzyme, filtered and balanced
- Accessed via the open2c community repository (downloads automatically within the notebook)
- Original paper: Rao et al. (2014) *A 3D Map of the Human Genome at Kilobase Resolution Reveals Principles of Chromatin Looping.* Cell 159, 1665–1680

## Methods & Tools

**Language:** Python 3.10+

| Library | Purpose |
|---|---|
| `cooler` | Loading and accessing Hi-C contact matrices in .cool format |
| `cooltools` | Supplementary Hi-C analysis utilities |
| `numpy` | Matrix operations and distance-decay computation |
| `matplotlib` | Contact map and P(s) visualization |

**Analysis steps:**
1. Load a 1 Mb resolution `.cool` file using the Cooler API
2. Visualize log-normalized raw contact matrices for chr6 and chr2
3. Compute P(s) — mean contact probability as a function of genomic distance — by averaging along matrix diagonals
4. Fit a power law to the P(s) curve and report the decay exponent
5. Compute the Observed/Expected (O/E) matrix by normalizing raw counts by the P(s)-derived expected frequency at each distance
6. Visualize O/E matrices to reveal A/B compartment structure (checkerboard enrichment pattern)
7. Compare P(s) curves between chr6 and chr2

## Key Results
- Raw contact matrices show clear diagonal dominance (nearby loci interact most) with centromeric gaps reflecting unmappable repeat regions
- P(s) curves follow approximately power-law decay; the estimated exponent is reported and compared against the fractal globule (~1.0) and equilibrium polymer (~1.5) predictions
- O/E normalization reveals the A/B compartment checkerboard pattern that is obscured in the raw matrix by the distance-decay effect
- Chr6 and chr2 show similar P(s) decay profiles, consistent with similar chromatin compaction at this resolution

## How to Run

**Option 1 — Google Colab (recommended)**
1. Upload `HiC_Contact_Map_Analysis.ipynb` to Google Colab
2. Run all cells top to bottom — the dataset downloads automatically

**Option 2 — Local environment**
```bash
git clone https://github.com/yourusername/hic-contact-map-analysis
cd hic-contact-map-analysis
pip install -r requirements.txt
jupyter notebook HiC_Contact_Map_Analysis.ipynb
```

## Project Structure
```
hic-contact-map-analysis/
├── README.md
├── HiC_Contact_Map_Analysis.ipynb
└── requirements.txt
```
