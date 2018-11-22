---
title: 'Chapter 1'
description: 'Chapter description goes here.'
---

## Data preparation

```yaml
type: NormalExercise
key: 2bafef99a3
lang: r
xp: 100
skills: 1
```

The CASchools dataset is already loaded. It contains data on test performance, school characteristics, and student demographic backgrounds. The data used here are from all 420 K-6 and K-8 districts in California with data available for 1998 and 1999. Test scores are the average of the reading and math scores on the Stanford 9 standardized test administered to schools students. School characteristics include enrollment, number of teachers, number of computers per classroom, and expenditures per student. The demographic variables include the percentage of students in the public assistance program, the percentage of students that qualify for a reduced price lunch, and the percentage of students that are English Learners.

`@instructions`
1) Add a variable stratio to the dataset CASchools defined as students/teachers.

2) Add a variable score to the dataset CASchools defined as the average of math and read.

3) Obtain summary statistics for all variables in the dataset CASchools.

`@hint`


`@pre_exercise_code`
```{r}
CASchools <- read.table("http://assets.datacamp.com/production/repositories/4109/datasets/58d484cd9aa9884502caf2e43cd1db69ab569f89/CASchools.txt")
```

`@sample_code`
```{r}
#1 Add a variable stratio to the dataset CASchools defined as students/teachers.
CASchools$stratio <- 

#2 Add a variable score to the dataset CASchools defined as the average of math and read.


#3 Obtain summary statistics for all variables in the dataset CASchools.

```

`@solution`
```{r}
#1 Add a variable stratio to the dataset CASchools defined as students/teachers.
CASchools$stratio <- CASchools$students/CASchools$teachers

#2 Add a variable score to the dataset CASchools defined as the average of math and read.
CASchools$score <- (CASchools$math + CASchools$read)/2

#3 Obtain summary statistics for all variables in the dataset CASchools.
summary(CASchools)

```

`@sct`
```{r}

```

---

## Simple regression

```yaml
type: TabExercise
key: 171fc033c6
xp: 100
```

We will now estimate the simple linear regression of score on stratio and we will assess the validity of the linearity assumption.

`@pre_exercise_code`
```{r}
CASchools <- read.table("http://assets.datacamp.com/production/repositories/4109/datasets/58d484cd9aa9884502caf2e43cd1db69ab569f89/CASchools.txt")
CASchools$stratio <- CASchools$students/CASchools$teachers
CASchools$score <- (CASchools$math + CASchools$read)/2
source("http://assets.datacamp.com/production/repositories/4109/datasets/2452ec47ee5ae7d60fcadf8ab51780a5a0244e2c/resettest.R")
```

***

```yaml
type: NormalExercise
key: d6674928cf
xp: 20
```

`@instructions`
Regress score on stratio (the variables are in the dataset CASchools) and save the results in fit1.

`@hint`


`@sample_code`
```{r}

```

`@solution`
```{r}
fit1 <- lm(score~stratio, data=CASchools)
```

`@sct`
```{r}

```

***

```yaml
type: MultipleChoiceExercise
key: c4172bce65
xp: 20
```

`@question`
Assume that all assumptions of the clasical linear regression model are satisfied. What is the estimated effect of increasing the number of students in the class from 20 to 22 on the expected score?

`@possible_answers`
1. It increases by 2.2798. 
2. It decreases by 2.2798.
3. [It decreases by -4.5596.]
4. We are not able to respond.

`@hint`


`@sct`
```{r}

```

***

```yaml
type: NormalExercise
key: 11e9fc60e0
xp: 20
```

`@instructions`
A first step to assess the linearity assumption consists in plotting the dependent and independent variables and adding the regression line.

`@hint`
Use the function plot for the scatterplot. Use abline and lm for the regression line.

`@sample_code`
```{r}
fit1 <- lm(score~stratio, data=CASchools)
#Generate a scatterplot of the dependent variable (y-axis) and regressor (x-axis)


#Add a line for the fitted values

```

