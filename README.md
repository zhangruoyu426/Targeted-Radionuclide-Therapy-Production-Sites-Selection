# Optimizing the Production Facility Network for Targeted Radionuclide Therapy: A Mixed-Integer Programming Approach

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange.svg)](https://jupyter.org/)

## Overview

This repository contains the complete implementation of a **mixed-integer linear programming (MILP)** model for optimizing the location, capacity, and service allocation of Pluvicto (¹⁷⁷Lu-PSMA-617) production facilities across the United States. The model balances construction and transportation costs while ensuring patient coverage within a clinically mandated 10-hour shipping window.

**Key Results:**
- A **five-facility network** achieves over **90% patient coverage** within 10 hours
- Optimal cost-weighting parameter: **λ = 0.1**
- Model outputs generally align with actual Novartis production sites

## Results

### Optimal Network Configuration

| Site | Location | Area (sq ft) | Capacity (vials/yr) | Utilization | Hospitals Served |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | New York-Newark-Jersey City | 22,297 | 80,268 | 100% | 143 |
| 2 | Chicago-Naperville-Elgin | 15,264 | 54,952 | 100% | 130 |
| 3 | Dallas-Fort Worth-Arlington | 10,000 | 36,000 | 65% | 84 |
| 4 | Atlanta-Sandy Springs-Roswell | 15,716 | 56,579 | 100% | 150 |
| 5 | Fresno, CA | 10,000 | 36,000 | 96% | 119 |

### Coverage Performance

- **90.7%** of patients within **10-hour** travel window
- **100%** of patients within **24-hour** travel window

### Cost Breakdown

- Total construction cost: **~$55 million**
- Annual transportation cost: **~$153 million**
- Optimized for λ = 0.1 (90% weight on transport)

## Industry Benchmarking

The model's recommended network was compared against Novartis's actual Pluvicto production footprint:

| Region | Model Recommendation | Novartis Actual | Match |
| :--- | :--- | :--- | :--- |
| Northeast | New York-Newark | Millburn, NJ | Strong |
| Midwest | Chicago | Indianapolis, IN | Size mismatch |
| West | Fresno | Carlsbad, CA | Strong |
| Southeast | Atlanta | Winter Park, FL (planned) | Location shift |
| South | Dallas | Denton, Tx (planned) | Strong |

**Interpretation:** The model successfully identifies the correct number (5) and geographic logic of facilities. Size differences indicate strategic overcapacity for future products and export markets.

## Model Formulation

The MILP model minimizes:

```
Minimize: λ × Construction Cost + (1-λ) × Transportation Cost
```

Subject to:
- **Coverage constraint:** Each treatment center assigned to a facility within max travel time
- **Capacity constraint:** Total demand assigned to each facility ≤ its capacity
- **Binary decisions:** Facility open/closed, capacity tier selected
- **Assignment constraints:** Each center served by exactly one facility

For the complete mathematical formulation, see the [full report](https://zhangruoyu426.github.io/Targeted-Radionuclide-Therapy-Production-Sites-Selection/Report.html).

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- Novartis for public data on Pluvicto production sites
- Treatment centers for patient volume data

---

**Last Updated:** July 2026
