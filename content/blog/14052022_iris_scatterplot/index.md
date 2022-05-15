---
title: "Scatterplot with Linear Trend Demonstration"
date: "14 May 2022"
excerpt: A simple demonstration of a scatterplot with linear trends.
output:
  code_folding: true
---



# Making a scatterplot with a linear trend
I'll use the built-in Iris dataset for this demonstration


```r
attach(iris)
data <- iris

data %>%
  ggplot(aes(x = Sepal.Width, y = Sepal.Length, group = Species)) +
  geom_point(aes(color = Species)) +
  geom_smooth(aes(color = Species), method = "lm", se = FALSE) +
  scale_color_d3() +
  labs(x = "Sepal Width",
       y = "Sepal Length",
       title = "Relationship between Sepal Length and Sepal Width by Species") +
  theme(legend.position = "bottom")
```

<img src="{{< blogdown/postref >}}index_files/figure-html/featured-1.png" width="672" />

