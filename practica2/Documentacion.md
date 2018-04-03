# Practica 2 SWAP   

### Clonar la información de un sitio web

###### Autores: Antonio Carrasco Castro, Fernado Roldán Zafra  

## Objetivos 
I.Probar el funcionamiento de la copia de archivos por ssh  
II. Clonado de una carpeta entre las dos máquinas. configuración de ssh  
III. Para acceder sin que solicite contraseña  
IV. Establecer una tarea en cron que se ejecute cada hora para mantener actualizado el contenido del directorio /var/www entre las dos máquinas 

## Preparativos

Si hiciera falta instalar el siguiente programa
sudo apt-get install rsync

## -Sesión 2  
Una vez instalado procedemos al objetivo uno, conexión SSH:

### Nota 
Levantar ssh-> sudo /etc/init.d/ssh start  
Conectarse-> ssh user@ipUser  

### Objetivo I

Se va a copiar archivos de una maquina a otra  con el comando de ssh de la siguiente manera:  
tar czf - directorio | ssh equipodestino 'cat > ~/tar.tgz'  

Copiado de SWAP1 a SWAP2  

![img](https://github.com/jonio1992/SWAP/blob/master/practica2/img/1.png)  
Copiado de SWAP2 a SWAP1  
![img](https://github.com/jonio1992/SWAP/blob/master/practica2/img/2.png)  
Muestro todo lo copiado de una maquina a la otra  
![img](https://github.com/jonio1992/SWAP/blob/master/practica2/img/3.png)  

### Objetivo II
Para el clonado de archivos y directorios de una máquina a otra, usamos el comando 'rsync'.  
Voy a clonar de la maquina 2 a la 1, **ATENCIÓN**, los comandos se hacen en la maquina 1.
Se muestra un ejemplo:  
![img](https://github.com/jonio1992/SWAP/blob/master/practica2/img/4.png)  

Como se sabe de la documentación de la sesión 1, pru2.html pertenece a la maquina SWAP2, con lo que se ha clonado con exito en la maquina SWAP1. Instantanea mostrandolo:  
![img](https://github.com/jonio1992/SWAP/blob/master/practica2/img/5.png)  

### Objetivo III Creando accesos ssh sin clave  

Tenemos que crear la clave publica y privada para la conecxión a la otra maquina sin necesidad de clava con el comando :  
ssh-keygen -b 4096 -t rsa  


![img](https://github.com/jonio1992/SWAP/blob/master/practica2/img/6.png)  

Para decirle a la otra maquina quienes somos, usamos el siguiente comando:  
ssh-copy-id "nombremaquina@ipmaquina".

![img](https://github.com/jonio1992/SWAP/blob/master/practica2/img/7.png)  

### Objetivo IV
Con permisos de root, modificamos el archivo /etc/crontab añadiendole una nueva orden para poder ejecutar procesos en segundo plano cada hora. El resultado se muestra en la siguiente imagen.  
![img](https://github.com/jonio1992/SWAP/blob/master/practica2/img/9.png)  
