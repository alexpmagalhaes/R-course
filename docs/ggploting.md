#  ggploting (aka the one you don’t want to skip)

[Home](https://alexpmagalhaes.github.io/R-course/index)

## Exercise 4
In this exercise you'll practice plotting data with the `ggplot2` package.
All you will need is a csv [file](https://alexpmagalhaes.github.io/SFB924-R-course/Materials/Datasets/Exercise4/totalrootdf.csv)
We will call this **df** just to be easier.


1. You need to set the _working directory_.
2. You need to load the necessary packages (**tidyverse**) for this exercise.
3. Use `read_csv()` to open the file.

```r
df <- read_csv("totalrootdf.csv")

```

* Try to plot the data frame with `ggplot(data = df)`.

* Map your data with `mapping = aes(x = XXX, y = YYY)`.

* add `geom_point()` to the plot.


```r
# trying to plot without mappings
ggplot(data = df)
```

```r
# Map rootlength to x-axis and Hair.Root.length to y-axis
ggplot(data = df,
       mapping = aes(x = rootlength, y = Hair.Root.length))
```

```r
#  Add points with geom_point()
ggplot(data = df,
       mapping = aes(x = rootlength, y = Hair.Root.length)) +
       geom_point()
```

```r
# Again, but with some additional arguments
# Also using a new theme temporarily
ggplot(data = df,
       mapping = aes(x = rootlength, y = Hair.Root.length)) +
       geom_point(col = "blue",                  # Red points
                  size = 2,                     # Larger size
                  alpha = .5,                   # Transparent points
                  position = "jitter") +        # Jitter the points
         scale_x_continuous(limits = c(0, 10)) +  # Axis limits
         scale_y_continuous(limits = c(0, 5)) +
  theme_minimal()
```

```r
# Assign class to the color aesthetic and add labels with labs()
ggplot(data = df,
       mapping = aes(x = rootlength, y = Hair.Root.length, col = Sample)) +  # Change color based on class column
  geom_point(size = 1, position = 'jitter') +
  labs(x = "Root length (mm)",
       y = "Root hair length (mm)",
       title = "GA effect in root architecture",
       subtitle = "Root length vs root hair lenth in GA PAC treated seedling",
       caption = "Source: Fake data repository")
```

```r
# Add a regression line for each class
ggplot(data = df,
       mapping = aes(x = rootlength, y = Hair.Root.length, col = Sample)) +
  geom_point(size = 1, alpha = .5) +
  geom_smooth(method = "lm")

```

```r
# Facet by class
ggplot(data = df,
       mapping = aes(x = rootlength,
                     y = Hair.Root.length,
                     color = factor(Sample))) +
  geom_point() +
  facet_wrap(~ Genotype) + coord_flip()
```

#### Now comes the challange!

Try to make this plot.

![challange](https://alexpmagalhaes.github.io/SFB924-R-course/jpegs/00001d.png)




Now lets save the plot!

```r
ggsave(filename = "myplot.pdf", plot = mg, width = 6, height = 4)
```
## You are done!


ggplot is more easily learned with exemples:

* Access the `ggplot2` cheatsheet [here](https://www.rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf). This has a nice overview of all the major functions in ggplot2.
* This practical Selva Prabhakaran's [website](http://r-statistics.co/Top50-Ggplot2-Visualizations-MasterList-R-Code.html) can help you with advence code.
* The main `ggplot2` [webpage](http://ggplot2.tidyverse.org/) has also great tutorials.

To check all the solutions pleae follow this [Link](http://rpubs.com/alexpmagalhaes/Exercise4).

To Download the notebook click [here](https://alexpmagalhaes.github.io/SFB924-R-course/Materials/Scripts/Exercise4.Rmd)

[Back to the Top](#tiding-up-r)

[Home](https://alexpmagalhaes.github.io/R-course/index)
