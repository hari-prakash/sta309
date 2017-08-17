# R resources for Chapters 14 and 15 (Inference for Regression and Multiple Regression)

## Useful commands

Let's use our class survey data and build a simple regression model to predict pulse rate from height. The `lm` ("linear model") command is the workhorse of regression in R:

	> model <- lm(pulse ~ height, data=survey)

Adding the `data=survey` parameter means that our formula of "pulse ~ height" is kept easy to read.  Note if you look at the result of this command it just consists of the coefficients (slope and intercept). You can get the full regression output by using the summary command:

	> summary(model)

These results give estimates and SEs for each coefficient, as well as the corresponding t-statistic and p-value for testing the null hypothesis that the population value of that coefficient is 0.   You can also get 95% CIs for each parameter.  Other confidence levels (e.g. 99% instead of 95%) can be obtained by changing the level.

	> confint(model, level=0.95)

To get a predicted pulse rate for a new person, we can use the `predict.lm` command and provide the model we computed earlier:

	> predict.lm(model, data.frame(height=70), interval="prediction")

The result of this command will consists of columns `fit`, `lwr`, and `upr`.  `fit` gives the predicted pulse rate for a new person that has height 70 inches.  (`lwr`, `upr`) gives a 95% confidence interval (add e.g. `level=0.99` to get a 99% CI) for the predicted pulse rate of this new person.

To add a second predictor variable to our model, just add it to the formula you give to `lm`. For example, let's say we want to predict pulse rate from both height and hours of sleep:

	> model2 <- lm(pulse ~ height + sleep, data=survey)

If we want to make a prediction or get a prediction interval we need to make sure to include values for all of the predictors. For example, to predict the pulse rate of someone that is 71 inches tall and got 5 hours of sleep:

	> predict.lm(model2, list(height=71, sleep=5), interval="prediction")

Now let's add a third variable -- gender -- as a predictor. In regression, all variables must be quantitative, but we can deal with this by creating a new variable in our data set (let's call it "male") which is 1 for men and 0 for women:

	> survey$male <- ifelse(gender == "Male", 1, 0)

Then we can add the new male variable to the regression:

	> model3 <- lm(pulse ~ height + sleep + gender, data=survey)

And we can predict as before; for example, suppose we wanted to predict pulse for a woman with height 68 inches and 5 hours of sleep:

	predict.lm(model3, list(height=68, sleep=5, male=0), interval="prediction")

Note that we have to put in 0 for male because we are looking to make a prediction for a woman; if we were predicting pulse rate for a man we'd put in 1 for male.

We can check assumptions by using similar tools as we have used in the past. For example, to check that the residuals are normally distributed, we calculate the residuals and construct a Q-Q plot:

	> residuals <- residual(model)  
	> qqnorm(residuals)  
	> abline(mean(residuals), sd(residuals))

We can also check for linearity and heteroscedasticity by examining the residual plots for the X-variables and the predicted variables:

	> plot(survey$height, residual(model))
	> plot(predict(model), residual(model))
	> abline(0,0)