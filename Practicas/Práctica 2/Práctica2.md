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

