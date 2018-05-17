# Practica 5 SWAP   

### Replicación de bases de datos MySQL

###### Autores: Antonio Carrasco Castro, Fernando Roldán Zafra  

## Objetivos 
I. Crear una BD con al menos una tabla y algunos datos.  
II. Realizar la copia de seguridad de la BD completa usando mysqldump en la máquina principal y copiar el archivo de copia de seguridad a la máquina secundaria.  
III. Restaurar dicha copia de seguridad en la segunda máquina (clonado manual de la BD), de forma que en ambas máquinas esté esa BD de forma idéntica.  
IV. Realizar la configuración maestro-esclavo de los servidores MySQL para que la replicación de datos se realice automáticamente.  


## Preparativos
sudo apt install mysql-client-core-5.7



## -Sesión 5

### Nota 
Levantar ssh -> sudo /etc/init.d/ssh start  
Conectarse -> ssh user@ipUser  
Acciones balanceador  -> /etc/init.d/{haproxy, nginx} {start, status, stop}  

### Objetivo I Crear una BD con al menos una tabla y algunos datos.



![img](https://github.com/jonio1992/SWAP/blob/master/practica5/img/1.png)  

![img](https://github.com/jonio1992/SWAP/blob/master/practica5/img/2.png)  

![img](https://github.com/jonio1992/SWAP/blob/master/practica5/img/3.png)  

### Objetivo II Clonar manualmente BD entre máquinas.
![img](https://github.com/jonio1992/SWAP/blob/master/practica5/img/4.png)  

![img](https://github.com/jonio1992/SWAP/blob/master/practica5/img/5.png)  

![img](https://github.com/jonio1992/SWAP/blob/master/practica5/img/6.png)  
### Objetivo III Configurar la estructura maestro-esclavo entre dos máquinas para realizar el clonado automático de la información.