`@solution`
```{r}
fit1 <- lm(score~stratio, data=CASchools)
#Generate a scatterplot of the dependent variable (y-axis) and regressor (x-axis)
plot(score~stratio, data=CASchools)

#Add a line for the fitted values
abline(lm(score~stratio, data=CASchools))

```

`@sct`
```{r}

```

***

```yaml
type: NormalExercise
key: fdab4b7a92
xp: 20
```

`@instructions`
We now complete the graphical assessement with a formal test. Perform the RESET specification test for the regression fit1 and save the results in test1

`@hint`


`@sample_code`
```{r}
fit1 <- lm(score~stratio, data=CASchools)
#reset test:
test1 <- 
```

`@solution`
```{r}
fit1 <- lm(score~stratio, data=CASchools)
#reset test:
test1 <- resettest(lm(score~stratio, data=CASchools))
```

`@sct`
```{r}

```

***

```yaml
type: MultipleChoiceExercise
key: 61fc8a9ccd
xp: 20
```

`@question`
The result of the RESET test indicates that

`@possible_answers`
1. We can reject the null hypothesis that the model is correctly specified at the 5% significance level.
2. We can reject the null hypothesis that the model is misspecified at the 5% significance level.
3. [We cannot reject the null hypothesis that the model is correctly specified at the 5% significance level.]
4. We cannot reject the null hypothesis that the model is misspecified at the 5% significance level.

`@hint`


`@sct`
```{r}

```

---

## Nonparametric regression

```yaml
type: TabExercise
key: 7af7febd8a
xp: 100
```



`@pre_exercise_code`
```{r}
CASchools <- read.table("http://assets.datacamp.com/production/repositories/4109/datasets/58d484cd9aa9884502caf2e43cd1db69ab569f89/CASchools.txt")
CASchools$stratio <- CASchools$students/CASchools$teachers
CASchools$score <- (CASchools$math + CASchools$read)/2
```

***

```yaml
type: NormalExercise
key: 8dbc913032
xp: 20
```

`@instructions`
We will now estimate the same relationship with a local linear regression.

`@hint`
Try with the functions lines() and loess.smooth().

`@sample_code`
```{r}
plot(score~stratio, data=CASchools)
abline(lm(score~stratio, data=CASchools))
#add a line in red that show the fitted values of the local linear regression

```

`@solution`
```{r}
plot(score~stratio, data=CASchools)
abline(lm(score~stratio, data=CASchools))
#add a line in red that show the fitted values of the local linear regression
lines(loess.smooth(CASchools$stratio, CASchools$score), col="red")
```

`@sct`
```{r}

```

***

```yaml
type: NormalExercise
key: a05fe70964
xp: 20
```

`@instructions`
Estimate the local linear regression with the function loess().

`@hint`


`@sample_code`
```{r}
#Estimate the local linear regression of score on stratio
loe1 <- 
```

`@solution`
```{r}
#Estimate the local linear regression of score on stratio
loe1 <- loess(score~stratio, data=CASchools)
```

`@sct`
```{r}

```

***

```yaml
type: NormalExercise
key: cee55711de
xp: 20
```

`@instructions`
Calculate the predicted values.

`@hint`


`@sample_code`
```{r}
#Estimate the local linear regression of score on stratio
loe1 <- loess(score~stratio, data=CASchools)
#Calculate the predicted values with their standard errors
ploe1 <- 
```

`@solution`
```{r}
#Estimate the local linear regression of score on stratio
loe1 <- loess(score~stratio, data=CASchools)
#Calculate the predicted values with their standard errors
ploe1 <- predict(loe1,se=TRUE)
```

`@sct`
```{r}

```

***

```yaml
type: NormalExercise
key: 434d5e30c3
xp: 20
```

`@instructions`
Calculate the confidence intervals.

`@hint`


`@sample_code`
```{r}
#Estimate the local linear regression of score on stratio
loe1 <- loess(score~stratio, data=CASchools)
#Calculate the predicted values with their standard errors
ploe1 <- predict(loe1,se=TRUE)
#Calculate the lower end of the 95% confidence interval
low_ci <- ploe1$fit-qnorm(0.975)*
high_ci <- 
```

