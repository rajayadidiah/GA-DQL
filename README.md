# GA-DQL: Hybrid Genetic Algorithm + Double Q-Learning for Battery-Constrained Drone Routing in WRSNs

**CS5100 Foundations of AI — Capstone, Spring 2026**
Northeastern University, Khoury College of Computer Sciences
Instructor: Prof. Jonathan Mwaura

**Author:** D. Raja Yadidiah Dakey (NUID 003167334) — `dakey.d@northeastern.edu`

---

## Reproduction target
Watkins, C.J.C.H. & Dayan, P. (1992). *Q-learning.* Machine Learning, 8, 279–292.

## What this repo contains
| File | Purpose |
|------|---------|
| `Capstone_Final_Improved.ipynb` | Full Jupyter notebook — GA + Q-Learning + Double Q-Learning + experiments + plots |
| `FAI_Thesis.pdf` | Full thesis (thesis-length version) |
| `Capstone_Presentation.pptx` | Slide deck |
| `LICENSE` | MIT |

## Problem
Schedule a battery-constrained drone to visit energy-depleted sensor nodes in a Wireless Rechargeable Sensor Network (WRSN) under **stochastic disruptions** (wind, charger blockage, urgent reroutes, battery spikes — combined 57% per-step disruption rate).

## Approach — two-layer hybrid
1. **Layer 1 — Enhanced GA** (offline nominal plan): tournament selection, adaptive mutation decay, 2-opt local search, order-dependent 4-term fitness.
2. **Layer 2 — Q-Learning recovery** (online): 550-state MDP (SOC bucket × nearest-charger × pending nodes), 3 actions (local repair / divert / safety-first), three-tier risk-aware reward shaping.
3. **Double Q-Learning** (van Hasselt, 2010) to correct max-operator overestimation bias.

## How to run
1. Open `Capstone_Final_Improved.ipynb` in Google Colab or Jupyter.
2. Runtime → Run All. Total runtime ≈ 12–15 min on a free Colab CPU.
3. All plots save to `capstone_outputs/`. No GPU needed (tabular Q-table).
4. Dependencies: `numpy`, `pandas`, `matplotlib` — all preinstalled on Colab.

## Experiment protocol
- 5 test cases: 25 / 25 / 50 / 50 / 100 sensor nodes
- 5 random seeds per variant (42, 43, 44, 45, 46)
- 500 training episodes for each Q-agent
- 5 variants compared: FCFS, GA-only, Q-learning only, Hybrid GA+QL, Hybrid GA+Double-Q + risk shaping

## Headline results
| Variant | AWT (s) | SOC Violations | Recovery Rate |
|---------|--------:|---------------:|--------------:|
| FCFS | 312 | 94 | — |
| GA-only | 233 | 78 | 0.41 |
| Q-learning | 258 | 51 | 0.63 |
| Hybrid GA + Q | 198 | 11 | 0.89 |
| **Hybrid GA + Double Q + risk shaping** | **182** | **0** | **0.97** |

- Average Wait Time reduced **21.7%** vs GA-only baseline
- SOC violations driven from **78 → 0** across 5 test cases
- Disruption recovery rate: **97%**

## Reproducibility verdict
**Partially Reproducible.** The Q-learning update, its off-policy property, and its qualitative convergence behaviour from Watkins & Dayan (1992) reproduce cleanly in our 550-state WRSN MDP under Robbins–Monro α-decay and ε-greedy exploration. The *trend claim* (Q-learning beats FCFS / greedy) holds across all 5 seeds and all 5 test cases. However, the formal *convergence guarantee* does not survive our 57% per-step disruption rate: standard Q-learning shows overestimation-driven unsafe-SOC events that only Double Q-Learning and three-tier reward shaping resolve. Full justification in the final report.

## Links
- **Final report PDF:** submitted via course portal
- **Demo video (YouTube):** https://youtu.be/REPLACE_WITH_YOUR_VIDEO_ID

## License
MIT — free to reuse with attribution.

## Contact
`dakey.r@northeastern.edu`