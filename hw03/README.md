
# Stat545 hw03

[link to STAT545-hw03-An-Byeongchan.md](STAT545-hw03-An-Byeongchan.md)  

 
[link to STAT545-hw03-An-Byeongchan.Rmd](STAT545-hw03-An-Byeongchan.Rmd)  
[link to STAT545-hw03-An-Byeongchan.html](STAT545-hw03-An-Byeongchan.html)

## Report my progress

I tried to use dplyr to manipulate and explore data and ggplot2 to visualize the results. I tried to apply many of fucntions taught in class. Doing the homework I had some troubles.  
  
When I tried to use 'color=continent', the colors used on the plot was so similar that it was quite hard to distinguish one from others. I was just wondering if the colors are randomly assigned and I could change colors used on the plot using 'color=continent'.  
  
I used 'mutate(below_mean= ifelse(lifeExp<40, 1, 0))' to count the frequency of below_mean. At first, I tried 'filter(lifeExp < 40)', but I just realized that this code does not contain the frequency of 0.  
  
I wrote 'spread(key="year", value="freq_lifeExp")' to make the table readable. I tried with 'reshape(idvar= "year", timevar= "continent", direction= "wide")' but it did not work. I am just wondering how I can make reshape() work. 

I tried decent-looking table using 'knitr::kable(g4 %>% spread(key="continent", value="freq_lifeExp"))'. It is working locally on my RStudio but it seems like it is not working on github.

At the very last part of my work,
'fit_America <- lm(lifeExp ~ log(gdpPercap), 
                  data =filter(g5,continent=="America"))' This code did not work. I could run the code for all the other continents.
