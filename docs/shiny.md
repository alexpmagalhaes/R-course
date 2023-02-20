#  Shiny and more

[Home](https://alexpmagalhaes.github.io/R-course/index)

## Exercise 5


We will explore a bit of shiny and helper packages in this exercise.

Two of my favorites are `ggplotgui` and `ggpubr`

#### ggplotgui

This shiny app is a GUI for ggplot. It just makes the whole experiance much quicker and accessable.

Try it out and see how nice it is!


```r
library("ggplotgui")
# You can call the function with and without passing a dataset
ggplot_shiny()
ggplot_shiny(df) # Passing ggplot's mpg dataset
```

ggbubr is another great that facilitates the creation of beautiful ggplot2-based graphs for researcher with non-advanced programming backgrounds.

It`s a wrapper around the ggplot2 package with a less opaque syntax.

* Helps researchers, with non-advanced R programming skills, to create easily publication-ready plots.
* Makes it possible to automatically add p-values and significance levels to box plots, bar plots, line plots, and more.
* Makes it easy to arrange and annotate multiple plots on the same page.
* Makes it easy to change grahical parameters such as colors and labels.


[https://rpkgs.datanovia.com/ggpubr/index.html](https://rpkgs.datanovia.com/ggpubr/index.html)

One exemple of a function you can try!

```r

library(ggpubr)

compare_means(rootlength ~ Treatment,  data = df, method = "anova")

df$Sample <- factor(df$Sample, levels = c("Col-0_Mock", "Col-0_GA", "Col-0_PAC", "dP_Mock", "ga1-13_Mock", "ga1-13_GA"))

ggviolin(df, x = "Sample", y = "rootlength",
          fill = "Treatment",
         palette = c("#00AFBB", "#E7B800", "#FC4E07"),
          x.text.angle = 45, , ylim = c(0, 15),
         add = "boxplot", add.params = list(fill = "white"))+
  stat_compare_means(method = "anova", label.y = 14)+
stat_compare_means(label = "p.signif", method = "t.test",
                     ref.group = "Col-0_Mock", label.y = 12)
```


If you are looking for excel replacements


* [rhandsontable](https://jrowen.github.io/rhandsontable/)

* [DTedit](https://github.com/jbryer/DTedit)

* [formattable](https://github.com/renkun-ken/formattable)

## The end

To check all the solutions pleae follow this [Link](http://rpubs.com/alexpmagalhaes/Exercise6).

To Download the notebook click [here](https://alexpmagalhaes.github.io/R-course/Materials/Scripts/Exercise6.Rmd)

[Back to the Top](#shiny-and-more)

[Home](https://alexpmagalhaes.github.io/R-course/index)
