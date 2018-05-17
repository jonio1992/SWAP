# Practica 4 SWAP   

### Asegurar la granja web

###### Autores: Antonio Carrasco Castro, Fernado Roldán Zafra  

## Objetivos 
I. Instalar un certificado SSL para configurar el acceso HTTPS a los servidores.  
II. Configurar las reglas del cortafuegos para proteger la granja web.  
 


## Preparativos



## -Sesión 4

### Nota 
Levantar ssh -> sudo /etc/init.d/ssh start  
Conectarse -> ssh user@ipUser  
Acciones balanceador  -> /etc/init.d/{haproxy, nginx} {start, status, stop}  

### Objetivo I Instalar un certificado SSL para configurar el acceso HTTPS a los servidores.
Lo primero que vamos a hacer es instalar los certificados SSL para poder acpetar peticiones HTTPS de un servidor, para ellos seguimos los pasos indicados en el guion:   
NOTA: 
  a2enmod ssl  
  service apache2 restart  
  
  debemos crear una carpeta donde almacenar los certificados, llamaremos a este ssl en la ruta:  
  /etc/apache2/ssl  
  
  Ahora tenemos que generar los cerificados  
    openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt  
  
  ahora para activarlo usamos y reiniciamos el servicio:  
  
a2ensite default-ssl   
  service apache2 reload  
![img](https://github.com/jonio1992/SWAP/blob/master/practica4/img/1.png)  

Y procedemos a comprobar si funciona el protocolo https  

Ahora se pueba con el balanceador para ver si lo acepta  

Para que funcione se a añadido en la configuracion del balanceador lo siguiente:  



### Objetivo II Configurar las reglas del cortafuegos para proteger la granja web.


