# R resources for Chapter 3 (Quantitative Data)

## Videos

*   [Displaying Univariate Data](http://www.youtube.com/embed/raEYhaV08_4)
*   [Histograms for Different Groups](http://www.youtube.com/embed/jBLdWuRVR74)
*   [Univariate Descriptive Statistics](http://www.youtube.com/embed/CKB80iT6Qlk)
*   [Boxplots](http://www.youtube.com/embed/fw5qyHpswXQ)

## Useful commands

Let's use the Internet Music example from HW2. Click on the data icon, and Open in Excel.  From R, import the dataset from Excel.  Be sure to uncheck "First Row as Names."

	> data <- read_excel("~/Desktop/InternetMusic.xlsx", header=F)

Note that we need to add `header=F` because the first line of the file is actual data, not the name of the column. Note that since this column of data has no headers, R automatically calls it `X0`.

Create a histogram:

	> hist(data$X0)

By default, a histogram will show counts.  

This histogram may not match up exactly with the histograms in MyStatLab, because (1) R may select different bin sizes and (2) R by default may use a different rule than MyStatLab about what to do with values on the boundary between two bins. To make R's boundary rules match MyStatLab's, add `include.lowest=F` and `right=F` as parameters to the hist function. To make the bins match MyStatLab's, you can pass a sequence of bin boundary points to R:

	> hist(data$X0, breaks=c(0,10,20,30,40,50), include.lowest=F, right=F)

As a shortcut, you can also use the `seq` command, so you don't have to type out every boundary; for example, `seq(0,50,10)` generates a sequence from 0 to 50 skipping by 10s:

	> hist(data$X0, breaks=seq(0,50,10), include.lowest=F, right=F)

We can also get descriptive statistics:

	> mean(data$X0)
	> median(data$X0)
	> sd(data$X0)  
	> fivenum(data$X0)
	> summary(data$X0)

Note that different software uses different algorithms to compute quartiles.  Even the quartiles computed by the `fivenum` and `summary` functions in R are not the same. Use `fivenum` for the homework.

When computing z-scores, note that if you apply a numeric operation to a vector, the operation will be applied to every element of that vector. For example:

	> vector <- c(1,2,3,4,5)  
	> 2*vector  
	> vector+1

The min and max functions may be helpful:

	> min(vector)  
	> max(vector)

If you need a refresher on how vectors work in R, see the [Vectors](http://www.youtube.com/embed/o_L_Q48KxC0) video.

Make a boxplot:

	> boxplot(data$X0)

Make a stem-and-leaf plot:

	> stem(data$X0)

Now let's look at a time series plot. Let's import the hurricane data from the homework:

	> data <- read.csv("~/Desktop/Hurricanes.csv")

Note that since the second column is called "#", which is not a valid R column name, R imports it as X. (you can see this by typing `View(data)`).

We can make a time series plot by using the plot command and passing type="l" as a parameter:

	> plot(data$X., type="l")
