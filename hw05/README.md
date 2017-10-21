
# Stat545 hw05

[link to STAT545-hw05-An-Byeongchan.md](STAT545-hw05-An-Byeongchan.md)  

 
[link to STAT545-hw05-An-Byeongchan.Rmd](STAT545-hw05-An-Byeongchan.Rmd)  
[link to STAT545-hw05-An-Byeongchan.html](STAT545-hw05-An-Byeongchan.html)

## Report my progress
  
I learned that when `fct_reorder2()` is used, the factor is still the groupiing variable but the default summarizing function is not `median()`. In this code `ggplot(h_gap, aes(x = year, y = lifeExp,color = fct_reorder2(country, year, lifeExp))) + geom_line()`, the order in the legend is not by the median value but by the most recent value.   
  
In this setting, `mutate()` is assigning the feature country to the `country` with reordered factors based on life_exp
>g4 <- g3 %>% 
  mutate(country = fct_reorder(country, life_exp))  
  
For scatter plot colored by continent, `scale_color_manual()` or `scale_color_brewer()` should be used instead of `scale_fill_manual()` or `scale_fill_brewer()`  
  
In `scale_color_gradient()`, `mid=""` cannot be used. `scale_color_gradient2()` should be used instead.  
  
In `ggsave()` `dpi =` is a plot resolution. It applies only to raster output types.