`@solution`
```{r}
#Estimate the local linear regression of score on stratio
loe1 <- loess(score~stratio, data=CASchools)
#Calculate the predicted values with their standard errors
ploe1 <- predict(loe1,se=TRUE)
#Calculate the lower end of the 95% confidence interval
low_ci <- ploe1$fit-qnorm(0.975)*ploe1$se.fit
high_ci <- ploe1$fit+qnorm(0.975)*ploe1$se.fit
```

`@sct`
```{r}

```

***

```yaml
type: NormalExercise
key: 4614afb224
xp: 20
```

`@instructions`
Plot the fitted values with the confidence intervals.

`@hint`


`@sample_code`
```{r}
#Estimate the local linear regression of score on stratio
loe1 <- loess(score~stratio, data=CASchools)
#Calculate the predicted values with their standard errors
ploe1 <- predict(loe1,se=TRUE)
#Calculate the lower end of the 95% confidence interval
low_ci <- ploe1$fit-qnorm(0.975)*ploe1$se.fit
high_ci <- ploe1$fit+qnorm(0.975)*ploe1$se.fit
#calculate the ranks of the x variable
order1 <- order(loe1$x)
#scatterplot 
plot(score~stratio, data=CASchools)
#add a red line for the fitted values of the local linear regression

#blue lines for the ends of the confidence interval

```

`@solution`
```{r}
#Estimate the local linear regression of score on stratio
loe1 <- loess(score~stratio, data=CASchools)
#Calculate the predicted values with their standard errors
ploe1 <- predict(loe1,se=TRUE)
#Calculate the lower end of the 95% confidence interval
low_ci <- ploe1$fit-qnorm(0.975)*ploe1$se.fit
high_ci <- ploe1$fit+qnorm(0.975)*ploe1$se.fit
#calculate the ranks of the x variable
order1 <- order(loe1$x)
#scatterplot 
plot(score~stratio, data=CASchools)
#red line for the fitted values of the local linear regression
lines(ploe1$fit[order1]~loe1$x[order1],col="red")
#blue lines for the ends of the confidence interval
lines(low_ci[order1]~loe1$x[order1],col="blue")
lines(high_ci[order1]~loe1$x[order1],col="blue")
```

`@sct`
```{r}

```

---

## Multiple regression: linearity

```yaml
type: TabExercise
key: a3732e108e
xp: 100
```

We estimate now a multiple linear regression and assess the linearity assumption.

`@pre_exercise_code`
```{r}
CASchools <- read.table("http://assets.datacamp.com/production/repositories/4109/datasets/58d484cd9aa9884502caf2e43cd1db69ab569f89/CASchools.txt")
CASchools$stratio <- CASchools$students/CASchools$teachers
CASchools$score <- (CASchools$math + CASchools$read)/2
source("http://assets.datacamp.com/production/repositories/4109/datasets/2452ec47ee5ae7d60fcadf8ab51780a5a0244e2c/resettest.R")
```

***

```yaml
type: NormalExercise
key: aee3f8d597
xp: 10
```

`@instructions`
Regress score on a constant, stratio, and income. These variables are in the dataset CASchools. Save the regression result in fit2.

`@hint`


`@sample_code`
```{r}

```

`@solution`
```{r}
fit2 <- lm(score ~ stratio + income, data = CASchools)
```

`@sct`
```{r}

```

***

```yaml
type: NormalExercise
key: d95e25f8b9
xp: 10
```

`@instructions`
We want to assess the validity of the linearity assumption. Use the plot function with the correct avalue for the argument `which' in order

`@hint`


`@sample_code`
```{r}
fit2 <- lm(score ~ stratio + income, data = CASchools)
#model specification plot
plot(fit2, which= )
```

`@solution`
```{r}
fit2 <- lm(score ~ stratio + income, data = CASchools)
#model specification plot
plot(fit2, which= 1)
```

`@sct`
```{r}

```

***

```yaml
type: MultipleChoiceExercise
key: c83fe88108
xp: 10
```

`@question`
In this figure, do you find any evidence for the misspecification of the regression fit2?

`@possible_answers`
1. Everything looks fine. The mean of the residuals is close to zero.
2. The red line is not flat but I cannot conclude that the model is misspecified.
3. [The model is obviously misspecified. The red line is below zero in the tails and above zero in the middle.]

`@hint`


`@sct`
```{r}

