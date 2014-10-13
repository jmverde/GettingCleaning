Test2 Question 4
========================================================


How many characters are in the 10th, 20th, 30th and 100th lines of HTML from this page: 

http://biostat.jhsph.edu/~jleek/contact.html 

(Hint: the nchar() function in R may be helpful)



Empezamos por bajar la web 


```r
conect <- url("http://biostat.jhsph.edu/~jleek/contact.html ")
htmlcode <- readLines(conect)
close(conect)
```


despues aplicamos con lapply en nchar 


```r
a <- lapply(htmlcode, nchar)

unlist(a[c(10, 20, 30, 100)])
```

```
## [1] 45 31  7 25
```

