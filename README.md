# CS5100 FAI Capstone — Hybrid GA + Double Q-Learning for Battery-Constrained Drone Routing

**Reproduction of:** Watkins, C.J.C.H. & Dayan, P. (1992). *Q-learning.* Machine Learning, 8, 279–292.

**Author:** D. Raja Yadidiah Dakey
**NUID:** 003167334
**Email:** dakey.r@northeastern.edu
**Course:** CS5100 Foundations of Artificial Intelligence — Spring 2026
**Instructor:** Prof. Jonathan Mwaura
**Institution:** Northeastern University, Khoury College of Computer Sciences

---

## 🎥 Demo video
**Public YouTube:** https://youtu.be/-O3yH9AKT7g

## 📄 Final report
[`Dakey_CS5100_Final_Report.pdf`](./Dakey_CS5100_Final_Report.pdf)

## 📓 Code
[`Capstone_Final_Improved.ipynb`](./Capstone_Final_Improved.ipynb) — self-contained Google Colab notebook. Runtime: ~12–15 min on a free Colab CPU. No GPU needed.

---

## What this project does

Reproduces tabular Q-learning from Watkins & Dayan (1992) on a battery-constrained drone-routing MDP, and evaluates three extensions:

1. **Double Q-Learning** (van Hasselt, 2010) — corrects overestimation bias
2. **GA-derived nominal route** (from my NIT Trichy B.Tech FYP) — structured exploration prior
3. **Three-tier risk-aware reward shaping** (Critical / Moderate / Mild SOC tiers)

## How to run

1. Open `Capstone_Final_Improved.ipynb` in Google Colab
2. `Runtime → Run all` (Ctrl+F9)
3. All plots, logs, and result tables are written to `/content/drive/MyDrive/capstone_outputs/`

## Dependencies
Pre-installed on Colab: `numpy`, `pandas`, `matplotlib`. No extra `pip install` required. No GPU.

## Experiment protocol

- **5 test cases:** 25 / 25 / 50 / 50 / 100 sensor nodes
- **5 random seeds per variant:** {42, 43, 44, 45, 46}
- **500 training episodes per agent**
- **5 variants compared:** FCFS, GA-Only, Q-Learning-Only, Hybrid GA+QL, Hybrid GA+Double-Q+risk-shaping

## Headline results (TC3, 50 nodes, mean of 5 seeds)

| Variant | AWT (s) | SOC Violations | Recovery Rate |
|---|---|---|---|
| GA-Only | 312 | 78 | 0% |
| Q-Learning-Only | 298 | 51 | 41% |
| GA + Greedy | 276 | 11 | 63% |
| Hybrid GA + QL | 198 | 3 | 89% |
| **Hybrid GA + Double Q + risk shaping** | **182** | **0** | **97%** |

## Reproducibility verdict

**Partially Reproducible.** The Watkins & Dayan (1992) Q-learning update, its off-policy property, and its qualitative convergence behaviour reproduce cleanly on our 550-state WRSN MDP. The formal convergence *guarantee* does not survive the 57% per-step disruption rate without Double Q-Learning and risk-aware reward shaping. Full justification: Analysis & Reproducibility Verdict sections of `Dakey_CS5100_Final_Report.pdf`.

## Repository contents

| File | Purpose |
|---|---|
| `Capstone_Final_Improved.ipynb` | End-to-end Colab notebook (environment, GA, Q-learning, Double-Q, experiments, plots) |
| `Dakey_CS5100_Final_Report.pdf` | 6-page final report (CS5100 Spring 2026 capstone submission) |
| `Capstone_Presentation.pptx` | Slide deck used for demo video |
| `FAI_Thesis.pdf` | Extended thesis / background reference |
| `LICENSE` | MIT |
| `README.md` | This file |

## Citation

If you use this code or build on it, please cite:

> Dakey, D. R. Y. (2026). *A Hybrid Offline-Online Routing Framework for Battery-Constrained Drone Delivery in Wireless Rechargeable Sensor Networks.* CS5100 Capstone Report, Northeastern University.

Original paper:

> Watkins, C. J. C. H., & Dayan, P. (1992). Q-learning. *Machine Learning, 8*(3), 279–292.

## License
MIT — free to reuse with attribution.

## Contact
dakey.r@northeastern.edu