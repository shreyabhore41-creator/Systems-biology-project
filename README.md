# Systems-biology-project
Development of an eight-compartment systems biology model to investigate the effects of CRISPR/Cas9 on tomato gene regulatory networks.
# CRISPR/Cas9 DNA Repair: An Eight-Compartment ODE Model

## Project Overview

This project develops an eight-compartment Ordinary Differential Equation (ODE) model to study the dynamics of CRISPR/Cas9-induced DNA double-strand break (DSB) formation and repair in tomato (*Solanum lycopersicum*).

The model explores how DNA molecules transition through different states following Cas9-induced cleavage, including Cas9 binding, direct and processed DNA breaks, precise repair, and different insertion/deletion outcomes.

The model was implemented in Python and compared with published experimental time-course data for three tomato genes: **Psy1, CRTISO, and PhyB2**.

## Objectives

- Understand CRISPR/Cas9-induced double-strand break formation and DNA repair.
- Develop an eight-compartment ODE model representing different DNA repair states.
- Simulate the dynamics of all eight compartments over 72 hours.
- Fit selected kinetic parameters using published experimental data.
- Compare model predictions with observed DNA integrity, DSB, and indel fractions.
- Evaluate the behaviour and limitations of the mathematical model.

## Eight-Compartment Model

The model consists of eight states representing the possible fates of DNA molecules:

| Symbol | Compartment | Description |
|---|---|---|
| S | Intact/Susceptible DNA | Uncut DNA not bound by Cas9 |
| E | Cas9-engaged DNA | DNA with Cas9 bound before cleavage |
| Id | Direct DSB | Break at the expected Cas9 cut position |
| Ip | Processed DSB | Break with altered DNA ends |
| R | Precisely Repaired DNA | DNA restored without sequence changes |
| Ins | Insertion | Accumulated insertion outcomes |
| Del | Deletion | Accumulated deletion outcomes |
| MH | Microhomology Deletion | Deletions mediated by microhomologous sequences |

The model describes transitions between these compartments using nine kinetic rate constants.

## Dataset

Experimental data were obtained from the supplementary Source Data associated with:

Ben-Tov et al. (2024), *Uncovering the dynamics of precise repair at CRISPR/Cas9-induced double-strand breaks*.

**Genes analysed:**
- Psy1
- CRTISO
- PhyB2

**Experimental time points:** 0, 6, 12, 24, 36, 48 and 72 hours.

The published dataset contains measurements of intact DNA, indels, direct DSBs and processed DSBs obtained using UMI-DSBseq.

The three observed categories used for model fitting were:
- Intact DNA
- Total DSBs
- Indels

## Methodology

1. **Data Preparation:** Experimental Source Data were loaded and processed using Pandas. Molecule counts were converted into fractions, and replicates were averaged at each time point.

2. **Model Development:** An eight-compartment ODE system was developed to represent Cas9 binding, cleavage, DNA-end processing, precise repair and indel formation.

3. **Parameter Fitting:** Three kinetic parameters (kon, kcut and kproc) were fitted using nonlinear least-squares optimisation with `scipy.optimize.least_squares`. The remaining six parameters were assigned assumed illustrative values.

4. **ODE Simulation:** The model was solved using `scipy.integrate.solve_ivp` over 72 hours.

5. **Model Evaluation:** Predicted values were compared with experimental observations using Root Mean Square Error (RMSE).

6. **Visualisation:** Time-course plots were generated to examine the behaviour of all eight compartments for the three genes.

## Technologies Used

- Python 3
- Jupyter Notebook
- NumPy
- Pandas
- SciPy
- Matplotlib
- openpyxl

## Results

The model reproduced the major trends observed in the experimental time-course data for all three genes.

### Model Fit (RMSE)

| Gene | RMSE |
|---|---:|
| Psy1 | 0.018 |
| CRTISO | 0.052 |
| PhyB2 | 0.050 |

Psy1 showed the closest agreement between model predictions and experimental observations.

The model predicted differences in DNA repair dynamics across the three genes, with PhyB2 showing the fastest depletion of the susceptible DNA compartment and Psy1 showing the slowest.

The predicted indel fractions at 72 hours were approximately:
- Psy1: 15.7%
- CRTISO: 41.7%
- PhyB2: 58.4%

The results also highlight the importance of precise DNA repair, which can restore the original sequence without leaving an indel.

## Limitations

- Only three of the nine kinetic parameters were fitted to experimental data.
- The remaining six rate constants were assumed.
- Individual internal compartments were not directly measured.
- The model assumes constant kinetic rates.
- Cell-cycle effects, chromatin state, cell death and Cas9 decay were not included.
- Insertions, deletions and microhomology-mediated deletions are modelled as accumulated outcomes.
- The model is deterministic and does not include parameter confidence intervals.

Therefore, the eight-compartment trajectories represent model predictions and hypotheses rather than direct experimental measurements.

## Future Directions

- Perform parameter sensitivity and identifiability analysis.
- Estimate additional kinetic parameters.
- Incorporate time-dependent Cas9 activity.
- Include direct DSB-to-indel transitions.
- Validate the model using higher-resolution 24-hour experimental data.
- Perform what-if simulations by changing cleavage and precise repair rates.

## Repository Contents

- `CRISPR_Cas9_project.ipynb` – Python implementation of the eight-compartment ODE model, data analysis, parameter fitting, simulations and visualisations.
- `README.md` – Project documentation.
- `.gitignore` – Files and directories excluded from version control.

## Reference

Ben-Tov, D., Mafessoni, F., Cucuy, A., Honig, A., Melamed-Bessudo, C., & Levy, A. A. (2024). Uncovering the dynamics of precise repair at CRISPR/Cas9-induced double-strand breaks. *Nature Communications*, 15, 5096.

https://doi.org/10.1038/s41467-024-49410-x

---

