Apuntes Week 2
========================================================

Seguimos viendo como se trata con archivos en distintos formatos

### MySQL

Hay que instalar: ver pdf

base de datos  tiene tablas que tiene registros

cada fila se llama record 

siempre estan linkadas por al menos una variable 


En primer lugar hay que conectar el R a la base de datos con dbConnect (y asignar a un objeto) y para sacar cosas se usa dbGetQuery y se pasa el comando como opcion, y acordarse de desconectar despues con dbDisconnect

en servidores grandes puede haber muchas DB, te conectas primero usas "show databases;" ves cuales son, te desconectas y luego te conectas con la opcion db="ladbquequiero" 

dbListTables  dice despues las tablas de esa DB en concreto 
dbListFields te da los campos de una tabla 

saber cuantas filas tiene una tabla

dbGetQuery(db,"select count(*) from tabla") 

Para conseguir una tabla

dbReadTable(db,"tabla") 



usar dbClearResult para limpiar las query cuando se acaban 



### HDF5


incluye metadata 

cada grupo tienen 0 o mas data sets y su metadata

group header con el nombre y atributos y group symbol table con la lista de objetos de cada grupo

datasets header con nombre tipo de datos dataspace y layout de almacenaje y un data array con los datos 

Mejor leer el pdf

### Leyedo de la red aka Web scrapping

