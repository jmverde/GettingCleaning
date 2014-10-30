Apuntes semana 4
========================================================

Que tengo que cogerlos a toda leche por que resulta que hacen falta las expresiones reguleras para el proyecto

Editing text variables
-----------------------

tolower() autoexplicativa

strsplit  sirve para separar cadenas por un caracter o cadena  ojo caracteres reservados hay que escaparlos con \\

quitar puntos y quedarte con lo primero sapply(lista con los splits,firstElement) con firstElement<-function(x){x[1]} 

substituir caracteres 
sub(c1,c2,datos,) substituye el primero 
gsub  substituye todas las instancias 

grep(cadena,lista) devuelve en que numero de la lista esta la cadena (y creo que eso vale para la parte dos del asunto del trabajo)


```r
cosa <- c("me", "mea", "meo")
grep("me", cosa)
```

```
## [1] 1 2 3
```


si se pone value = T  en vez de dar la lista da los valores 

stringr tiene alguna funcion chula
sbstr para sacar cachos 
paste para pegar cadenas
paste0 no pone espacios 
str_trim para eliminar espacios al final


Expresiones reguleras
-----------------------



dplyr b
------- 

Encadenamiento de derecha a izquierda (lo que seria una composicion de funciones)   se hace con %>% y se aplica en lo que sea el primer argumento 

datos %>%
by_group(grupos) %>%
summarize(mean(n)) %>%
print()

se puede ver mas haciendo ?chain

tidyr
-----

depende mucho de dplyr 

gather hace meltings tambien 

separate mola: sirve para separar varias variables en la misma columna, cuando se ponen en cosas como texto chico_grupoA 


lubridate
----- 
se puede usar para seguir fechas 


today() da la fecha de hoy 

year(), month y day retornan justamente eso 

wday da el dia de la semana, 1 domingo y seguimos 
now() da un date time y se puede usar hour, minute y second


 Fortunately, lubridate offers a variety of functions for parsing date-times. These
| functions take the form of ymd(), dmy(), hms(), ymd_hms(), etc., where each letter in the
| name of the function stands for the location of years (y), months (m), days (d), hours
| (h), minutes (m), and/or seconds (s) in the date-time being read in.  y lo lee en POSIXct

para cambiar uno se usa update 

se pueden usar tzone para poner otras zonas horarias 

se puede somar tiempo con days(3) 
with_tz sirve para cambiar de zona horaria


