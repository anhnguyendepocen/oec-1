
<!-- README.md is generated from README.Rmd. Please edit that file -->
OEC R package <img src="http://pacha.hk/oec-r-package/observatory.png" width=150 align="right" alt="sticker"/>
==============================================================================================================

[![mitlicense](https://img.shields.io/badge/License-MIT-green.svg)](https://opensource.org/licenses/MIT) [![Build Status](https://travis-ci.org/pachamaltese/oec.svg?branch=master)](https://travis-ci.org/pachamaltese/oec) [![Build status](https://ci.appveyor.com/api/projects/status/5xvlffxy8ro4wc34?svg=true)](https://ci.appveyor.com/project/pachamaltese/oec) [![cran checks](https://cranchecks.info/badges/summary/oec)](https://cran.r-project.org/web/checks/check_results_oec.html) [![CRAN downloads](http://cranlogs.r-pkg.org/badges/oec)](http://cran.rstudio.com/web/packages/oec/index.html) [![CRAN downloads](http://cranlogs.r-pkg.org/badges/grand-total/oec)](http://cran.rstudio.com/web/packages/oec/index.html) [![Coverage status](https://codecov.io/gh/observatory-economic-complexity/oec-r-package/branch/master/graph/badge.svg)](https://codecov.io/github/observatory-economic-complexity/oec-r-package?branch=master)

`oec` provides an easy way to obtain data from the [Observatory of Economic Complexity](http://atlas.media.mit.edu/en/) by accessing its API.

Installation
------------

``` r
# Install release version from CRAN
install.packages("oec")

# Install development version from GitHub
devtools::install_github("pachamaltese/oec-r-package")
```

Usage
-----

Please read the vignette for a detailed user guide.

``` r
library(oec)

# What does Chile exchange with China?  
# year 2015 - SITC (4 characters)
getdata("chl", "chn", 2015)

# What does Chile exchange with China?  
# years 2010 to 2015 - SITC (4 characters)
getdata_batch("chl", "chn", 2010, 2015)
```

This package features a full pkgdown site [here](http.//pacha.hk/oec/docs/).

Maelle' s initial feedback
--------------------------

### Code

-   \[x\] You use assign in functions instead of returning output. Please return output, you don't need to use assign here.
-   \[x\] Why do you use rm inside a function? *fixed, it was a bad try to make lighter function calls*
-   \[x\] There is a separate file containing imports (confusingly called exports wink). It'd be easier to see where functions are imported from if you used the syntax jsonlite::fromJSON. You could then remove the separate R code with imports. <http://r-pkgs.had.co.nz/namespace.html#imports>
-   \[x\] Your package depends on purrr for a single function. Consider replacing it with do.call and rbind. *To (over)simplify now I also use purrr's flatten df function*
-   \[x\] Regarding all the stopifnot, have informative error messages when the user entered a wrong parameter value.
-   \[x\] You could have a single exported function instead of two if I follow correctly? It'd take arguments like the batch one, that could be vector of length 1 (the user would input say one or several country pairs). The other function would be an utility function, that wouldn't need to be exported. It might simplify the interface?
-   \[x\] If there is only one function call in a pipeline it might be clearer to remove the pipe.

<!-- -->

    origin_destination <- origin_destination %>%
        mutate(trade_exchange_val = 
    !!sym("export_val") + !!sym("import_val"))

would become

    origin_destination <-  mutate(origin_destination,
        trade_exchange_val = !!sym("export_val") + !!sym("import_val"))

-   \[x\] In case you might ignore it, and in case it could be useful, there's a countrycode package. *the OEC uses an ISO modification, so countrycode would complicate this*

### Data

-   \[x\] Where do the data files in data come from? Why are they pre-prepared, are you sure they won't be updated? *everything in data/ comes from atlas.media.mit.edu and corresponds to unaltered trade codes (i.e HS96 was created not to touch HS92 created in 1992, HS02 was an update to HS96, etc so these tables do not change*
-   \[ \] You could keep their data processing in data-raw. *ok, I'll add a vignette to explain the changes*

### Documentation

-   \[x\] Please add the URL to the data source.
-   \[x\] Are you allowed to use the logo in your README? *yes, I' m a part of the original team*
-   \[ \] A flowchart of what processing your package does might be useful to explain the added value of using the package and to explain what has been preprocessed or not (what's being downloaded vs what's in data/).
-   \[x\] In the README when mentioning the vignette have a link to the pkgdown website.
-   \[ \] Please add @return fields to the documentation of the functions.
-   \[ \] A vignette with an actual use case, and visualizations, would be nice (or an extension of the existing vignette).
-   \[ \] Please explain what the data is e.g. SITC or add an external link.
-   \[ \] Because some chunks of the vignette are unevaluated without a pre-generated output, I can't understand what the "problem" is. You could pre-generate the output.

### Misc

-   \[x\] Could you rename the repo "oec" like the package? *travis also renamed*
-   \[x\] The "Maintainer" field in DESCRIPTION is useless because it'll be generated automatically from Authors.
-   \[x\] What are the files .Rapp.history in data/ and .build.timestamp in vignettes/? *temp files from R CMD, ok now*
-   \[x\] Please add a code coverage integration and badge (via e.g. usethis::usethis::use\_coverage())

The MIT License
---------------

Copyright (c) 2016, Mauricio "Pachá" Vargas

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
