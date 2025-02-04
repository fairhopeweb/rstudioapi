
<!-- README.md is generated from README.Rmd. Please edit that file -->

# rstudioapi <a href='https://rstudio.github.io/rstudioapi/'><img src='man/figures/logo.png' align="right" height="139" /></a>

<!-- badges: start -->

[![CRAN
status](https://www.r-pkg.org/badges/version/rstudioapi)](https://CRAN.R-project.org/package=rstudioapi)
[![Codecov test
coverage](https://codecov.io/gh/rstudio/rstudioapi/branch/main/graph/badge.svg)](https://codecov.io/gh/rstudio/rstudioapi?branch=main)
[![R-CMD-check](https://github.com/rstudio/rstudioapi/workflows/R-CMD-check/badge.svg)](https://github.com/rstudio/rstudioapi/actions)
<!-- badges: end -->

The `rstudioapi` package is designed to make it easy to conditionally
access the [RStudio](https://rstudio.com/) API from CRAN packages,
avoiding any potential problems with `R CMD check`. This package
contains a handful of useful wrapper functions to access the API. To see
the functions that are currently available in the API, run
`help(package = "rstudioapi")`

## Installation

You can install the released version of `rstudioapi` from
[CRAN](https://CRAN.R-project.org) with:

``` r
install.packages("rstudioapi")
```

And the development version from [GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("rstudio/rstudioapi")
```

## Example

The `rstudioapi` package is designed to never be attached to your search
path. Always prefix function calls with `rstudioapi::`.

``` r
# Returns T/F
rstudioapi::isAvailable()
# Returns error if not available
rstudioapi::verifyAvailable()

# Optional argument allows you to specify version requirement
rstudioapi::isAvailable("0.99")
rstudioapi::verifyAvailable("0.99")

# Call an rstudio function
rstudioapi::callFun("viewer", "http://localhost:8080")

# This will raise an error if rstudio is not running, or the function
# is not found. To run a different function if it's not available,
# use exists
if (rstudioapi::hasFun("viewer")) {
  rstudioapi::callFun("viewer", "http://localhost:8080")
} else {
  browseURL("http://localhost:8080")
}

# You can use find to get the function. Throws an error if the function
# does not exist.
rstudioapi::findFun("viewer")

# You can also check version in exists and find
rstudioapi::findFun("viewer", 0.99)
rstudioapi::hasFun("viewer", 0.99)
```
