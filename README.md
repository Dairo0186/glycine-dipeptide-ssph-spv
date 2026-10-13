# Glycine Dipeptide SSPH–SPV

Reproducibility repository for the manuscript **“Topological Organization of the Gas-Phase Glycine Dipeptide Energy Landscape”**.

This repository contains the corrected periodic potential-energy grid, the sublevel-set persistent-homology (SSPH) analysis, the persistence-derived critical-event tables, the principal figures, and the quantum-chemical stationary-point validation (SPV) used for gas-phase N-acetylglycine-*N*′-methylamide (Ace–Gly–NMe).

## Scientific scope

- Electronic-structure level: B3LYP-D3(BJ)/def2-SVP.
- Reduced coordinates: peptide-backbone dihedrals $\phi$ and $\psi$.
- Periodic domain: $\mathbb{S}^1\times\mathbb{S}^1\cong\mathbb{T}^2$.
- Final grid: $36\times36$ unique angular configurations at $10^\circ$ resolution.
- Persistence coefficient field: $\mathbb{F}_2$.
- Reporting threshold: $\varepsilon_{\mathrm{pers}}=0.045\ \mathrm{kcal\,mol^{-1}}$.

At this reporting scale, the filtration retains five $H_0$ classes, six $H_1$ classes, and one $H_2$ class. The corresponding event counts are $(m_0,m_1,m_2)=(5,10,5)$, satisfying $m_0-m_1+m_2=0=\chi(\mathbb{T}^2)$. The five retained basin components form a single connected sublevel-set component by $3.168126\ \mathrm{kcal\,mol^{-1}}$.

Independent unconstrained optimizations and harmonic frequency calculations confirm M1–M5 as local minima at the selected level of theory. Separate transition-state and mode-displacement calculations validate the four basin-merger events S1–S4 as first-order saddles connecting the minimum pairs reported in `results/stationary_points/validated_saddles.tsv`. The remaining persistence-derived index-1 events are topological descriptors and are not claimed as optimized transition states.

## Repository structure

```text
notebooks/                         Reproducible SSPH analysis notebook
data/processed/                    Corrected SSPH input and periodic grid
data/validation/                   Periodic-reconciliation audit
results/persistence/               Retained and complete positive intervals
results/stationary_points/         Minimum and saddle summaries
figures/                           Principal publication figures
gaussian/minima/                   Unconstrained minimum opt+freq logs
gaussian/saddles/                  TS and mode-displacement opt+freq logs
gaussian/periodic_reconciliation/  Boundary and restarted scan calculations
```

The large Gaussian checkpoint and scratch files are intentionally excluded. The deposited `.log` files retain the route sections, molecular specifications, convergence information, frequencies, and final energies required to inspect the validation calculations.

## Reproducing the SSPH analysis

1. Create a Python 3.12 environment.
2. Install the dependencies:

   ```bash
   python -m pip install -r requirements.txt
   ```

3. Open `notebooks/glycine_ssph_spv.ipynb` and run all cells from the repository root. The notebook reads `data/processed/morse_input_periodic_symmetry_repaired.txt`.

The persistent-homology calculation always uses the complete, unclipped energy array. Energy clipping is applied only to selected graphical color scales.

## Periodic preprocessing

Periodically equivalent boundary configurations were compared before endpoint removal. When sequential scans converged to different constrained branches, endpoint-derived geometries were independently reoptimized and the lowest converged constrained energy was assigned to the periodic equivalence class. Nine raw-grid records were updated in total. The original values, replacements, calculation sources, and selection rationale are documented in `data/validation/Table_S1_energy_repair_audit.tsv`.

No averaging, smoothing, fitting, or interpolation was applied to the energies used for persistent homology.

## Citation

Please cite the associated manuscript and this repository. Bibliographic metadata are provided in `CITATION.cff`. The journal DOI will be added after publication.

## License

Code is released under the MIT License. Quantum-chemical outputs and numerical research data are provided for scholarly reproducibility with attribution to the authors.