```

***

```yaml
type: NormalExercise
key: c27d074a22
xp: 10
```

`@instructions`
Perform a formal test to test the null hypothesis that fit2 is misspecified.

`@hint`


`@sample_code`
```{r}
fit2 <- lm(score ~ stratio + income, data = CASchools)
#model specification test

```

`@solution`
```{r}
fit2 <- lm(score ~ stratio + income, data = CASchools)
#model specification test
resettest(fit2)
```

`@sct`
```{r}

```

***

```yaml
type: MultipleChoiceExercise
key: e486abfff6
xp: 10
```

`@question`
The model is clearly misspecified. What do you do?

`@possible_answers`
1. [I estimate a more flexible model.]
2. I collect more data.
3. I must use an instrumental variable.
4. I am sick of econometrics.

`@hint`


`@sct`
```{r}

```

***

```yaml
type: MultipleChoiceExercise
key: 6ccd95e3f1
xp: 10
```

`@question`
Use the console to plot the residuals as a function of stratio and then as a function of income. Which variable is more likely to cause the rejection of the linearity assumption?

`@possible_answers`
1. stratio
2. [income]
3. both
4. I see nothing nonlinear in the bivariate relationship. The problem must come from the omitted interaction.

`@hint`


`@sct`
```{r}

```

***

```yaml
type: NormalExercise
key: 03e21166b7
xp: 10
```

`@instructions`
We estimate now a more flexible model in income. Use the function poly to include a second order polynom in income as a regressor. The argument raw must be set to TRUE.

`@hint`


`@sample_code`
```{r}
#Add the correct arguments to the function poly:
fit3 <- lm(score ~ stratio + poly(income), data = CASchools)

#Test the validity of the linearity assumption for this model:

```

`@solution`
```{r}
#Add the correct arguments to the function poly:
fit3 <- lm(score ~ stratio + poly(income, 2, raw=TRUE), data = CASchools)

#Test the validity of the linearity assumption for this model:
resettest(fit3)
```

`@sct`
```{r}

```

***

```yaml
type: MultipleChoiceExercise
key: 834717f45b
xp: 10
```

`@question`
Is this model better? Are you satisfied?

`@possible_answers`
1. This model is great!
2. [This model is slightly better but I am still rejecting the null hypothesis that the model is correct at the 5% level.]
3. Include income to the power 2 did not improve the model at all.

`@hint`


`@sct`
```{r}

```

***

```yaml
type: NormalExercise
key: dfebdbcaa7
xp: 10
```

`@instructions`
We want to be really flexible in income and include powers of income up to the 4th term.

`@hint`


`@sample_code`
```{r}
#Add the correct arguments to the function poly:
fit4 <- lm(score ~ stratio + poly(income), data = CASchools)

#Test the validity of the linearity assumption for this model:

```

`@solution`
```{r}
#Add the correct arguments to the function poly:
fit4 <- lm(score ~ stratio + poly(income, 4, raw=TRUE), data = CASchools)

#Test the validity of the linearity assumption for this model:
resettest(fit4)
```

`@sct`
```{r}

```

***

```yaml
type: NormalExercise
key: f0f38264b3
xp: 10
```

`@instructions`
The model looks fine. We do a final graphical assessment of this model.

`@hint`


`@sample_code`
```{r}
#estimation
fit4 <- lm(score ~ stratio + poly(income, 4, raw=TRUE), data = CASchools)

#Use plot to assess the validity of the model specification

```

`@solution`
```{r}
#estimation
fit4 <- lm(score ~ stratio + poly(income, 4, raw=TRUE), data = CASchools)

#Use plot to assess the validity of the model specification
plot(fit4, which=1)
```

`@sct`
```{r}

