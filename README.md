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

## How to run

1. Open `jordan_smr_ml_pipeline.ipynb` in Jupyter or VS Code.
2. Run all cells from the project root (`databases/`).
3. All outputs are saved to `output/final/`.

## Current status

- [x] Data prep pipeline: COMPLETE
- [x] Feature matrix: 151,156 cells, 12 features, 133,166 viable
- [ ] Section 2 — EDA: ready to run
- [ ] Section 3 — Label generation: ready to run
- [ ] Section 4 — Stage 1 Logistic Regression: ready to run
- [ ] Section 5 — Stage 2 XGBoost: ready to run
- [ ] Section 6 — SHAP explainability: ready to run
- [ ] Section 7 — Suitability heatmap: ready to run
- [ ] Section 8 — Top candidate sites: ready to run
- [ ] Section 9 — Save final outputs: ready to run

## Key numbers

- Total cells: 151,156
- Viable after hard filters: 133,166 (88.1%)
- Eliminated by seismic: 13,515
- Eliminated by population: 1,596
- Eliminated by permanent water: 1,531
- Eliminated by slope: 1,348
