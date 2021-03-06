[![Travis build status](https://travis-ci.org/tidymodels/embed.svg?branch=master)](https://travis-ci.org/tidymodels/embed)
[![Coverage status](https://codecov.io/gh/tidymodels/embed/branch/master/graph/badge.svg)](https://codecov.io/github/tidymodels/embed?branch=master)
[![CRAN_Status_Badge](http://www.r-pkg.org/badges/version/embed)](http://cran.r-project.org/web/packages/embed)
[![Downloads](http://cranlogs.r-pkg.org/badges/embed)](http://cran.rstudio.com/package=embed)
![](https://img.shields.io/badge/lifecycle-experimental-orange.svg)


`embed` is a package that contains extra steps for the [`recipes`](http://cran.rstudio.com/package=recipes) package for embedding categorical predictors into one or more numeric columns. All of the preprocessing methods are _supervised_. 

These steps are contained in a separate package because the package dependencies, [`rstanarm`](http://cran.rstudio.com/package=rstanarm), [`lme4`](http://cran.rstudio.com/package=lme4), and [`keras`](http://cran.rstudio.com/package=keras),  are fairly heavy. 

The steps included are:

* `step_lencode_glm`, `step_lencode_bayes`, and `step_lencode_mixed` estimate the effect of each of the factor levels on the outcome and these estimates are used as the new encoding. The estimates are estimated by a generalized linear model. This step can be executed without pooling (via `glm`) or with partial pooling (`stan_glm` or `lmer`). Currently implemented for numeric and two-class outcomes. 

* `step_embed` uses `keras::layer_embedding` to translate the original _C_ factor levels into a set of _D_ new variables (< _C_). The model fitting routine optimizes which factor levels are mapped to each of the new variables as well as the corresponding regression coefficients (i.e., neural network weights) that will be used as the new encodings.  

Some references for these methods are:

* Francois C and Allaire JJ (2018) [_Deep Learning with R_](https://www.manning.com/books/deep-learning-with-r), Manning
* Guo, C and Berkhahn F (2016) "[Entity Embeddings of Categorical Variables](https://arxiv.org/abs/1604.06737)"
* Micci-Barreca D (2001) "A preprocessing scheme for high-cardinality categorical attributes in classification and prediction problems," ACM SIGKDD Explorations Newsletter, 3(1), 27-32.
* Zumel N and Mount J (2017) "[`vtreat`: a `data.frame` Processor for Predictive Modeling](https://arxiv.org/abs/1611.09477)"


To install the package:

```r
install.packages("embed")

## for development version:
require("devtools")
install_github("tidymodels/embed")
```
