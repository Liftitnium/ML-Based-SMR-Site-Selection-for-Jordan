# Jordan SMR Site Selection — ML Pipeline

## Project structure

```
databases/
├── jordan_smr_ml_pipeline.ipynb   # main notebook — start here
├── datasets/
│   ├── srtm/                      # SRTM elevation tiles
│   ├── osm/                       # OpenStreetMap Jordan
│   ├── aquastat/                  # AQUASTAT water statistics CSV
│   └── gsw/                       # Global Surface Water GeoTIFF
└── output/
    ├── final/                     # all pipeline outputs
    └── _extracted/                # working dataset copies (do not delete)
```

## Environment setup

From the project root:

```bash
python3 -m venv .venv
source .venv/bin/activate   # On Windows: .venv\Scripts\activate
pip install -r requirements.txt
python -m ipykernel install --user --name jordan-smr --display-name "Python (jordan-smr)"
```

Then in Jupyter or VS Code, select the **Python (jordan-smr)** kernel for the notebook.

## How to run

1. Open `jordan_smr_ml_pipeline.ipynb` in Jupyter or VS Code.
2. Select kernel **Python (jordan-smr)** (or ensure the notebook runs from the project root).
3. Run all cells. All outputs are saved to `output/final/`.


## Key numbers

- Total cells: 151,156
- Viable after hard filters: 133,166 (88.1%)
- Eliminated by seismic: 13,515
- Eliminated by population: 1,596
- Eliminated by permanent water: 1,531
- Eliminated by slope: 1,348

## Citation
If you use this work, please cite:
Nasrallah, R. (2026). A Multi-Criteria Machine Learning Framework 
for SMR Site Selection in Water-Scarce Economies: A Jordan Case Study. 
IE University, Madrid.

## Contact
Raji Nasrallah — IE University  
GitHub: github.com/Liftitnium
