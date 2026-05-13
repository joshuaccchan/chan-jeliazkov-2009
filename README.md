# Chan and Jeliazkov (2009): MATLAB Examples

MATLAB code illustrating the precision sampler from:

> Chan, J. C. C. and Jeliazkov, I. (2009). Efficient Simulation and Integrated
> Likelihood Estimation in State Space Models. *International Journal of
> Mathematical Modelling and Numerical Optimisation*, 1(1/2), 101–120.

The paper develops a sparse / band-matrix precision sampler that simulates
the latent states of a linear Gaussian state space model in one block,
avoiding the filter–smoother recursions of the conventional Kalman approach.
The three scripts below are stand-alone applications of that algorithm to
state space models commonly used in macroeconomics; they are not
replications of the paper itself.

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

Open MATLAB in the repo directory and run any of:

```matlab
>> UC
>> linreg_tvp
>> DFM
```

Each script is self-contained: it loads its data, runs a Gibbs sampler
(10,000 or 20,000 post-burn-in draws using the precision sampler from the
paper), and produces the figures used to illustrate the method. The random
seed is fixed (`rng(42)`) so results are reproducible across runs.

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
