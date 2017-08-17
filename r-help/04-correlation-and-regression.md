# R resources for Chapter 4 (Correlation and Regression)

## Videos

*   [Scatterplots](http://www.youtube.com/embed/BnvYHqIptv4)
*   [Correlation](http://www.youtube.com/embed/GHYiLM6ZMEY)

## Useful commands

Let's use the bookstore example from HW 3.  For convenience, shorten the column names to Number and Sales and save the file as data1 before importing into R.

	> data1 <- read_excel("~/Downloads/data1.xlsx")

Now we can make a scatterplot, and label the axes:

	> plot(data1$Number, data1$Sales, xlab="Number of salespeople working", ylab="Sales, in $1000s")

We can also calculate the correlation:

	> cor(data1$Number,data1$Sales)

If we want to calculate the best fit line, we can ask R to build a linear model:

	> model <- lm(data1$Sales ~ data$Number)

We can get the slope and intercept of the best fit line by looking at this model:

	> model

And we can use the abline function to overlay the best fit line on the scatterplot:

	> plot(data$Number, data$Sales, xlab="Number of salespeople working", ylab="Sales, in $1000s")  
	> abline(model)

We can also calculate the residuals and create a residuals plot to check assumptions:

	> residuals <- resid(model)  
	> plot(data$Number, residuals)  
	> abline(0, 0)

(That last command adds a horizontal line at Y = 0 to help you more easily check whether there is a trend in the residual plot.)