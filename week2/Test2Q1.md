Test2 Question 1 
========================================================



Register an application with the Github API here https://github.com/settings/applications. Access the API to get information on your instructors repositories (hint: this is the url you want "https://api.github.com/users/jtleek/repos"). Use this data to find the time that the datasharing repo was created. What time was it created? This tutorial may be useful (https://github.com/hadley/httr/blob/master/demo/oauth2-github.r). You may also need to run the code in the base R package and not R studio.


Voy a hacerlos en archivos distintos para no cargar la API de GitHub cuando este con otras preguntas 


Esto de todas fromas hay que correrlo a mano, lo dejo aqui asi, pero para crear el token hay que hacerlo de forma interactvia


En primer lugar he registrado la aplicacion en GitHub

Cargamos el package 


```r
library(httr)
```


cargamos la aplicacion como cuentan aca https://github.com/hadley/httr/blob/master/demo/oauth2-github.r


```r
oauth_endpoints("github")
```

```
## <oauth_endpoint>
##  authorize: https://github.com/login/oauth/authorize
##  access:    https://github.com/login/oauth/access_token
```

```r

myapp <- oauth_app("github", key = "7e2c48d888343d3779d7", secret = "fa231d3509ee0c3768584bebaa3d05ce44657934")

github_token <- oauth2.0_token(oauth_endpoints("github"), myapp)
```

```
## Error: oauth_listener() needs an interactive environment.
```

```r

gtoken <- config(token = github_token)
```

```
## Error: object 'github_token' not found
```



Por ahora esto solo es una prueba


```r
req <- GET("https://api.github.com/rate_limit", gtoken)
```

```
## Error: object 'gtoken' not found
```

```r
stop_for_status(req)
```

```
## Error: object 'req' not found
```

```r
content(req)
```

```
## Error: object 'req' not found
```



La web a consultar seria "https://api.github.com/users/jtleek/repos" 


```r
consult <- GET("https://api.github.com/users/jtleek/repos", gtoken)
```

```
## Error: object 'gtoken' not found
```

```r
stop_for_status(consult)
```

```
## Error: object 'consult' not found
```




Lo procesamos un poco


```r
datjson <- content(consult)
```

```
## Error: object 'consult' not found
```

```r
library(jsonlite)
```

```
## Warning: package 'jsonlite' was built under R version 3.1.1
```

```
## 
## Attaching package: 'jsonlite'
## 
## The following object is masked from 'package:utils':
## 
##     View
```

```r

datjson2 <- jsonlite::fromJSON(toJSON(datjson))
```

```
## Error: object 'datjson' not found
```



Ahora que ya es un data frame seleccionamos el repositorio que nos preguntan 
(para llegar aqui hay que jugar un poco con names para saber como se llama la columna que queremos )

```r
datdatash <- datjson2[datjson2$name == "datasharing", ]
```

```
## Error: object 'datjson2' not found
```

```r
datdatash$created_at
```

```
## Error: object 'datdatash' not found
```

