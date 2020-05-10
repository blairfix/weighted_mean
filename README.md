# weighted_mean

`weighted_mean` is an R function that calculates the weighted mean of a vector, given another vector of weights.


### Inputs

* `x` = a vector of values that you want to average
* `weights` =  the associated weights

### Output
`weighted_mean` returns the mean of `x` weighted by `weights`.


### Example:

```R
library(RcppArmadillo)
library(Rcpp)

sourceCpp("weighted_mean.cpp")

x = c(1, 5, 10)
weights = c(2, 10, 1)

# get weighted mean
weighted_mean(x, weights)

4.769231
```


### Installation
To use `weighted_mean`, install the following R packages:
 * [Rcpp](https://cran.r-project.org/web/packages/Rcpp/index.html) 
 * [RcppArmadillo](https://cran.r-project.org/web/packages/RcppArmadillo/index.html) 

Put the source code (`weighted_mean.cpp`) in the directory of your R script. Then source it with the command `sourceCpp('weighted_mean.cpp')`.


### Performance

Base R has a function for calculating the weighted mean: `weighted.mean`. So why would you use this alternative version? In a word, *speed*. `weighted_mean` is implemented in C++ and is about twice as fast as the base R version.


```R
library(microbenchmark)

x = rlnorm(10^6, 1, 1)
weights = rlnorm(10^6, 1, 1)

microbenchmark(
  weighted.mean = weighted.mean(x, weights),
  weighted_mean = weighted_mean(x, weights),
  times = 100
)


Unit: milliseconds
          expr       min        lq      mean    median        uq       max neval
 weighted.mean 15.716250 15.944238 19.917655 16.255049 23.987969 104.60258   100
 weighted_mean  6.202405  6.350673  7.690995  6.492289  9.782438  11.09623   100

```




