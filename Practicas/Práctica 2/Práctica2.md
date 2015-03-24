# Práctica 2
Rubén Jiménez Ortega

Grupo: 3
##Objetivos
• Aprender a copiar archivos mediante ssh.

• Clonar contenido entre máquinas.

• Configurar el ssh para acceder a máquinas remotas sin contraseña.

• Establecer tareas en cron.

#Solución
Para la realización de de esta práctica voy a utilizar una conexión a la máquina virtual a través de *putty*.

Lo primero que voy a realizar es identificar cada máquina virtual de la forma que recomendó el profesor mediante el siguiente comando:

*$export PS1="\u@$(ip addr show dev eth0 | grep "inet " | cut -d" " -f6) $"*
###Instalar la herramienta rsync
Yo ya lo tenia instalado por defecto en Ubuntu Server, pero si no lo hubiese tenido instalado únicamente tendríamos que usar el comando:

*$sudo apt-get install rsync*

Ahora vamos a probar el funcionamiento clonando la carpeta con el contenido del servidor web:

![imagen] (https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%202/1.PNG)

###Acceso sin contraseña para ssh
El uso de rsync nos será de gran ayuda para mantener el contenido de varias máquinas actualizado e idéntico en todas ellas. Sin embargo, esa actualización debería hacerse automáticamente, a través de scripts que no requieran la intervención del administrador que vaya tecleando las contraseñas.

Es más, al realizar scripts que se conectan mediante ssh a equipos remotos para ejecutar alguna acción (p.ej. copias de seguridad o clonado) nos podemos encontrar que se queden esperando la contraseña.

Mediante ssh-keygen podemos generar la clave, con la opción -t para el tipo de clave. Así, en la máquina secundaria ejecutaremos:

*$ ssh-keygen -t dsa*

![imagen](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%202/2.PNG)

El siguiente paso es copiar la clave pública en la máquina secundaria.

![imagen](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%202/3.PNG)

A continuación ya podremos conectarnos a dicho equipo sin contraseña:

![imagen](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%202/4.PNG)

Para ejecutar comandos simplemente deberemos añadirlo al final del comando ssh
para conectarnos:

![imagen](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%202/5.PNG)

Enviaremos un fichero entre ambas máquinas para corroborar el funcionamiento de la conexión. Para esto, he creado un archivo *nuevo.txt*

![imagen](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%202/6.PNG)

Comprobamos en la máquina 1 que se recibió el fichero.

Concluido lo relacionado con la conexión ssh comenzaremos con el clonado de la carpeta /var/www entre ambas máquinas mediante la orden rsync.

![imagen](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%202/7.PNG)

Comprobamos que se han transferido los ficheros de la máquina principal a la secundaria para que ambos directorios sean totalmente iguales.

![imagen](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%202/8.PNG)

###Programar tareas con crontab

Cron es un administrador procesos en segundo plano que ejecuta procesos en el
instante indicado en el fichero crontab.

Accedemos el fichero /etc/crontab de la máquina secundaria y añadiremos lo siguiente al fichero:

![imagen](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%202/9.PNG)

Reiniciamos el servicio con *service cron restart*.

Esperamos unos minutos y realizamos el ls en la máquina secundaria:

![imagen](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%202/10.PNG)