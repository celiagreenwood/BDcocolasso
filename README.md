
<!-- README.md is generated from README.Rmd. Please edit that file -->

# BDcocolasso

<!-- badges: start -->

[![Travis build
status](https://travis-ci.org/celiaescribe/BDcocolasso.svg?branch=master)](https://travis-ci.org/celiaescribe/BDcocolasso)
<!-- badges: end -->

R software package to implement sparse regression in high-dimensional
setting, with a small portion of covariates corrupted (that is to say
with additive error measure, or with missing data). This package
implements simple CoCoLasso algorithm, and a variation called
Block-Descent CoCoLasso, or BDCoCoLasso, for settings where only a small
percentage of the features are corrupted.

This package is based on the [CoCoLasso
algorithm](https://arxiv.org/pdf/1510.07123.pdf). CoCoLASSO requires a
computationally demanding positive semi-definite projection of the
covariance matrix for a high dimensional feature set. In our context
when there are corrupted and uncorrupted covariates, we take advantage
of the block descent minimization trick to develop a more efficient
algorithm. In an alternating block minimization algorithm, the CoCoLasso
corrections are used when updating corrupted coefficient vectors, and a
simple LASSO is used for the uncorrupted coefficient vectors. Both
subproblems are convex and hence a global solution can be obtained, even
though adaption of the cross-validation step requires care in this
setting where there are products of corrupted and uncorrupted matrices.

## Installation

``` r
install.packages("BDcocolasso")
```

And the development version from [GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("celiaescribe/BDcocolasso")
```

## Vignette

See the online vignette for details about the BDcoco model and example
usage of the functions.

## Model input

There exist two settings in which the BD-CoCoLasso can be used : in the
simple CoCoLasso version, and in the Block-Descent-CoCoLasso version.
The inputs vary according to the chosen setting, and according to the
chosen noise setting.

  - **CoCoLasso setting**: This method requires six inputs (let n be the
    number of observations and p the number of X variables):

<!-- end list -->

1.  **X**: n x p matrix of covariates. Can be high-dimensional, i.e., p
    \>\> n. Must be continuous or with binary categorical features. Can
    contain missing values in NA format in the missing data setting.
2.  **y**: a continuous response of length n.
3.  **n**: Number of samples
4.  **p**: Number of covariates
5.  **noise**: Type of noise setting. There are two possibilities :
    *additive* or *missing*. In the *additive* setting it is necessary
    to specify the *tau* parameter, corresponding to the standard
    deviation of the additive error matrix. In the *missing* setting,
    nothing has to be specified.
6.  **block**: Chosen setting. Here, *block* should be equal to *TRUE*.

<!-- end list -->

  - **BD-CoCoLasso setting**: This method requires six inputs (let n be
    the number of observations, p the number of X variables, p1 the
    number of uncorrupted variables and p2 the number of corrupted
    variables, with p1 + p2 = p):

<!-- end list -->

1.  **X**: n x p matrix of covariates. Can be high-dimensional, i.e., p
    \>\> n. Must be continuous or with binary categorical features. Can
    contain missing values in NA format in the missing data setting. The
    first p1 columns must correspond to the uncorrupted covariates, and
    the last p2 columns must correspond to the corrupted covariates.
2.  **y**: a continuous response of length n.
3.  **n**: Number of samples
4.  **p**: Number of covariates
5.  **p1**: Number of uncorrupted covariates
6.  **p2**: Number of corrupted covariates
7.  **noise**: Type of noise setting. There are two possibilities :
    *additive* or *missing*. In the *additive* setting it is necessary
    to specify the *tau* parameter, corresponding to the standard
    deviation of the additive error matrix. In the *missing* setting,
    nothing has to be specified.
8.  **block**: Chosen setting. Here, *block* should be equal to *TRUE*.

## Contact

email : celia.escribe@polytechnique.edu

## Credit

We based this R package on the following articles :

  - [Cocolasso for high dimensional error-in-variables
    regression](https://arxiv.org/pdf/1510.07123.pdf)
  - [High-dimensional regression with noisy and missing data: Provable
    guarantees with nonconvexity](https://arxiv.org/pdf/1109.3714.pdf)
