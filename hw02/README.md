
# Stat545 hw02

[link to STAT545-hw02-An-Byeongchan.md](STAT545-hw02-An-Byeongchan.md)  


[link to STAT545-hw02-An-Byeongchan.Rmd](STAT545-hw02-An-Byeongchan.Rmd)  
[link to STAT545-hw02-An-Byeongchan.html](STAT545-hw02-An-Byeongchan.html)

## Report my progress
I realized that I could use not only ggplot but plot as well. For example, I used plot(x=gapminder$continent, y=gapminder$lifeExp, gapminder). It was convenient to show the general distribution by showing many of the summary stats such as mean, median, quartiles, and outliers. geom_boxplot() makes similar plot.

When I tried to make a summary for each group formed by each continent, I couldn't use the function summary(). And it seems like summarize() function takes only single value (I couldn't use quantile() function in summarize()).

Furthermore, I was wondering if there is any convenient shortcut(function) for using different color points on quartile (I could do it by assigning each variable in each interval.).