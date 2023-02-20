#  Statistics

[Home](https://alexpmagalhaes.github.io/R-course/index)

## Exercise 5


In this practical you'll do basic statistics in R. By the end of this practical you will know how to:
1. Calculate basic descriptive statistics using `mean()`, `median()`, `table()`.
2. Conduct 1 and 2 sample hypothesis tests with `t.test()`, `cor.test()` and `chisq.test()`
3. Calculate regression analyses with `glm()`
4. Explore statistical objects with `names()`, `summary()`, `print()`, `predict()`
5. Use sampling functions such as `rnorm()` to conduct simulations

All you will need is a csv [file](https://alexpmagalhaes.github.io/R-course/Materials/Datasets/Exercise4/totalrootdf.csv)
We will call this **df** just to be easier.

1. You need to set the _working directory_.
2. You need to load the necessary packages (**tidyverse**) for this exercise.
3. Use `read_csv()` to open the file.

```r
df <- read_csv("totalrootdf.csv")

```

```r
mean(df$rootlength)   # What is the mean rootlength?
median(df$rootlength)   # What is the median rootlength?
max(df$rootlength)    # What is the maximum rootlength?
table(df$Genotype)    # How many observations for each Genotype?

```


```r
htest_A <- t.test(x = df$rootlength,     # The data
                  alternative = "two.sided",  # Two-sided test
                  mu = 0.5)                   # The null hyopthesis
htest_A            # Print result
names(htest_A)     # See all attributes in object
htest_A$statistic  # Get just the test statistic
htest_A$p.value    # Get the p-value
htest_A$conf.int   # Get a confidence interval

```

```r
res.aov <- aov(rootlength ~ Genotype, data = df)

summary(res.aov)

TukeyHSD(res.aov)

```
## You are done!

Here are the main descriptive statistics functions we will be covering.

| Function| Description|
|:------|:--------|
| `table()` | Frequency table |
|`mean(), median(), mode()`|Measures of central tendency|
|`sd(), range(), var()`|Measures of variability|
|`max(), min()`|Extreme values|
| `summary()`| Several summary statistics |

Here are the main statistical functions we will be covering.

| Function| Hypothesis Test| Additional Help |
|:------|:-------------------|:----|
|     `t.test()`|    One and two sample t-test| https://bookdown.org/ndphillips/YaRrr/htests.html#t-test-t.test
|     `cor.test()`|    Correlation test| https://bookdown.org/ndphillips/YaRrr/htests.html#correlation-cor.test
|     `chisq.test()`|    Chi-Square test| https://bookdown.org/ndphillips/YaRrr/htests.html#chi-square-chsq.test
|     `glm()`|    Regression| https://bookdown.org/ndphillips/YaRrr/regression.html|

Here are the random sampling functions we will use

| Function| Description| Additional Help |
|:------|:--------|:----|
|`sample()`|Draw a random sample of values from a vector| `?sample`|
|`rnorm()`|Draw random values from a Normal distribution| `?rnorm()`|
|`runif`|Draw random values from a Uniform distribution| `?runif()`|


To check all the solutions pleae follow this [Link](http://rpubs.com/alexpmagalhaes/Exercise5).

To Download the notebook click [here](https://alexpmagalhaes.github.io/R-course/Materials/Scripts/Exercise5.Rmd)

[Back to the Top](#statistics)

[Home](https://alexpmagalhaes.github.io/R-course/index)
