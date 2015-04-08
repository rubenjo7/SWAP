# Práctica 3. El servidor web nginx.
Rubén Jiménez Ortega

Grupo: 3
##Objetivos
• En esta práctica configuraremos una red entre varias máquinas de forma que tengamos un balanceador que reparta la carga entre varios servidores finales.

• El problema a solucionar es la sobrecarga de los servidores. Se puede balancear cualquier protocolo, pero dado que esta asignatura se centra en las tecnologías web, balancearemos los servidores HTTP que tenemos configurados.

• De esta forma conseguiremos una infraestructura redundante y de alta disponibilidad.

#Solución
**Nginx** es un servidor web ligero de alto rendimiento. Lo usan muchos sitios web conocidos.

Debido a su buen rendimiento, se usa como servidor web en lugar del Apache o IIS,
aunque uno de los usos más extendidos es como balanceador de carga en un cluster
web.

###Instalar nginx en Ubuntu Server 12.04

El proceso de instalación en Ubuntu se basa en el uso de apt-get.

Lo primero que debemos hacer es importar la clave del repositorio de software:

![imagen] (https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%203/1.PNG)

![imagen] (https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%203/2.PNG)

A continuación, debemos añadir el repositorio, editando el fichero /etc/apt/sources.list
y añadiendo al final las siguientes líneas:

![imagen] (https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%203/3.PNG)

Ahora ya podemos instalar el paquete del nginx:

Usamos primero:

	apt-get update
Y despúes: 

	apt-get install nginx

Una vez instalado, podemos proceder a su configuración como balanceador de carga.

###Balanceo de carga usando nginx

Creo el archivo /etc/nginx/conf.d/default.conf 

![imagen] (https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%203/4.PNG)

Lo edito de la siguiente forma:

![imagen] (https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%203/5.PNG)

Para probar si todo ha ido bien primero modifico los archivos index.html de los dos servidores Back-end poniendo su nombre y IP en el archivo, luego reinicio ngix y hago solicitudes http al balanceador, se ve en la imagen que el balanceador reenvía la primera solicitud primero a la maquina 2 y la segunda a la maquina 1:

![imagen] (https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%203/6.PNG)

Ahora edito el archivo de configuración para darle mas peso a la maquina 2 de forma que cada 3 peticiones una vaya a parar a la maquina 1 y dos a la maquina 2:

![imagen] (https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%203/7.PNG)

Como se puede apreciar los resultados se ajustan a lo comentado anteriormente:

![imagen] (https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%203/8.PNG)

Para hacer que todo el trafico proveniente del mismo IP vaya siempre al mismo back-end edito el archivo de configuración poniendo la directiva *ip_hash*:

![imagen] (https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%203/9.PNG)

Para hacer la conexión persistente edito el archivo de configuración poniendo la directiva *keepalive*:

![imagen] (https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%203/10.PNG)

###Opciones de configuración del nginx para establecer cómo le pasará trabajo a las máquinas servidoras finales

Un ejemplo de configuración seria el que sigue:

![imagen] (https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%203/11.PNG)

Tenemos 3 servidores el primero con un peso 3, el segundo con un peso 2. Además si devuelve 2 fallos de petición en un intervalo de 15 segundos se marcará como no disponible. El tercer servidor es el mismo balanceador escuchando por el puerto 8080 ya que el 80 lo usa nginx y esta marcado como backup, por lo que no se le mandará peticiones hasta que los otros 2 no estén disponibles. En location ponemos *health_check*, de manera que vaya preguntando el estado a los servidores cada 60 segundos y en caso que falle 3 veces la repuesta de algún servidor lo marque como no disponible.

##Balanceo de carga con haproxy

**Haproxy** es un balanceador de carga y también proxy, de forma que puede balancear
cualquier tipo de tráfico.

Veamos cómo instalar y configurar haproxy para realizar funciones de balanceo de
carga sencillas.

###Instalar haproxy

Primero paramos nginx y luego instalamos haproxy:

![imagen] (https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%203/12.PNG)

###Configuración básica de haproxy como balanceador de carga

Ahora hay que configurar el archivo /etc/haproxy/haproxy.cfg

Para empezar guardo una copia de seguridad del la configuración por defecto 
	sudo mv /etc/haproxy/haproxy.cfg /etc/haproxy/haproxy.cfg.backup 
y creo el nuevo archivo /etc/haproxy/haproxy.cfg como sigue :

![imagen] (https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%203/13.PNG)

###Comprobar el funcionamiento del balanceador

Una vez guardada la configuración ejecuto el comando sudo /usr/sbin/haproxy -f /etc/haproxy/haproxy.cfg y como no da salido ningun mensaje de error hago solicitudes http al balanceador, como se puede observar hace balanceo round-robin:

![imagen] (https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%203/14.PNG)
