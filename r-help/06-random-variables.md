# R resources for Chapter 6 (Random Variables)

Consider the Red Light example in HW 5.  Before importing the data into R, you can rename the columns X and Prob and rename the file data8.

	data8 <- read_excel("~/Downloads/data8.xlsx")

To calculate the expected value and standard deviation of a discrete random variable you can multiply two columns in a data.frame, make a new column for the data.frame, and use the sum and sqrt functions.

	> EX <- sum(data8$X*data8$Prob)  
	> data8$SqDeviation <- (data8$X-EX)^2  
	> VarX <- sum(data8$SqDeviation * data8$Prob)  
	> sqrt(VarX)  

Alternatively, you can define a vector of possible values and a vector of probabilities for the same calculation.

The sample function can be used for simulations.  For example if we wish to simulate 20 random dice throws, we could first define a vector with the numbers 1 through 6 and then use the sample function.  In the function we specify the elements from which to choose, the number of items to select, and `TRUE` (or `T`) to indicate that the sample is with replacement. 

	> die <- c(1, 2, 3, 4, 5, 6)  
	> sample(die, 20, TRUE)

 Suppose a student guesses on a multiple choice test with 23 questions and 4 choices for each question.  Then the number of question correct will be Binomial(23, 0.25).  The probability of getting exactly 10 questions correct can be found in R with dbinom(n, size, prob) which computes the probability distribution function.

	> dbinom(10, 23, 0.25)

The probability of getting 10 or fewer correct can be found by adding the results for 0 through 10 or with the pbinom function which computes the cumulative probability function.  The following lines give the exact same result.

	> sum(dbinom(0:10, 23, 0.25))  
	> pbinom(10, 23, 0.25)

If we want to simulate the results of a 1000 students who guess on this test, we can use the rbinom(n, size, prob) function which computes random values.

	> results <- rbinom(1000, 23, 0.25)

If we want to simulate the question by question results for one student's guessing on the 23 question test, we use the `rbinom` function, but with n=23 and size=1.

	> rbinom(23, 1, 0.25)