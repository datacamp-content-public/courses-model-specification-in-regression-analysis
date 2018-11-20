---
title: 'Chapter 1'
description: 'Chapter description goes here.'
---

## Example coding exercise

```yaml
type: NormalExercise
key: 2bafef99a3
lang: r
xp: 100
skills: 1
```

The CASchools dataset contains data on test performance, school characteristics and student demographic backgrounds. The data used here are from all 420 K-6 and K-8 districts in California with data available for 1998 and 1999. Test scores are the average of the reading and math scores on the Stanford 9 standardized test administered to 5th grade students. School characteristics include enrollment, number of teachers, number of computers per classroom, and expenditures per student. The demographic variables include the percentage of
students in the public assistance program, the percentage of students that qualify for a reduced price lunch, and the percentage of students that are
English Learners.

`@instructions`
1) Load the AER package.
2) Load the dataset CASchools.
3) Add a variable stratio to the dataset CASchools defined as students/teachers.
4) Add a variable score to the dataset CASchools defined as the average of math and read.

`@hint`


`@pre_exercise_code`
```{r}

```

`@sample_code`
```{r}
#1 Load the AER package.


#2 Load the dataset CASchools.


#3 Add a variable stratio to the dataset CASchools defined as students/teachers.


#4 Add a variable score to the dataset CASchools defined as the average of math and read.


```

`@solution`
```{r}
#1 Load the AER package.
library(AER)

#2 Load the dataset CASchools.
data(CASchools)

#3 Add a variable stratio to the dataset CASchools defined as students/teachers.
CASchools$stratio <- CASchools$students/CASchools$teachers

```

`@sct`
```{r}

```
