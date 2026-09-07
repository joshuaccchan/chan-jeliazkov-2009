# Chan and Jeliazkov (2009): MATLAB Examples

MATLAB code illustrating the precision sampler of:

> Chan, J. C. C. and Jeliazkov, I. (2009). Efficient Simulation and Integrated
> Likelihood Estimation in State Space Models. *International Journal of
> Mathematical Modelling and Numerical Optimisation*, 1(1/2), 101–120.

The paper develops a band-matrix precision sampler that simulates the latent
states of a linear Gaussian state space model in a single block, in place of
the filter–smoother recursions of the conventional Kalman approach. The three
scripts here apply that algorithm to state space models in common use in
macroeconomics. They illustrate the method; they do not replicate the results
in the paper.

The package distributed with the paper is archived separately, in
[bvar-toolkit](https://github.com/joshuaccchan/bvar-toolkit). The original
`sp_code` files are kept there verbatim under
[`replications/chan_jeliazkov2009_statespace/`](https://github.com/joshuaccchan/bvar-toolkit/tree/main/replications/chan_jeliazkov2009_statespace),
and
[`examples/ex01_precision_sampler.m`](https://github.com/joshuaccchan/bvar-toolkit/blob/main/examples/ex01_precision_sampler.m)
in the same repository derives the sampler from the banded precision matrix and
checks its draws against a Kalman smoother.

## Contents

| File                    | Description                                                                                                                |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| `UC.m`                  | Local-level unobserved components model (random-walk trend + iid noise) on US CPI inflation.                               |
| `linreg_tvp.m`          | Time-varying parameter regression of US PCE inflation on the output gap and lagged inflation (a TVP Phillips curve).        |
| `DFM.m`                 | Dynamic factor model with AR(1) factor dynamics, applied to FRED-MD macroeconomic series. The number of factors `r` is set near the top of the script.                    |
| `SURform.m`             | Helper used by `linreg_tvp.m` to build a stacked SUR design matrix.                                                         |
| `USCPI.csv`             | Monthly US CPI inflation data.                                                                                              |
| `USPCE_OutputGap.csv`   | Quarterly US PCE inflation and output gap.                                                                                  |
| `FRED-MD.csv`           | Monthly FRED-MD macroeconomic indicators.                                                                                   |

## Requirements

- MATLAB R2019b or later (uses `readmatrix` / `readtable`).
- Statistics and Machine Learning Toolbox (for `gamrnd`).

## Running

Open MATLAB in the repository directory and run any of:

```matlab
>> UC
>> linreg_tvp
>> DFM
```

Each script is self-contained. It loads its data, runs a Gibbs sampler of
10,000 or 20,000 draws after the burn-in period, drawing the states with the
precision sampler of the paper, and produces the figures that illustrate the
method. The seed is fixed at `rng(42)`, so the results are reproducible.

## Citation

```bibtex
@article{CJ09,
  author  = {Chan, J. C. C. and Jeliazkov, I.},
  title   = {Efficient Simulation and Integrated Likelihood Estimation in State Space Models},
  journal = {International Journal of Mathematical Modelling and Numerical Optimisation},
  volume  = {1},
  number  = {1/2},
  pages   = {101--120},
  year    = {2009}
}
```

## License

MIT — see [LICENSE](LICENSE).
