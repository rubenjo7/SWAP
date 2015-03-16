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

*export PS1="\u@$(ip addr show dev eth0 | grep "inet " | cut -d" " -f6) $"*
###Instalar la herramienta rsync
Yo ya lo tenia instalado por defecto en Ubuntu Server, pero si no lo hubiese tenido instalado únicamente tendríamos que usar el comando:

*sudo apt-get install rsync*

Ahora vamos a probar el funcionamiento clonando la carpeta con el contenido del servidor web:

![imagen] (https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%202/1.PNG)

