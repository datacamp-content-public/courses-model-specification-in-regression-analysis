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

```

***

```yaml
type: NormalExercise
key: d6674928cf
xp: 100
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
