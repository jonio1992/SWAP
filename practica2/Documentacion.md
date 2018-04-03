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

objetivo1 img 1,2,3  

![img](https://github.com/jonio1992/SWAP/blob/master/practica2/img/1.png)  

![img](https://github.com/jonio1992/SWAP/blob/master/practica2/img/2.png)

![img](https://github.com/jonio1992/SWAP/blob/master/practica2/img/3.png)

objetivo 2 img 4,5  nos clonamos de la maquina 2 a la 1, ojo los comandos se hacen en la maquina 1
![img](https://github.com/jonio1992/SWAP/blob/master/practica2/img/4.png)

![img](https://github.com/jonio1992/SWAP/blob/master/practica2/img/5.png)

objetivo 3  img 6,7 creando accesos sin clave

![img](https://github.com/jonio1992/SWAP/blob/master/practica2/img/6.png)

![img](https://github.com/jonio1992/SWAP/blob/master/practica2/img/7.png)

objetivo 4  img 9

![img](https://github.com/jonio1992/SWAP/blob/master/practica2/img/9.png)
