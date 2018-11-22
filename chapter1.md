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
plot(fit4,which=1)
```

`@sct`
```{r}

```
