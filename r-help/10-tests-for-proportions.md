# R resources for Chapter 10 (Tests for Proportions)

As with confidence intervals, we need the sample size, `n`, and the sample proportion, `p.hat`:

	> survey <- read.csv("~/Desktop/survey.csv")
	> n <- length(survey$voting)
	> k <- sum(survey$voting == "yes, in Texas"))  
	> p.hat <- k/n

Suppose we want to test ![H_0 : p=0.6](http://chart.apis.google.com/chart?cht=tx&chl=p=0.6) vs ![H_0 : p\\neq0.6](http://chart.apis.google.com/chart?cht=tx&chl=p<0.6)  (lower-tail test): 

	> p0 <- 0.6
	> SD.p <- sqrt(p0*(1-p0)/n)
	> ts.z <- (p.hat - p0)/SD.p
	> p.val.lower <- pnorm(ts.z)

Suppose instead that we instead want to test ![H_0 : p=0.6](http://chart.apis.google.com/chart?cht=tx&chl=p=0.6) vs ![H_0 : p>0.6](http://chart.apis.google.com/chart?cht=tx&chl=p>0.6) (upper-tail test). In this case,

	> p.val.upper <- 1-pnorm(ts.z)
	
or
	
	> p.val.upper <- pnorm(ts.z,lower.tail=F) 
Finally, if we want to test ![H_0 : p=0.6](http://chart.apis.google.com/chart?cht=tx&chl=p=0.6) vs ![H_0 : p\\neq0.6](http://chart.apis.google.com/chart?cht=tx&chl=p<0.6) (two-tail test), we need to double the tail probability, so the P-value is either twice the lower P-value or twice the upper P-value.  One of these will be larger than 1 and the other is correct, so we can use the min function to choose the correct value and calculate the P-value as:

	> p.val.two <- min(2*pnorm(ts.z), 2*(pnorm(ts.z, lower.tail=F))

Instead of running through these calculations each time, we can also write our own function that automates this for us:

	ztest.p <- function(k,n,p0) {  
	  p.hat <- k/n  
	  SD <- sqrt(p0*(1-p0)/n)  
	  ts.z <- (p.hat - p0)/SD  
	  p.val.lower <- pnorm(ts.z)  
	  p.val.upper <- 1-pnorm(ts.z)   
	  list(test.statistic=ts.z,  
	       p.val.lower=p.val.lower,  
	       p.val.upper=p.val.upper,  
	       p.val.two=min(2*p.val.upper,2*p.val.lower)  
	  )  
	}