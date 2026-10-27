# Jordan SMR Site Selection — ML Pipeline

A personal project: a geospatial pipeline that splits Jordan into a 1 km grid (151,156 cells), attaches seismic, population, terrain, water and infrastructure features to each cell, and ranks candidate sites for a Small Modular Reactor.

**Read this before the results.** The ranking comes from a heuristic I made up, not from real siting data. There is no ground truth here, so the maps show what my rules prefer, not where a reactor should actually go. Details in [How it really works](#how-it-really-works).

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

## How it really works

1. **Hard filters.** Cells are dropped when PGA > 0.3g, population > 1,000/km², slope > 18° or surface-water occurrence > 80%. This leaves 133,166 cells.
2. **Labels (Stage 1).** A cell is labelled "highly suitable" when it meets all of: PGA < 0.15g, slope < 5°, population < 100/km², river within 10 km, water occurrence < 20, road within 50 km. These thresholds are my own choices. IAEA SSG-35 names the factors (seismic hazard, population, terrain, cooling water) but does not give these numbers.
3. **Logistic regression** is trained on those labels using the same features the rules were written from. Its high accuracy and AUC therefore only show that it can learn my rules back; they are not evidence of real-world suitability.
4. **Suitability score (Stage 2).** A weighted sum with hand-picked weights: water features 2×, safety 1.5×, infrastructure 1×. XGBoost is trained to predict that sum, so it reproduces the heuristic rather than discovering anything new.
5. **SHAP** explains the XGBoost model, which means it explains my heuristic. "River distance matters most" is a consequence of the 2× water weight, not a finding.

### Limitations

- No validation against real siting studies, existing nuclear or thermal plant locations, or expert judgement.
- Thresholds and weights were not tuned or tested for sensitivity; different reasonable choices would move the top sites.
- HydroRIVERS includes seasonal wadis, so "distance to river" (mean 1.6 km) overstates access to reliable cooling water in a desert country.
- The data-prep code that builds `jordan_smr_features.csv` is not in this repo, and some notebook cells are stored as Markdown, so the notebook does not run cleanly top to bottom yet.

### What would make it real

Validate against known plant sites or published Jordanian siting studies, run a sensitivity analysis on the thresholds and weights, use perennial-water sources only, and commit the data-prep pipeline.

## Data sources

SRTM elevation (NASA), GEM seismic hazard, HydroSHEDS (HydroRIVERS, HydroLAKES, HydroBASINS), JRC Global Surface Water, GHSL population, ERA5 climate (Copernicus), Global Power Plant Database, OpenStreetMap, GADM boundaries, FAO AQUASTAT. Each keeps its own licence; check them before reusing the data.

## Citation
This is an unpublished personal project. If you reference it:
Nasrallah, R. (2026). Jordan SMR site selection: a heuristic geospatial pipeline. GitHub, github.com/Liftitnium/ML-Based-SMR-Site-Selection-for-Jordan.

## Contact
Raji Nasrallah — IE University  
GitHub: github.com/Liftitnium
