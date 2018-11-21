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
xp: 25
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
xp: 25
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
xp: 25
```

`@instructions`
A first step to assess the linearity assumption consists in plotting the dependent and independent variables and adding the regression line.

`@hint`
Use the function plot for the scatterplot. Use abline and lm for the regression line.

`@sample_code`
```{r}
#Generate a scatterplot of the dependent variable (y-axis) and regressor (x-axis)


#Add a line for the fitted values


```

`@solution`
```{r}
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
xp: 25
```

`@instructions`
We now complete the graphical assessement with a formal test. A simple

`@hint`


`@sample_code`
```{r}

```

`@solution`
```{r}
resettest(lm(score~stratio, data=CASchools))
```

`@sct`
```{r}

```
