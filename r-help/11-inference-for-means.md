# R resources for Chapter 11 (Inference for Means)

## Videos

*   [Sampling distributions](https://www.youtube.com/embed/K-y77viwmkA)
*   [One-sample t-test](https://www.youtube.com/embed/GyFGfdG4aO4)

## Useful commands

Let's use our class survey data as before and examine the average number of hours students sleep.  First, let's try calculating the standard error and sample mean manually:

	> n <- length(survey$sleep)  
	> standard.error <- sd(survey$sleep) / sqrt(n)  
	> sample.mean <- mean(survey$sleep)

We can also calculate the critical value from the t-distribution. Note that we use 0.975 here just like we would use `qnorm(0.975)` to calculate the critical value for a 95% confidence interval of a proportion from the Normal distribution; the logic is the same here, but we are using the t distribution rather than a Normal distribution:

	> critical.value <- qt(0.975, df=n-1)

Now, we can construct a 95% confidence interval for the average number of hours students sleep:

	> ci <- sample.mean + critical.value * c(-standard.error, standard.error)

Now let's test the hypothesis that average student gets 8 hours of sleep.  So the null hypothesis is ![formula](http://chart.apis.google.com/chart?cht=tx&chl=\mu=8)  and the test statistic is:

	> mu0 <- 8  
	> ts.t <- (sample.mean - mu0) / standard.error

And we can compute the p-value (assuming we want to run a two-sided test) as:

	> 2 * pt(abs(ts.t), lower.tail=F, df=n-1)

R also automates this process for us!  All we have to do is to run the following command, which does all of the work for us:

	> t.test(survey$sleep, mu=8)

For one sided tests, use `alternative="less"` or `alternative="greater"`.  In this case, ignore the confidence interval provided.  If you want to use the confidence interval, it is not necessary to specify anything more than the data.  Use the `conf.level` if you want something other than the default value of 0.95. 

	> t.test(survey$sleep, conf.level=0.99)

To find the required sample size for a confidence interval with a particular margin of error, we use the formula:

![formula](http://chart.apis.google.com/chart?cht=tx&chl=n=\left(\frac{z*\sigma}{\text{ME}} \right)^2)

Typically, ![formula](http://chart.apis.google.com/chart?cht=tx&chl=\sigma) is unknown so we use an estimate obtained from a sample.  z* is equal to `qnorm(1 - (1 - conf.level) / 2)` The result must always be **rounded up** to make sure that the sample size is adequate.