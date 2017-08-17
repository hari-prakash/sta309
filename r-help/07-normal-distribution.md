# R resources for Chapter 7 (Normal Distribution)

The cumulative probability function is pnorm(q, mean, sd) finds the probability to the left of the value q.  So, if the distribution of women's heights is Normal with mean equal 66 and standard deviation equal to 2.5, we can use the function to find the proportion of women who are below 5' (or 60" tall).

	> pnorm(60, 66, 2.5)

The quantile function `qnorm(p, mean, sd)` is the inverse of the pnorm function and is used to find percentiles. For example if heights are normally distributed with a mean of 66 and a standard deviation of 2.5, then we can find the height separating the lower 90% and the top 10% with

	> qnorm(0.9, 66, 2.5)

The `rnorm(n, mean, sd)` function is used for simulating values from a Normal distribution.  To create a vector of 100 values from the height distribution, use

	> heights <- rnorm(100, 66, 2.5)

 The `qqnorm` function produces a normal probability plot and abline function will add the diagonal line to the plot as follows.

	> qqnorm(heights)  
	> abline(mean(heights), sd(heights))

Skewness and kurtosis are functions available in the `moments` package.  To use the function, you must first install the package.

	> install.packages("moments")  
	> library(moments)  
	> skewness(heights)  
	> kurtosis(heights)

(You only need to run `install.packages` once for the `moments` package; after that, you can jump right to running `library(moments)`.)

If you have missing data, include `na.rm=T` as an option in the `skewness` and `kurtosis` functions so R ignores the missing data (if you omit the `na.rm=T` option then R will return `NA` as the result of `skewness` or `kurtosis`.