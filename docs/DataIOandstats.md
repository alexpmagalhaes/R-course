#  Data, data and more data

[Home](https://alexpmagalhaes.github.io/R-course/index)

## Exercise 2

We are going to learn how to read data from a set of files, write data and calculate some statistcs.
By the end you will be able to:
  1. Create  `data.frames` using `data.frame()` and `tibble()`
  2. Write files to the disk in a variaty of formats using `write.csv()`, `write.delim()` and others like it.
  3. Use functions like `dim()` or `sumary()`
  4. Subsection data using `[ ]`
  5. Generate data for into vectors using `rnorm()`, `runif()`.



1. Frist step is to make a folder on the desktop so we can have a _working directory_.
2. Download the 3 tables that are required for this exercise and copy them to the folder you created earlier. [File 1](https://alexpmagalhaes.github.io/R-course/Materials/Datasets/Exercise2/DEGS.txt), [File 2](https://alexpmagalhaes.github.io/R-course/Materials/Datasets/Exercise2/qPCR.xls), [File 3](https://alexpmagalhaes.github.io/R-course/Materials/Datasets/Exercise2/rootlength.csv).
3. Open a new notebook and **let's get started**!

In this exercice you’ll learn how to deal with simple tables and functions, how to read and save data and make some simple statistics.

Create data.frames and tibbles! using data.frame() and tibble()
Access vectors from data frames using $


Read in data of various types
Create data.frames and tibbles! using data.frame() and tibble()
Access vectors from data frames using $
Calculate basic descriptive statistics using `mean()`, `median()`, `table()` (and more!)

  1. You need to set the _working directory_! You can use `setwd()` for these porpuse.
  2. You need to load the necessary packages (**tidyverse** and **readxl**) for this exercise.
  3. Use `read_csv()`, `read_excel` and `read_delim` to open the files you downloaded earlier. _Import Datasets_ button it the _enviroment_ tab in RStudio can be used to acomplish the same.
  4. Have a look at the first rows of the table and note if the table is loaded the right way. Also when using RStudio you can click twice in object to open the full table.
  5. Some of the files are not in csv file format. Write to the folder csv versions of the txt and excel files with `write.csv`.

  ```r
  rootl_df <- read.csv("rootlength.csv", header = TRUE, row.names = NULL, sep = ",", dec = ".")

  qpcr_df <- read_excel("qPCR.xls", col_names = TRUE, sheet = NULL, range = NULL, col_types = NULL)

  heat_df <- read.delim("DEGS.txt", header = TRUE, row.names = 1, dec = ".")

  head(rootl_df)

  write.csv(qpcr_df, file = "qpcr_df.csv", quote = FALSE, row.names = TRUE)

  write.csv(heat_df, file = "heat_df.csv", quote = FALSE, row.names = TRUE)

```


By now you should be able to read and write in R.
Next step is to check some properties of the tables you loaded.
This not only helps you understant if the objects were created the right way but if also allows you to quickly get some statistics on your objects.

  One way to check if the tabble is correcly loaded is to check the **number of rows and columns**. `dim()` function will print them.
  You can still use functions like `mean()` on tables but you would need to select a column to do so. If you want rapid **statistics on all each column** use `summary()`. Functions like those can also used in condicional functions using brakets `[ ]` to **subsection the data**.

  1. For the first table you need to get the number of rows and columns
  2. You also need to report the mean of first column, all well of the global summary of the rest of the table.
  3. Check the distribution of the data to have a felling on the type of statistics you could do in the down stream analysis.
  4. Put together a function of your choice with a subsection of the data.

  ```r

dim(rootl_df)

mean(rootl_df$colMock)

summary(rootl_df)

hist(rootl_df$colMock)

mean(rootl_df$colMock[rootl_df$colMock < 5])

```

  Sometimes you also need to simulate data.
  R can sample data points from a number of distributions.

Sampeling can be achived by `runif()`, `rnorm()`, `rbinom()`,`rpois()`, `rbeta()`.

Depending on the type of distribution to be sampled, the minimum variale parameters to discripe that distribution have to be given.

Today you are going to sample from **uniform** and **normal** distributions. The resulting samples can be stored in **vectors** that can be concatinated into tables. To do that we will use `tibble`.

  1. Load `tibble! package
  2. You need to make a vector containing 500 sampling points from a uniform distribution with `min` of 3 and `max`imun of 4.
  3. Another vector with 500 normaly distributed point must be created with mean of 4.5 and a Standard Deviation of 1.
  4. Use tibble to create a data frame with those two vectors.
  5. Visualize the distribution of those two sets.
  6. Write a csv file containing the new data frame.


```r
library("tibble")

colMock <- runif(500, min = 3, max = 4)
colGA <- rnorm(500, 4.5, 1)

newtable <- tibble(colMock, colGA )

hist(colGA)
hist(colMock)

write.csv(newtable, file = "newtable.csv", quote = FALSE , row.names = FALSE )

```



## You are done!

Now everything changes!


##### Please proced to [Exercise 3](https://alexpmagalhaes.github.io/R-course/docs/tidyverse.md)



#### Functions used in this exercise

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


  | Function| Description|
  |:------|:------------------------------|
  |`[ ]`| Select individual elements from `vector`|
  |`[[ ]]`| Select element from a list or `data_frame` |
  |`$`| Select named element/variable from list or `data_frame`|

  | Function| Description|
  |:------|:--------|
  |`head(), tail()`| Inspect first or last elements of object|
  |`str()`| Inspect the structure of the data object|
  |`View()`| To access an Excel like data interface|
  |`summary()`| Summary statistics for a given `data_frame`|
  |`dim()`| Prints the the number of rows and columns|


  | Function| Description|
  |:------|:--------|
  |`rnorm()`| Sampe from normal distribution|
  |`runif()`| Sampe from uniform distribution|
  |`rbinom()`| Sampe from binomial distribution|
  |`rpois()`| Sampe from poisson distribution|
  |`rbeta()`| Sampe from beta distribution|





To check all the solutions pleae follow this [Link](http://rpubs.com/alexpmagalhaes/Exercise2).

To Download the notebook click [here](https://alexpmagalhaes.github.io/R-course/Materials/Scripts/Exercise2.Rmd)

[Back to the Top](#data-data-and-more-data)

[Home](https://alexpmagalhaes.github.io/R-course/index)
