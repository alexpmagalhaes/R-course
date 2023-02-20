# Welcome to the MolMed R course

[Home](https://alexpmagalhaes.github.io/R-course/index)

## Let's start

In this Exercise you’ll learn how to work with simple data objects and use functions in R.
At the end of this exercise you will be able to:

1. Create vectors of different types using `c()`
2. Understand the three main vector classes _numeric_, _character_, and _logical_ using `class()`
3. Calculate basic descriptive statistics using `mean()`, `median()`, `max()` and more!
4. Make simple frequency histograms using `hist()` and simple functions.


Fist I want to introduce to you **R Notebooks!**

You are going to open Rstudio and go to **File** -> **New File** -> **R Notebook**.

This notebooks are written in a blogging language called _markdown_.
This language is great for *R* because it works in a linear fashion. The [R Markdown](http://rmarkdown.rstudio.com) version that is installed in R studio alows you to execute code within the notebook, the results appear beneath.

In the editor on the right you should type R code to solve the exercises.
When you click the *run* buttun the chunk that is selected will execute all the commands.

Code that is *commented*, in other words, starts with `#` is ignored by r. so you can use it to comment code that you wrote.

Code cann also be executed in the console. This is a great way to check the code, as your submission is not checked for correctness.

Add a new chunk by clicking the *Insert Chunk* button on the toolbar or by pressing <kbd>&#8984;</kbd> or <kbd>Control</kbd> + <kbd>Shift</kbd> and <kbd>I</kbd>.


##### Lets go with the Homework and expand a bit

1. On the notebook I want you to:
  1. Calculate 5+7-1
  2. Store that result to an object
  3. Store each individual variable as an object (call them **x**, **y** and **z**)
  4. Define a function to sum **x** and **y** and subtract **z**
  5. **Print** that function
  6. Use other arithmetic functions with that object like  `log2()`, `log10()`, `exp()`, `sqrt()`.


  ```r
  5+7-1

  rs <- 5+7-1

  x <- 5
  y <- 7
  z <- 1

  fm = x+y-z

  fm

  log2(fm)
  log10(fm)
  exp(fm)
  sqrt(fm)
  ```

2. Working with **vector**, **lists** or other types of data objects is important.
Many packages for R requier diferent types of data to function correctly so you should be able to generate and modify them. We will focus in vectors because its the most importa of these data objects.

To start you need to generate a vector with `c()`function.

  1. Make a vector contaning
    * 4 twos
    * 6 threes
    * 8 fours
    * 8 fives
    * 4 sevens
    * 4 eights
    * 2 nines
  2. Get some information on the object like `length()`, `class()` , `max()`and the `mean()` of the values.
  3. Plot an frequency graph of the object with `hist()`.
  4. Add 1 to that vector
  5. Print that new vector

  ```r
  vc <- c(2,2,2,2,3,3,3,4,4,4,4,4,4,4,4,5,5,5,5,5,5,5,5,7,7,7,7,8,8,8,8,9,9)

  length(vc)
  class(vc)
  max(vc)
  mean(vc)

  hist(vc)

  newvc <- vc + 1

  newvc
  ```

#### Types of data in R


Numerous data types can be used in R.

##### Types of data include

- **numeric** - numbers with decimal values. ex. 8.4
- **integer** - natural numbers. ex. 8 *Sometimes interchangable.*
- **logical** - operators/boolean values ex. TRUE or FALSE.
- **character** - text values. ex. "genotype"

*Please note the quotation marks indicate that "some text" is a character. This can be used in some file types to indicate **characters* class data.*

##### Lets make and change some values of objects:

Create a set of objects for **numeric**, **logical**, **character**


```r
nvalue <- 1523

cvalue <- "genotype"

lvalue <- TRUE

```


Common formatation errors can be trace back to value classes that are loaded into R and expected by a package. *Always check the class of data that R loaded and check the documentation for the expected data class for each function*

Please check the class of your numeric value! and a **x** from the previous exercises to this value.


```r
class(nvalue)

nvalue + x
```


#### Functions used in this exercise

| Function| Description|
|:------|:--------|
|     `c(), rep(), seq(), numeric(), etc.`| Vector creation|
|     `matrix(), cbind()`| Matrix creation|
|     `data.frame()`| Data frame creation|
| `list()`| List creation |

| Function| Description|
|:------|:--------|
| `hist()`| Makes a frequency plot|
|`class()`|Check a given object class|
|`length()`| Print the number of variables|



To check all the solutions pleae follow this [Link](http://rpubs.com/alexpmagalhaes/Exercise1).

To Download the notebook click [here](https://alexpmagalhaes.github.io/R-course/Materials/Scripts/Exercise1.Rmd)

[Back to the Top](#welcome-to-the-r-course)

[Home](https://alexpmagalhaes.github.io/R-course/index)




`