```

---

## Multiple regression: normality of the error terms

```yaml
type: TabExercise
key: 4ebe7f0f52
xp: 100
```

In this exercise we want to assess the validity of the normality assumption.

`@pre_exercise_code`
```{r}
CASchools <- read.table("http://assets.datacamp.com/production/repositories/4109/datasets/58d484cd9aa9884502caf2e43cd1db69ab569f89/CASchools.txt")
CASchools$stratio <- CASchools$students/CASchools$teachers
CASchools$score <- (CASchools$math + CASchools$read)/2
source("http://assets.datacamp.com/production/repositories/4109/datasets/2452ec47ee5ae7d60fcadf8ab51780a5a0244e2c/resettest.R")
source("http://assets.datacamp.com/production/repositories/4109/datasets/e712d965a40e19322dc00dc13cd94e541266890c/nortest.R")
```

***

```yaml
type: NormalExercise
key: 45ed78633a
xp: 20
```

`@instructions`
Use plot with the correct argument which to assess graphically the validity of the normality assumption.

`@hint`


`@sample_code`
```{r}
#regression
fit2 <- lm(score ~ stratio + income, data = CASchools)
#q-q-plot

```

`@solution`
```{r}
#regression
fit2 <- lm(score ~ stratio + income, data = CASchools)
#q-q-plot of the residuals
plot(fit2, which=2)
```

`@sct`
```{r}

```

***

```yaml
type: MultipleChoiceExercise
key: 72b2fa76f1
xp: 20
```

`@question`
How do you interprete this plot?

`@possible_answers`
1. The points should all be close to zero when the error terms are normally distributed. Therefore, I reject the normality assumption.
2. The points should all be perfectly on the diagonal when the error terms are normally distributed. Therefore, I reject the normality assumption.
3. [The points should be close to the diagonal when the error terms are normally distributed. Here they slightly deviate from the diagonal at the upper tail.]

`@hint`


`@sct`
```{r}

```

***

```yaml
type: NormalExercise
key: 23c43e89e7
xp: 20
```

`@instructions`
To be sure, we now use a formal test. Perform the Cramer-von Mises test for normality of the standardized residuals.

`@hint`
The functions rstandard and cvm.test are useful!

`@sample_code`
```{r}
#regression
fit2 <- lm(score ~ stratio + income, data = CASchools)

#standardized residuals
standard.resid <- 

#Cramer-von-Mises test for the standardized residuals (add the correct function at the beginning of the line!)
(standard.resid)
```

`@solution`
```{r}
#regression
fit2 <- lm(score ~ stratio + income, data = CASchools)

#standardized residuals
standard.resid <- rstandard(fit2)

#Cramer-von-Mises test for the standardized residuals (add the correct function!)
cvm.test(standard.resid)
```

`@sct`
```{r}

```

***

```yaml
type: MultipleChoiceExercise
key: 09923fac3f
xp: 20
```

`@question`
How do you interpret the results of the test? (we use a significance level of 10%)

`@possible_answers`
1. [The p-value is above 10%. The null hypothesis is that the error terms are normally distributed. Thus, I cannot reject the validity of the normality assumption.]
2. The p-value is above 10%. The null hypothesis is that the error terms are not normally distributed. Thus, I cannot reject that the error terms are not normally distributed.
3. W is below 10%. The null hypothesis is that the error terms are normally distributed. Thus, I can reject the validity of the normality assumption.
4. W is below 10%. The null hypothesis is that the error terms are not normally distributed. Thus, I can reject that the error terms are not normally distributed.

`@hint`


`@sct`
```{r}

```

***

```yaml
type: MultipleChoiceExercise
key: 31c4571105
xp: 20
```

`@question`
Here we could not reject the validity of the normality assumption. What would be the consequence of a rejection?

`@possible_answers`
1. The estimated coefficients would be biased in finite samples.
2. The estimated variance of the estimated coefficients would be biased in finite samples.
3. [The confidence intervals would not cover the true coefficient with the rate in finite samples.]
4. All of the above.

`@hint`


`@sct`
```{r}

