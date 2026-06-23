# NGL Fractionation Train — Aspen HYSYS Process Simulation

Simulating the separation of natural gas liquids from crude wellhead gas using a three-column distillation train, built entirely in Aspen HYSYS with the Peng-Robinson equation of state.

## Flowsheet Overview

![NGL Fractionation Train Flowsheet](https://github.com/purity-portfolio/NGL-fractionation-train-simulation/blob/main/NGL%20FRACTIONATION%20TRAIN.png)

---
 
## Problem Statement
 
Crude natural gas from two production wells contains heavier hydrocarbons (C2–C8) that must be removed before the gas is suitable for pipeline transportation. This simulation models the full separation sequence from raw wellhead feed to four distinct product streams across three distillation columns operating in series.

---
 
## Tools Used
 
| Tool | Purpose |
|---|---|
| Aspen HYSYS v12 | Process simulation and column convergence |
| Peng-Robinson (PR) EOS | Fluid package for vapour-liquid equilibrium |
| HYSYS Column Specs | Overhead purity and product ratio targeting |

---
 
## Feed Conditions
 
Two wellhead streams are combined as feed to the Demethanizer.
 
| Component | Well 1 (mol fraction) | Well 2 (mol fraction) |
|---|---|---|
| N₂ | 0.0025 | 0.0057 |
| CO₂ | 0.0048 | 0.0029 |
| C1 (Methane) | 0.7041 | 0.7227 |
| C2 (Ethane) | 0.1921 | 0.1176 |
| C3 (Propane) | 0.0706 | 0.0750 |
| n-C4 | 0.0112 | 0.0204 |
| i-C4 | 0.0085 | 0.0197 |
| n-C5 | 0.0036 | 0.0147 |
| i-C5 | 0.0020 | 0.0102 |
| n-C6 | 0.0003 | 0.0037 |
| n-C7 | 0.0002 | 0.0047 |
| n-C8 | 0.0001 | 0.0027 |
 
| Stream Parameter | Well 1 | Well 2 |
|---|---|---|
| Temperature | -140°F | -120°F |
| Pressure | 330 psia | 332 psia |
| Flow Rate | 3,575 lbmol/h | 475 lbmol/h |




