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

---
 
## Process Description
 
### Column 1 — Demethanizer (Reboiled Absorber)
 
The two well streams enter a 10-stage reboiled absorber. Well 1 feeds from the top stage; Well 2 from stage 2. An external duty of 2×10⁶ BTU/hr is supplied at stage 4 to improve separation efficiency.
 
| Parameter | Value |
|---|---|
| No. of stages | 10 |
| Top stage pressure | 330 psia |
| Reboiler pressure | 335 psia |
| Top stage temperature | -125°F |
| Reboiler temperature | 80°F |
| Overhead product rate | 2,950 lbmol/h |
| **Product purity target** | **C1 mole fraction ≥ 0.96** |
 
**Overhead product:** Pipeline-grade methane  
**Bottom product:** NGL-rich liquid (C2+), pumped to 2,790 kPa and fed to Column 2
 
---
 
### Column 2 — De-ethanizer (Distillation Column)
 
A 14-stage distillation column with a partial condenser. Feed enters at stage 6. Ethane exits as the overhead vapour product; the C3+ bottom stream is pressure-reduced to 1,690 kPa via a valve and fed to Column 3.
 
| Parameter | Value |
|---|---|
| No. of stages | 14 |
| Feed stage | 6 |
| Condenser type | Partial |
| Condenser pressure | 2,725 kPa |
| Reboiler pressure | 2,792 kPa |
| Condenser temperature | -4°C |
| Reboiler temperature | 95°C |
| Overhead vapour rate | 320 kgmol/h |
| Reflux ratio | 2.5 (molar) |
| **Product purity target** | **C2/C3 ratio in bottoms ≤ 0.01** |
 
**Overhead products:** Ethane vapour + ethane liquid  
**Bottom product:** C3+ stream, throttled to 1,690 kPa
 
---
 
### Column 3 — De-propanizer (Distillation Column)
 
A 24-stage distillation column with a total condenser. Feed enters at stage 11. Propane is recovered overhead as a liquid product; heavier hydrocarbons (C4+) exit at the bottom.
 
| Parameter | Value |
|---|---|
| No. of stages | 24 |
| Feed stage | 11 |
| Condenser type | Total |
| Condenser pressure | 1,585 kPa |
| Reboiler pressure | 1,655 kPa |
| Condenser temperature | 38°C |
| Reboiler temperature | 120°C |
| Distillate rate | 110 kgmol/h |
| Reflux ratio | 1.0 (molar) |
| **Product purity target** | **i-C4 + n-C4 overhead mol fraction ≤ 0.15; C3 bottoms mol fraction ≤ 0.02** |
 
**Overhead product:** Propane liquid (LPG-grade)  
**Bottom product:** Heavier hydrocarbons (C4+, NGL condensate)
 
---
 
## Product Summary
 
| Stream | Product | Key Specification Met |
|---|---|---|
| Demethanizer overhead | Methane (pipeline gas) | C1 mol fraction = 0.96 |
| De-ethanizer overhead | Ethane (vapour + liquid) | C2/C3 bottoms ratio = 0.01 |
| De-propanizer overhead | Propane liquid (LPG) | i-C4 + n-C4 ≤ 0.15 mol fraction |
| De-propanizer bottoms | Heavier hydrocarbons (C4+) | C3 mol fraction ≤ 0.02 |
 
---
 
## Key Engineering Decisions
 
- **Reboiled absorber for Column 1** — chosen over a standard distillation column because the Demethanizer operates at cryogenic conditions (-125°F top stage) where a conventional condenser is impractical. The external duty injection at stage 4 compensates for the absence of a condenser and improves methane recovery.
- **Peng-Robinson EOS** — selected as the fluid package because it accurately models vapour-liquid equilibria for light hydrocarbon systems at the high-pressure, low-temperature conditions across all three columns.
- **Pressure staging across the train** — each column operates at progressively lower pressure (330 psia → ~400 psia → ~2,790 kPa → ~1,690 kPa), with deliberate pressure reduction via pump and valve between columns to maintain thermodynamic driving force for separation.
- **Partial condenser on De-ethanizer** — allows simultaneous recovery of ethane as both vapour and liquid products, providing flexibility for downstream use.
---
 
## What I Learnt
 
**Sequencing matters in multi-column trains.** The order of separation, lightest component first isn't arbitrary. Removing methane first prevents it from loading up the downstream columns and driving up reboiler duties. Getting the sequencing wrong would have cascading convergence problems across the whole flowsheet.
 
**Product specifications drive backwards into your design.** The requirement for methane overhead mole fraction of 0.96 forced me to revisit my Ovhd Prod Rate specification. I didn't fully appreciate early on how tightly these constraints are coupled changing one spec ripples through everything else.
 
**Pressure drops are easy to overlook but critical.** The 35 kPa condenser pressure drop in both the De-Ethanizer and De-Propanizer seems minor, but ignoring it throws off your temperature profiles entirely. I learned to always account for pressure drops across every section of a column, not just the overall operating pressure.
 
**Simulation and understanding are two different things.** Getting the flowsheet to converge felt like a win, but I realized I couldn't fully explain why certain parameters were set the way they were until I went back to the fundamentals. The simulator gives you answers the engineering understanding has to come from you.
 




