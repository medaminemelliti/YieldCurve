# YieldCurve

Reconstructing the Tunisian zero coupon yield curve from scratch using 
publicly available Tunisie Clearing data, bootstrapping, log-linear 
interpolation, Nelson-Siegel fitting and TC benchmark comparison.

Full methodology: [Medium article](https://medium.com/@medaminemelliti/building-tunisias-yield-curve-from-scratch-bootstrapping-interpolation-tc-benchmark-d68e397df9ce)

## What it does

- Loads daily bond data (BTCTs + BTAs) from Tunisie Clearing
- Bootstraps zero coupon discount factors from the short end (BTCTs) 
  to the long end (BTAs)
- Fits a Nelson-Siegel model on the bootstrapped rates
- Benchmarks the fitted curve against TC's published NS parameters

## Data

Three Excel files are required, all downloadable from Tunisie Clearing:

| File | Source |
|---|---|
| `data.xlsx` | Daily yield curve snapshot - tunisiayieldcurve.tn |
| `btct_ref.xlsx` | BTCT reference file - tunisieclearing.com |
| `bta_ref.xlsx` | BTA reference file - tunisieclearing.com |

## Requirements

```bash
pip install pandas numpy scipy matplotlib openpyxl
```

## Usage

```bash
jupyter notebook zc_curve.ipynb
```

Update the valuation date and filenames at the top of the notebook 
to run on a different date.

## Results (17/04/2026)

| | β0 | β1 | β2 | λ | RMSE |
|---|---|---|---|---|---|
| **Fitted** | 0.083918 | -0.016518 | 0.021123 | 0.7020 | 0.0191 bps |
| **TC** | 0.084459 | -0.017103 | 0.020044 | 0.7173 | 0.0238 bps |

54 instruments bootstrapped, 3 outliers removed.
