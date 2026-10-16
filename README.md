# RobustBART simulation code

This repository contains the simulation and biomass case-study code accompanying **“An Adaptive Weighted BART Framework for Robust Regression under Contamination.”**

The code covers Case 1 and Case 2 under four contamination distributions and two clean-data proportions. Each included scenario uses 200 Monte Carlo replications.

## Simulation design covered

| Case | Contamination distribution | Clean proportion |
|---|---|---|
| Case 1 | Normal, Student t(3), centered chi-square(6), centered exponential | 0.55 and 0.95 |
| Case 2 | Normal, Student t(3), centered chi-square(6), centered exponential | 0.55 and 0.95 |

The scripts compare default BART, BART(O), BART(H), BART(B), random forest, and support vector regression using MAPE and MAE. They also save selected parameter estimates and computation times.

## Repository structure

```text
RobustBART_GitHub_Case12/
├── code/
│   ├── Case1/
│   └── Case2/
├── realdata/
│   ├── Func1.R
│   └── realdata_biomass.R
├── results/
├── install_packages.R
├── run_all.R
├── run_realdata.R
├── VALIDATION_NOTES.md
├── CITATION.cff
└── README.md
```

Each scenario folder contains its simulation script and a local copy of `Func1.R`. The `Func1.R` copies are identical and are retained in each folder so that the original relative `source("Func1.R")` call continues to work.

## Requirements

- R 4.2 or later is recommended.
- A working Java/JDK installation is required by `bartMachine`.
- Required R packages: `EnvStats`, `bartMachine`, `MLmetrics`, `quantreg`, `boot`, `randomForest`, `e1071`, and `modeldata`.

Install any missing packages from the repository root:

```sh
Rscript install_packages.R
```

## Run one scenario

Run a script from its own scenario directory because it loads the local `Func1.R`. For example:

```sh
cd code/Case1/Case1+normal
Rscript 095.R
```

The resulting `.RData` file is written to that scenario directory. Generated `.RData` files are excluded from Git tracking.

## Run all scenarios

From the repository root:

```sh
Rscript run_all.R
```

This sequentially runs all 16 scenarios, copies their output files into `results/` using unambiguous filenames, and writes `results/sessionInfo.txt`. The complete run can be computationally expensive because it fits several models in each of 3,200 Monte Carlo replications.

## Run the biomass case study

The biomass data are loaded from the public `biomass` dataset in the R package `modeldata`; no separate data download is required. From the repository root, run:

```sh
Rscript run_realdata.R
```

This runs the random-attack analysis and copies the resulting workspace to `results/biomass_random_attack.RData`. The analysis uses the training subset, a 10% attack proportion, random seed `111`, and 200 repetitions.

The case study has its own `realdata/Func1.R`. It is intentionally kept separate because it differs from the function file supplied with the simulation code.

## Random seed and replications

Every analysis uses random seed `111`. All repository scripts use 200 replications. The supplied `Case1/Case1+t/t095.R` and `realdata/realdata_biomass.R` files used 100 replications; both were changed to 200 here to make the code consistent with the manuscript. The obsolete 100-repetition copies are not included in the public repository to avoid ambiguity.

## Reproducibility note

Please read [`VALIDATION_NOTES.md`](VALIDATION_NOTES.md) before publication. In particular, the supplied simulation and biomass scripts generate `X` once before the replication loop and then modify it inside the loop without resetting it. This behavior has been preserved because changing it may alter the reported numerical results and requires confirmation by the authors.

## Scope

This package contains the Case 1 and Case 2 simulations and the biomass random-attack analysis supplied by the authors. It does not contain code that formats the final manuscript tables and figures.

## Citation

Citation metadata are provided in [`CITATION.cff`](CITATION.cff), allowing GitHub to display a **Cite this repository** button.

## License

No software license is included. The authors should select an appropriate license before making the repository public. Without a license, the default copyright restrictions apply.

## Intended repository

<https://github.com/ygwang2018/RobustBART>
