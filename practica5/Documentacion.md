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
![img](https://github.com/jonio1992/SWAP/blob/master/practica5/img/7.png)  

![img](https://github.com/jonio1992/SWAP/blob/master/practica5/img/8.png)  


### Objetivo IV Realizar la configuración maestro-esclavo de los servidores MySQL para que la replicación de datos se realice automáticamente.

La atomatizacion del proceso de clonado de BD sobre una máquina a otra(Master-slave, Master-Master), se debe iniciar sobre el archivo de configuracion de mysql de la máquina master en mi caso SWAP1.  
Este archivo se aloja en /etc/mysql/mysql.conf.d/mysqld.cnf  en el que se van a hacer las siguientes modificaciones  
1) Comentamos la linea "bind-address"

![img](https://github.com/jonio1992/SWAP/blob/master/practica5/img/9.png)  
 
2) El archivo de almacenamiento de log errores esta descomentado por defecto, lo dejamos así.  

3) Descomentar la linea server-id = 1  

4) Descomentar la linea log_bin = /var/log/mysql/mysql-bin.log  

Guardamos el fichero y reiniciamos el servicio  
/etc/init.d/mysql restart  

En este punto, cambiamos a la máquina esclava ( SWAP2) y hacemos en el mismo archivo de configuración pero para esta máquina los siguientes pasos:  

1) Comentamos la linea "bind-address"
 
2) El archivo de almacenamiento de log errores esta descomentado por defecto, lo dejamos así.  

3) Descomentar la linea server-id = 1 y la modificamos por server-id = 2   

4) Descomentar la linea log_bin = /var/log/mysql/mysql-bin.log  

NOTA: si estamos en versiones de mysql (<) 5.5 ver; hay que seguir una configuración adiccional,  indicar estos datos relativos al master en el archivo de configuración. En mi caso no hace falta:  
 Master-host = ipMaestro  
Master-user = usuariosDB  
Master-password = contraseñaMaestro  

Guardamos el fichero y reiniciamos el servicio  
/etc/init.d/mysql restart  

Nota: si da algún fallo, revisar la configuración, si no encontramos el fallo mejor reinsalar el servicio o la máquina completa.  

Desde este punto, ya podemos configurar las maquinas maestro-esclavo desde mysql, para ello iniciamos mysql en la máquina master:  

sudo mysql -uroot -p  

Hay que crear un usuario y le darle permisos de acceso para la replicación. Dentro de mySQL ejecutamos lo siguiente:
![img](https://github.com/jonio1992/SWAP/blob/master/practica5/img/10.png)  

Usamos SHOW MASTER STATUS; para ver información necesaria para el slave.  
![img](https://github.com/jonio1992/SWAP/blob/master/practica5/img/11.png)  

Con la información anterior, usamos la ip de la máquina maestra, el log file y position:  
![img](https://github.com/jonio1992/SWAP/blob/master/practica5/img/12.png)  

Vemos el estado del slave para ver que puede capturar modificaciones en las tablas del master  
![img](https://github.com/jonio1992/SWAP/blob/master/practica5/img/13.png)  

Un ejemplo de copiado automático:  
![img](https://github.com/jonio1992/SWAP/blob/master/practica5/img/14.png)  







