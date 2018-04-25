# Practica 3 SWAP   

### Balanceo de carga

###### Autores: Antonio Carrasco Castro, Fernado Roldán Zafra  

## Objetivos 
I. Configurar una máquina e instalar el nginx como balanceador de carga.  
II. Configurar una máquina e instalar el haproxy como balanceador de carga.  
III. Someter a la granja web a una alta carga, generada con la herramienta Apache Benchmark, teniendo primero nginx y después haproxy.  


## Preparativos
Hay que recordar el programa rsync está activo por el crontab de la anterior práctica. Para facilitar esta práctica voy a deshabilitarlo del crontab y que no se sincronicen las carpetas html que usaré para diferencias cada máquina a la hora de las comprobaciones de las peticiones al balanceador.

Herramienta: nmap  
Muy util para ver los puertos ocupados con el siguiente comando:  

sudo nmap -sT -O localhost


## -Sesión 3  


### Nota 
Levantar ssh -> sudo /etc/init.d/ssh start  
Conectarse -> ssh user@ipUser  
Acciones balanceador  -> /etc/init.d/{haproxy, nginx} {start, status, stop}  

### Objetivo I Configurar una máquina e instalar el nginx como balanceador de carga.
Para esta práctica he creado una nueva maquina que hará de balanceador de carga hacia las otras dos máquinas usadas en las anteriores prácticas (SWAP1 y SWAP2).  


![img](https://github.com/jonio1992/SWAP/blob/master/practica3/img/1.png)  

Para la instalción de nginx, se han usado los comandos que se comentan en el guion de prácticas 3:  

sudo apt-get update && sudo apt-get dist-upgrade && sudo apt-get autoremove  

sudo apt-get install nginx  

/etc/init.d/nginx start  

Pasamos a la configuración de nginx. Una configuración básica sobre el archivo alojado en:   /etc/nginx/conf.d/default.conf  
 
![img](https://github.com/jonio1992/SWAP/blob/master/practica3/img/2.png)  

En esta imagen se muestra las ip de las máquinas servidoras y la configuración para la máquina que hará de balaceador de carga.

![img](https://github.com/jonio1992/SWAP/blob/master/practica3/img/3.png)  

![img](https://github.com/jonio1992/SWAP/blob/master/practica3/img/4.png)  


### Objetivo II Configurar una máquina e instalar el haproxy como balanceador de carga.

Para la instalción de haproxy, se han usado los comandos que se comentan en el guion de prácticas 3:  

* sudo apt-get install haproxy  
* sudo /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg  

Una vez instalado el programa haproxy en la máquina que va a balancear, nos vamos a su archivo de configuración alojado en: /etc/haproxy/haproxy.cfg.  

![img](https://github.com/jonio1992/SWAP/blob/master/practica3/img/5.png)  

Como se muestra en la imagen, se ve las ip de las máquinas servidoras y el archivo de configuración de haproxy.

![img](https://github.com/jonio1992/SWAP/blob/master/practica3/img/6.png)  

![img](https://github.com/jonio1992/SWAP/blob/master/practica3/img/7.png)  


### Objetivo III Someter a la granja web a una alta carga, generada con la herramienta Apache Benchmark, teniendo primero nginx y después haproxy.
Para esta parte se va usar el test ab (apache benchmark) para somenter el balanceador a alta carga.  
Para ello vamos a usar una máquina aparte del balanceador y los servidores. Debemos tener acceso a la maquina balanceadora pues no podemos tener los dos balanceadores(nginx y haproxy) activos a la vez. Usando el comando que hay en nota podremos parar, arrancar o comporabar el estado del balanceador.  

El comando para el benchmark es el siguiente:  

ab -n 1000 -c 10 http://IP:BALANCEADOR/index.html  

En mi caso estaba teniendo problemas con que tenía peticiones con estado failed, para arreglarlo añadimos la opcion "-l" (ele)  

 ab -l -n 100000 -c 20 http://IP:BALANCEADOR/index.html
 
 Esta opción es para cuando se tiene paginas dinámicas, que en mi caso supongo que pasa porque el mensaje de carga de index.html que hay en cada máquina servidora cambia y por eso existe este error.

![img](https://github.com/jonio1992/SWAP/blob/master/practica3/img/nginx.png)  
**test ab para nginx**

![img](https://github.com/jonio1992/SWAP/blob/master/practica3/img/haproxy.png)  

**test ab para haproxy**

Los test se han ejecutado en un ordenador sobremesa con algo mejor de CPU y tuve que cambiar las ip que ya que cambiaban de mi portatil al sobremesa en las maquinas virtuales.

Me ha salido que el test con los mismo parametros de carga y concurrencia, nginx es más rápido que haproxy realizando el test. También hay que recalcar que los tiempo de establecer la conecxión, tiempo necesario para servir una respuesta, y tiempo para obtener los primeros bit de la respuesta son menores en nginx que en haproxy aunque vemos que haproxy es menor en media de peticiones atendidas por segundo, aunque casi similar entre los dos balanceadores. Conclusión, me quedaría con nginx.