```

---

## Multiple regression: heteroscedasticity

```yaml
type: TabExercise
key: 373481ad1e
xp: 100
```

In this exercise we will test for heteroscedasticity and estimate robust standard errors

`@pre_exercise_code`
```{r}
CASchools <- read.table("http://assets.datacamp.com/production/repositories/4109/datasets/58d484cd9aa9884502caf2e43cd1db69ab569f89/CASchools.txt")
CASchools$stratio <- CASchools$students/CASchools$teachers
CASchools$score <- (CASchools$math + CASchools$read)/2
source("http://assets.datacamp.com/production/repositories/4109/datasets/46b197379ed9fce23068c367d4f8737540d38825/sandwich.R")
source("http://assets.datacamp.com/production/repositories/4109/datasets/d2d7a5184c3d15185e9d0907e2d928f67938b38e/lmtest.R")
```

***

```yaml
type: NormalExercise
key: 142182d8b7
xp: 15
```

`@instructions`
Regress score on stratio and english and save the result in fit5. All the variables are in the dataset CASchools.

`@hint`


`@sample_code`
```{r}

```

`@solution`
```{r}
fit5 <- lm(score~stratio+english,data=CASchools)
```

`@sct`
```{r}

```

***

```yaml
type: NormalExercise
key: ed0123c329
xp: 15
```

`@instructions`
Use the function plot to assess visually the validity of the homoscedasticity assumption.

`@hint`


`@sample_code`
```{r}
#Regression
fit5 <- lm(score~stratio+english,data=CASchools)

#Assessment of the homoscedasticity assumption

```

`@solution`
```{r}
#Regression
fit5 <- lm(score~stratio+english,data=CASchools)

#Assessment of the homoscedasticity assumption
plot(fit5, which=3)
```

`@sct`
```{r}

```

***

```yaml
type: MultipleChoiceExercise
key: 6f6ed10e94
xp: 15
```

`@question`
How do you interpret this figure?

`@possible_answers`
1. The observation number 6 is problematic.
2. The red line should be close to 0 everywhere. Here it is not the case such that the homoscedasticity assumption is likely to be satisfied.
3. [The red line should be flat. Here it is not the case such that the homoscedasticity assumption is likely to be satisfied.]
4. It looks absolutely fine.

`@hint`


`@sct`
```{r}

```

***

```yaml
type: NormalExercise
key: 5e0c935741
xp: 15
```

`@instructions`
Perform the Breusch-Pagan test against heteroskedasticity.

`@hint`
Use the function bptest.

`@sample_code`
```{r}
#Regression
fit5 <- lm(score~stratio+english,data=CASchools)

#Breusch-Pagan test

```

`@solution`
```{r}
#Regression
fit5 <- lm(score~stratio+english,data=CASchools)

#Breusch-Pagan test
bptest(fit5)
```

`@sct`
```{r}

```

***

```yaml
type: MultipleChoiceExercise
key: 9cfd60eae9
xp: 15
```

`@question`
How do you interpret the output?

`@possible_answers`
1. The p-value is very low. I can reject heteroscedasticity.
2. [The p-value is very low. I can reject homoscedasticity.]
3. The p-value is very low. I cannot reject heteroscedasticity.
4. The p-value is very low. I cannot reject homoscedasticity.

`@hint`


`@sct`
```{r}

```

***

```yaml
type: MultipleChoiceExercise
key: c98ffe41a3
xp: 15
```

`@question`
We must reject the homoscedasticity assumption. What is the consequence?

`@possible_answers`
1. The coefficients are biased in finite samples but are correct asymptotically.
2. The standard errors are biased in finite samples but are correct asymptotically.
3. [The standard errors are biased in finite samples and asymptotically.]
4. The causal interpretation of the coefficients is lost.

`@hint`


`@sct`
```{r}

```

***

```yaml
type: MultipleChoiceExercise
key: 2b17ccbdb4
xp: 15
```

`@question`
We must reject the homoscedasticity assumption. What should you do?

`@possible_answers`
1. [We should estimate differently the standard errors.]
2. We should estimate a more flexible model.
3. We should collect more data.
4. We should stop doing econometrics.

`@hint`


`@sct`
```{r}

```

***

```yaml
type: NormalExercise
key: fefd6628ff
xp: -5
```

`@instructions`


`@hint`


`@sample_code`
```{r}

```

`@solution`
```{r}

```

`@sct`
```{r}

```
