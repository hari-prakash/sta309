# R resources for Chapter 9 (Intervals for Proportions)

First let's run through the commands needed to calculate a confidence interval manually. Let's create a 95% confidence interval for the proportion of our class that is registered to vote in Texas.

	> survey <- read.csv("~/Desktop/survey.csv")  
	> n <- length(survey$voting)  
	> k <- sum(sum(survey$voting == "yes, in Texas"))  
	> p.hat <- k/n

Then we estimate the standard error.

	> standard.error <- sqrt(p.hat * (1 - p.hat) / n)

Since there are two tails of the normal distribution, the 95% confidence level would imply that 97.5% of the area should be in the lower tail of the normal distribution. Therefore, the critical value is given by `qnorm(.975)` and we can compute the margin of error:

	> margin.of.error <- qnorm(0.975) * standard.error

Combining it with the sample proportion, we obtain the confidence interval:

	> p.hat + c(-margin.of.error, margin.of.error)

Instead of running through these calculations each time, we can also write our own function that automates this for us:

	ci.prop <- function(k, n, conf.level=0.95) {  
	  critical.value <- qnorm(1 - (1 - conf.level) / 2)  
	  p.hat <- k / n  
	  standard.error <- sqrt(p.hat * (1 - p.hat) / n)  
	  margin.of.error <- critical.value * standard.error  
	  return(p.hat + c(-margin.of.error, margin.of.error))  
	}

This creates a function that takes three parameters, `k` (number of successes), `n` (number of trials), and `conf.level` (confidence level, which is set to 95% by default), and gives it the name `ci.prop`. The function does a number of calculations and then returns the confidence interval as a vector.  You can then use this function just like any other function in R.

Now we can just call our function. For example, to estimate a 90% CI for 40 successes out of 100 trials:

	> ci.prop(40, 100, 0.9)

Or to calculate a 95% CI, we can omit the last parameter because it is 95% by default:

	> ci.prop(40, 100)

To find the required sample size for a confidence interval with a particular margin of error, we use the formula:

![formula](http://chart.apis.google.com/chart?cht=tx&chl=n=p(1-p)\left(\frac{z_*}{\text{ME}}\right)^2)

Typically, p is unknown so we use 0.5.  As above, z* is `qnorm(1 - (1 - conf.level) / 2)`. The result must always be rounded up to make sure that the sample size is adequate.