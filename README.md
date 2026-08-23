# Monte Carlo Sensitivity

Monte Carlo simulation is the standard device for propagating uncertainty into investment appraisal, yet the applied literature routinely makes three modelling choices without justification: the distribution family assigned to the inputs, the independence assumption between them, and the number of iterations. This repository quantifies how far these choices move the reported conclusion of a feasibility study. A controlled experiment on a canonical cash flow varies the distribution family, the coefficient of variation of the elicitation, the correlation between revenue and cost, and the hurdle rate, one factor at a time and then in selected pairs, all under common random numbers. A companion analytical model exploits the linearity of net present value to deliver closed forms for the first two moments in every cell, which serve both to interpret the simulated effects and to validate the implementation. Expected NPV proves robust to the distribution family, varying by less than 9% across extremes, whereas the probability of infeasibility shifts by 11.8 percentage points between the PERT and uniform readings of the very same three elicited points. A paired design with matched moments attributes 83% of that shift to the variance each family implicitly imposes and only 17% to its shape. The code reproduces every table and every figure of the paper.

## Requirements

Our experiments have been performed using Python 3.12.3 and Jupyter Notebook. The following modules are required to run the experiment:

* NumPy 2.4.4 (https://numpy.org/)
* SciPy 1.17.1 (https://scipy.org/)
* Matplotlib 3.10.8 (https://matplotlib.org/)

No further dependencies are needed. The code is fully vectorised and never loops over the `N = 100,000` replications, so the whole experiment runs in seconds on a personal computer.

## Running the experiment

1. Clone this repository directly from terminal:

       $ git clone https://github.com/gpmq-uenp/Monte-Carlo-Sensitivity.git
       OR
       Download the .zip file and decompress it.

2. Install the required modules:

       $ pip install numpy scipy matplotlib

3. Open the notebook:

       $ jupyter notebook MonteCarloSensitivity.ipynb

4. Run the cells in order. Cell 0 defines the shared core and must be executed before cells 1 and 3 to 6. Cells 2 and 7 are self-contained and run on their own.

   | cell | output |
   |---|---|
   | 0 | shared core: elicitation, annuity factor, the four inverse transforms, exact moment functions, input generator and NPV routines |
   | 1 | Axis 1, pairing A — distribution family under the same elicited points |
   | 2 | Axis 1, pairing B — families re-elicited to matched moments |
   | 3 | Axis 2 — magnitude of the uncertainty, calibrated by coefficient of variation |
   | 4 | Axis 3 — correlation between revenue and cost, via a Gaussian copula |
   | 5 | Axis 4 — hurdle rate, using the NPV/IRR identity of Proposition 2 |
   | 6 | selected interactions: family × CV and correlation × CV |
   | 7 | the five figures of the paper, written to `figures/` |

5. Enter the project's `figures/` folder and check out the results.

## Reproducibility

The master seed is fixed at `2026` and reset at the start of each comparable treatment, so that all families and all correlation levels are driven by the same random numbers: any difference between two treatments is attributable to the modelling choice and not to sampling variability. Every cell of the design has an exact closed-form benchmark, and the simulated moments are checked against those analytical values rather than merely reported. No empirical data are used — the canonical project is synthetic and fully specified in the paper, so the study is reproducible from this repository alone.

## Cite as

Sozzo, B.T.S.; Souza, R.S.; Naozuka, G.T. How much do modelling choices move the risk estimate? Distribution family, dependence and hurdle rate in investment appraisal. *Computational Economics* (under review).

Sozzo, B.T.S.; Souza, R.S.; Naozuka, G.T. Monte Carlo Sensitivity, 2026. Version 1.0. Available online: https://github.com/gpmq-uenp/Monte-Carlo-Sensitivity (accessed on 23 August 2026), doi: https://doi.org/10.5281/zenodo.22073342

