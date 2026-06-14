# Power System Operation and Management (PowerWorld / PWRFLOW)

## Overview
This repository contains a comprehensive suite of power system engineering analyses focusing on load flow optimization, power exchange dispatch control, and network security/contingency mitigation. All simulation models and data were implemented in **PowerWorld (PWRFLOW)** as part of the ECE curriculum at the Aristotle University of Thessaloniki (AUTh).

The project investigates practical power system operational constraints across three main layers: passive voltage control, inter-area market dispatch, and dynamic corrective action under N-1 line outages.

---

## Technical Project Modules

### Module 1: Two-Bus System Voltage Profiles & Reactive Compensation
*   **Grid Layout:** Symmetrical 150kV radial link connecting a generation slack bus to a heavy commercial/industrial $PQ$ load[cite: 5].
*   **Engineering Analysis:**
    *   **Load Characterization:** Evaluated grid behavior across a scaled load ramp up to $P_{D2} = 4.0\text{ pu}$ with a constant power factor ($\tan\phi = 0.3$)[cite: 5]. Tracked the mathematical non-linear voltage collapse ($U_2-P_{D2}$ curve) and transmission line losses ($P_{loss}$).
    *   **Transformer Tap Control:** Modeled an in-line Transformer Tap Changer ($t$). Proved that adjusting the tap ratio to $t = 0.95\text{ pu}$ optimally restores the load voltage profile back to $1.0\text{ pu}$, despite increasing net inline currents and active losses.
    *   **Shunt Capacitor Compensation:** Integrated a variable shunt capacitor bank ($b_k$) at the load bus. Comparative loss analytics ($P_{loss}-U_2$) proved that reactive shunt compensation minimizes line currents and mitigates losses much more efficiently than transformer tap optimization by optimizing the inline reactive power path.

### Module 2: Active Inter-Area Power Exchange Control (3-Area System)
*   **Grid Layout:** 3 interconnected control areas operating on a shared 150kV mesh network with rigid power transaction treaties (Area 1 committing to export 200 MW to Area 2).
*   **Engineering Analysis:**
    *   **Inadvertent Inter-Area Power Flows:** Demonstrated that standard generation dispatch ($P_{G4}$, $P_{G9}$) causes uncontracted loop flows through the parallel transmission paths of Area 3 due to Kirchhoff's Laws.
    *   **Economic Impact Evaluation:** Quantified the daily wheeling fees and auxiliary loss penalties ($C_{1\rightarrow3} = 1663.2\text{ €/day}$) imposed on Area 1 for using Area 3's infrastructure under uncompensated scheduling.
    *   **Phase-Shifting Transformer (PST) Optimization:** Modeled and tuned a Phase-Shifting Transformer on the $3-5$ tie-line. Proved that a phase shift setting of $\phi_{35} = -27.5^{\circ}$ fully confines the 200 MW transaction to the designated corridor, dropping loop flows through Area 3 to approximately 0 MW.

### Module 3: Network Security, Contingency Analysis & Corrective Actions (6-Bus System)
*   **Grid Layout:** Symmetrical 6-Bus meshed grid operating under a 100 MVA thermal ceiling constraint per transmission branch.
*   **Engineering Analysis:**
    *   **N-1 Contingency Event:** Simulated a catastrophic line outage (tripping of tie-line $4-6$), which severely forced the system into insecure operation, driving branch $2-4$ into a critical overcurrent/overload state ($S_{24} = 105.25\text{ MVA}$).
    *   **Generation Shift Sensitivity Factors (GSSF):** Calculated the exact power transfer sensitivity coefficients ($\frac{\partial S_{24}}{\partial P_{Gi}}$) for the available generation units via selective 10 MW generation steps:
        *   **Area 2 Sensitivity:** $\frac{\partial S_{24}}{\partial P_{G2}} = 0.177$
        *   **Area 6 Sensitivity:** $\frac{\partial S_{24}}{\partial P_{G6}} = 0.0776$
    *   **Optimal Corrective Dispatch:** Deployed the sensitivity matrices to resolve the violation. Executed a targeted generation reduction at Bus 2 ($\Delta P_{G2} = -29.54\text{ MW}$) combined with an automatic slack adjustment at Bus 1 ($\Delta P_{G1} = +29.41\text{ MW}$), bringing branch $2-4$ back within safe thermal operating boundaries ($S_{24} \le 100\text{ MVA}$) while minimizing generation redispatch costs.

---

## Technical Toolkit & Analytical Tools
*   **Grid Modeling Software:** PowerWorld Simulator (PWRFLOW Tool)[cite: 5]
*   **Mathematical Formulations:** Newton-Raphson Load Flow, Generation Sensitivity Factors (GSSF), Inter-Area Power Exchange Controls
*   **Data Vis & Visualization:** Custom voltage-load ($U-P$), loss-load ($P_{loss}-P$), and tap-loss curves plotted via Excel backend data matrices.

---

└── 03_Six_Bus_N-1_Contingency/
    ├── Six_Bus_Contingency.pwb
    └── Sensitivity_Matrix_Corrective_Action.xlsx
