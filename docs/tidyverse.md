#  Tiding up R

[Home](https://alexpmagalhaes.github.io/SFB924-R-course/index)

## Exercise 3

R is a software language for carrying out any level of statistical analyses and visualization.
For one reason or another transferring your Excel can be a challange for beginers.
Even when working with other tools, it's s rare that you get the data in the right form.

Often creating new variables and summaries, renaming or reordering data in R requierds a advanced programmming skils or hours in excel.

Packages like tibble, dyplr and tidyr can help to do almost everything you will need. On top of that packages like Tidyverse not only bundle them in one package, but also simplify the code and elliminate any overlap between packages.

In this chapteryou will learn how to transform data to be abble to use the downstream analysis tools in R to get your plots and statisticl analysis the way you want them.
By the end you will be able to:
 1. Use tidyverse to open files.
 2. Use **pipe** logic `%>%` to do multiple transformation at once.
 3. Use the many functions of dplyr to **select, filter, rename** and **rearange data**.
 4. The dplyr to **create** new variables and **transform** data.
 5. Combine data aka "vlookup" of excel
 6. **Transpose** and **reformat** data with tidyr.

 This tutorial will be a bit different for the earlier.
 You will be asked to complete a challange that will allow you to rearange and qPCR data set in the typical sampleling layout and calculate means of tecnical samples.


To explore the basic data manipulation you will need to creat a new folder for Exercise 3 and download the [File 1](https://alexpmagalhaes.github.io/SFB924-R-course/Materials/Datasets/Exercise3/root_length.csv), [2](https://alexpmagalhaes.github.io/SFB924-R-course/Materials/Datasets/Exercise3/root_hair.csv) and [3](https://alexpmagalhaes.github.io/SFB924-R-course/Materials/Datasets/Exercise3/qPCR_replicates.csv).

We will work fist with File **1** and **2**. I will name variables 'XXX' or 'YYY',the files you need as 'FILE1' or 'FILE2'.

1. You need to set the _working directory_.
2. You need to load the necessary packages (**tidyverse**) for this exercise.
3. Use `read_csv()` to open the **FILE1** and **FILE2**.

```r
rldf <- read_csv("root_length.csv")
rhdf <- read_csv("root_hair.csv")
```

From now on you have to consider using **pipe** logic.


4. To check the names of the column is accomplished with `names(FILE1)`.

```r
names(rldf)
```

5. `Summany()` still works with tidyverse so you can use it to get stats on the table.
6. Using `rename( NEWXXX = XXX )` you are able to change the name of a column.

```r
rldf <- rldf %>%
  rename(rootlength = length )
```

7. Selecting a column can be done with **select(XXX, YYY)**, a `-`sign before the variable will omit it. Also you can select multiple columns if they have a patern using `starts_with("AA")`.

```r
rldf %>%
  select('rootlength', Genotype)

rldf %>%
    select(-Genotype)

rldf %>%
      select(starts_with("root"))
```

8. `mutate()` can be used to add new columns to the data set. `mutate()` accepts functions , condicionals and logical operator and text:
      1. Arithmetic operators: `+`, `-`, `*`, `/`, `^`.
      2. Modular arithmetic: `%/%` (integer division) and `%%` (remainder).
      3. Logs: `log()`, `log2()`, `log10()`.
      4. Cumulative and rolling aggregate: `cumsum()`, `cumprod()`, `cummin()`, `cummax()`and `cummean()`.
      5. Logical comparisons: `<`, `<=`, `>`, `>=`, `!=`, and `==`.
      6. Ranking: `min_rank()`.

```r
tenrldf <- rldf %>%
  mutate(tenrootlength = rootlength * 10)

logrldf <- rldf %>%
      mutate(logrootlength = log2(rootlength))
```

If you want to only keep the new columns you can use `transmute().

9. Filtering is acomplished by `filter()` and logical operators you can use are `&` is **and**, `|` is **or**, and `!` is **not**.

![Logical opetarors](https://alexpmagalhaes.github.io/SFB924-R-course/jpegs/spread_data_R.png)

```r
rldfColGA <- rldf %>%
  filter(Genotype == "Col-0" & Treatment == "GA")
```
10. To rearange the columns use `arrange()` and `desc()` inside the formula to rearrange in descending order.

```r
rldf <- rldf %>%
  arrange(desc(rootsample))
```

11. To join two data frames by a commun variable like "vlookup"function in excel you ca use `left_join()`. Be aware that the full table will be join and variables with the same name will have ".x" and ".y" attached.

```r
rhdf <- rhdf %>%
  select(-Genotype, -Treatment)

totaldf <- rldf %>%
  left_join(rhdf, by = "rootsample")

totaldf

write.csv(totaldf, file = "totalrootdf.csv", row.names = FALSE)
```
12. Widening and shortning a data frame is an important step so other packages can use the data. `spread(key = XXX, value = YYY, fill = VALUE )` and `gather(key = XXX, value = YYY, fill = VALUE )` acomplieh this task.

![wideandlong](https://alexpmagalhaes.github.io/SFB924-R-course/jpegs/transform-logical.png)


```r
widetotaldf <- totaldf %>%
  spread(key = 'sample', value = 'rootlength',  fill = NA)
widetotaldf
```

#### Now comes the challange!

File 3 in of this exercise is a tipical qPCR experiment formated table.
I want you to:
* calculate the mean of each gene
* write an output file with the results.


To aid in this task I will list all the functions you will need.
`read_csv`, `write.csv`, `gather`, `spread`, `str_split_fixed`, `paste`, `collapse`, `group_by`, `summarize`, `mean`, `column_to_rownames`, `apply`.


```r echo = FALSE

repqPCR <- read_csv("qPCR_replicates.csv")
longrepqPCR <- gather(repqPCR, "group", "Expression", -ID)
longrepqPCR$tgroup = apply(
  str_split_fixed(longrepqPCR$group, "_", 3)[, c(1, 2)],
  1,
  paste, collapse ="_"
  )
meansqPCR <- longrepqPCR %>%
  group_by(ID, tgroup) %>%
  summarize(expression_mean = mean(Expression)) %>%
  spread(., tgroup, expression_mean)
meansqPCR <- meansqPCR %>% column_to_rownames('ID')
write.csv(meansqPCR, file= "meansqPCR.csv")

```

## You are done!

| Function| Description|
|:------|:--------|
|`setwd()`| Sets the working directory|
|`date()`| Prints the current date|
|`read_csv()`| Read comma delimited csv file|
|`read_delim()`| Read tab-ular delimited txt file|
|`read_csv2()`| Read semi-column delimited csv file|
|`readRDS()`| Read RDS file|
|`tibble()`| Make a `data.frame`the tidyverse way|

| Function| Description|
|:------|:--------|
|`write_csv()`| Write csv file|
|`saveRDS()`| Save RDS file |

##### Tidyverse verbs

| verb| action|
|:---|:----------------------|
|`filter()`|Select rows based on some criteria|
|`arrange()`|Sort rows|
|`select()`|Select columns (and ignore all others)|
|`rename()`|Rename columns|
|`mutate()`|Add new columns|
|`case_when()`|Recode values of a column|
|`group_by(), summarise()`|Group data and then calculate summary statistics|
|`left_join()`|Combine multiple datasets using a key column|
|`spread()` and `gather()`| Converte long datasets in to wide|
|`gather()`| Converte wide datasets in to long|

To check all the solutions pleae follow this [Link](http://rpubs.com/alexpmagalhaes/Exercise3).

To Download the notebook click [here](https://alexpmagalhaes.github.io/SFB924-R-course/Materials/Scripts/Exercise3.Rmd)

[Back to the Top](#tiding-up-r)

[Home](https://alexpmagalhaes.github.io/SFB924-R-course/index)
