```r
g <- ggplot(df, aes(x = Sample, y = rootlength, colour = Treatment)) +
geom_boxplot(notch = FALSE) +
geom_jitter(size = 0.5, alpha = 0.05, width = 0.25, colour = 'black') +
labs(x = 'Samples', y = 'Root length (mm)') +
ggtitle('Effect of GA in root lenth')+
labs(colour = 'Treatment')+
scale_colour_brewer(palette = 'Set2') +
theme_bw() +
theme(
  axis.text.x = element_text(angle = 45, hjust = 1),
  legend.position = 'top',
  panel.grid.major = element_blank(),
  panel.grid.minor = element_blank()
)

g1 <- ggplot(df, aes(x = Sample, y = Hair.Root.length, colour = Treatment)) +
geom_violin() +
geom_jitter(size = 0.5, alpha = 0.05, width = 0.25, colour = 'black') +
labs(x = 'Samples', y = 'Root length (mm)') +
ggtitle('Effect of GA in Hair root lenth')+
labs(colour = 'Treatment')+
scale_colour_brewer(palette = 'Set2') +
stat_summary(fun.y = "mean", geom = "point", col = "black", size = 3) +
theme_bw() +
theme(
  axis.text.x = element_text(angle = 45, hjust = 1),
  legend.position = 'top',
  panel.grid.major = element_blank(),
  panel.grid.minor = element_blank()
)

install.packages("cowplot")
library("cowplot")


mg <- plot_grid(g, g1,labels = c('A', 'B'), label_size = 12)
mg

```

```r

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
