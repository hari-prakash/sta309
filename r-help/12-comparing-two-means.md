# R resources for Chapter 12 (Comparing Two Means)

## Videos

*   [Paired t-test](http://www.youtube.com/embed/wo6DzjpQ5Oc)
*   [Independent t-test](http://www.youtube.com/embed/EKiX4-aHVa4)

## Useful commands

The `t.test` function can be used for one sample, paired, and tests for two independent samples.

Paired t-tests can be done with a **one sample test** on differences. For one sided tests, use `alternative="less"` or `alternative="greater"`. If you use a one-sided test, ignore the provided confidence interval.

First create a new variable with the differences:

	> Diet$difference <- Diet$`Loss at 6 Months_Atkins` - Diet$`Loss at 12 Months_Atkins`

Then use the t.test function with only one variable (the differences):

	> t.test(Diet$difference, mu=0)

To do a **matched pairs test**, you may also specify two variables and the option `paired=T`. 

	> t.test(Diet$`Loss at 6 Months_Atkins`,Diet$`Loss at 12 Months_Atkins`, paired=T)  

To do a test with **two independent samples**, provide two variables without the `paired` option (or specify `paired=F`):

	> t.test(Diet$`Loss at 6 Months_Atkins`,Diet$`Loss at 6 Months_Conventional`, alternative="greater")  
