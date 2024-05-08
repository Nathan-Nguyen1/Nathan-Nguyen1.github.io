---
title: "A Brief Overview of Multiple Hypothesis Testing"
date: "08 May 2024"
excerpt: Some important considerations to minimize Type I error.
output:
  code_folding: true
---



# Making a scatterplot with a linear trend
I'll use the built-in Iris dataset for this demonstration


```r
# define number of hypothesis tests
num_tests <- 1:500

# define alpha values
alphas <- c(0.001, 0.01, 0.05)

# define fwer function
fwer_function <- function(num_tests, alpha) {
  1 - (1 - alpha)^num_tests
}

fwer_data <- expand.grid(num_tests = num_tests, alpha = alphas) %>% 
  mutate(fwer = fwer_function(num_tests, alpha))

fwer_data %>% 
  ggplot(aes(x = num_tests, y = fwer, color = factor(alpha), group = alpha)) +
  geom_line() +
  scale_color_lancet() +
  # scale_x_log10() +
  labs(title = "Family-wise Error Rate for Different Significance Levels",
       subtitle = "Simulated for 500 Hypothesis Tests",
       x = "Number of Hypotheses",
       y = "Family-Wise Error Rate",
       color = expression(alpha-level),
       caption = "Figure inspired by An Introduction to Statistical Learning") +
  theme_bw() +
  geom_hline(yintercept = 0.05, linetype = "dashed", color = "black") +
  scale_x_log10(breaks = c(1, 5, 10, 50, 100, 500),
                labels = c("1", "5", "10", "50", "100", "500"))
```

<img src="{{< blogdown/postref >}}index_files/figure-html/featured-1.png" width="672" />
