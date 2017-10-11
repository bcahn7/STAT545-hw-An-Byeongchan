
# Stat545 hw04

[link to STAT545-hw04-An-Byeongchan.md](STAT545-hw04-An-Byeongchan.md)  

 
[link to STAT545-hw04-An-Byeongchan.Rmd](STAT545-hw04-An-Byeongchan.Rmd)  
[link to STAT545-hw04-An-Byeongchan.html](STAT545-hw04-An-Byeongchan.html)

## Report my progress

I tried to use some `join` functions to combine two datasets. Also, I utilized `gather()` and `spread()` for reshaping a dataset.   
  
I realized that when using `spread()`, I lose the column headers for "key" and "value". It would be good to indicate what the values are as the "value" header disappears. 

I learned that I needed to put quote key for `Korea, Rep.` because there exists a space. For example, ```ggplot(aes(x = `Korea, Rep.`, y = Japan))```

`geom_abline()` create reference lines. Similarly, `geom_hline()` is for horizontal lines and `geom_vline()` is for vertical lines. This helps to analyze and interpret plots.