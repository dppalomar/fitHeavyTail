<!-- README.md is generated from README.Rmd. Please edit that file -->
This package provides several functions to estimate the mean and covariance matrix for multivariate iid time-series under heavy-tailed distributions commonly arising in financial data.

Installation
------------

``` r
# Installation from local file
install.packages(file.choose(), repos = NULL, type="source")

# Or from GitHub
# install.packages("devtools")
devtools::install_github("dppalomar/covHeavyTail")

# Get help
library(covHeavyTail)
help(package="covHeavyTail")
?momentsStudentt
```

Example
-------

This is a simple illustrative example:

``` r
#generate heavy-tailed data
N <- 40
T <- 100
mu <- rep(0,N)
nv <- 4
U <- t(mvtnorm::rmvnorm(n=round(0.7*N), sigma=0.1*diag(N)))
R_cov <- U %*% t(U) + diag(N)
X <- mvtnorm::rmvt(n=T, delta=mu, sigma=(nv-2)/nv*R_cov, df=nv)

#estimate mean and covariance matrix
res <- momentsStudentt(X)
norm(res$mu - mu, "2")
norm(colMeans(X) - mu, "2")
norm(res$cov - R_cov, "F")
norm(cov(X) - R_cov, "F")
```