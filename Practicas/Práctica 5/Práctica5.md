# Práctica 5. Replicación de bases de datos MySQL.
Rubén Jiménez Ortega

Grupo: 3

#Objetivos de la práctica

Los objetivos concretos de esta práctica son:

• Copiar archivos de copia de seguridad mediante ssh.

• Clonar manualmente BD entre máquinas.

• Configurar la estructura maestro-esclavo entre dos máquinas para realizar el
clonado automático de la información.

#Crear una BD e insertar datos

Para el resto de la práctica debemos crearnos una BD en MySQL e insertar algunos
datos. Así tendremos datos con los cuales hacer las copias de seguridad. En todo
momento usaremos la interfaz de línea de comandos del MySQL:

![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%205/1.PNG)

![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%205/2.PNG)

Ya tenemos datos (un registro) insertados en nuestra BD llamada “datos”. Podemos
haber insertado más registros. Veamos cómo entrar y hacer una consulta:

![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%205/3.PNG)

#Replicar una BD MySQL con mysqldump

MySQL ofrece la una herramienta para clonar las BD que tenemos en nuestra
maquina. Esta herramienta es *mysqldump*.

**Mysqldump** es parte de los programas de cliente de MySQL, que puede ser utilizado
para generar copias de seguridad de BD. Puede utilizarse para volcar una o varias BD
para copia de seguridad o para transferir datos a otro servidor SQL (no
necesariamente un servidor MySQL). EL volcado contiene comandos SQL para crear
la BD, las tablas y rellenarlas.

Concretamente, las opciones --quick o --opt hacen que MySQL cargue el resultado
entero en memoria antes de volcarlo a fichero, lo que puede ser un problema si se
trata de una BD grande. Sin embargo, la opción --opt está activada por defecto.
La sintaxis de uso es:

	# mysqldump ejemplodb -u root -p > /root/ejemplodb.sql
 
 Así, en el servidor de BD principal (maquina1) hacemos:
 
 ![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%205/4.PNG)
 
 Ahora ya sí podemos hacer el mysqldump para guardar los datos. En el servidor
principal (maquina1) hacemos:
 
 ![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%205/5.PNG)
 
 Como habíamos bloqueado las tablas, debemos desbloquearlas (quitar el “LOCK”):
 
  ![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%205/6.PNG)
  
  Ya podemos ir a la máquina esclavo (maquina2, secundaria) para copiar el archivo
.SQL con todos los datos salvados desde la máquina principal (maquina1):

  ![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%205/7.PNG)
  
  y habremos copiado desde la máquina principal (1) a la máquina secundaria (2) los
datos que hay almacenados en la BD.

Con el archivo de copia de seguridad en el esclavo ya podemos importar la BD
completa en el MySQL. Para ello, en un primer paso creamos la BD:
 
   ![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%205/8.PNG)
   
#Replicación de BD mediante una configuración maestro-esclavo
   
La opción anterior funciona perfectamente, pero es algo que realiza un operador a mano.
   
MySQL tiene la opción de configurar el demonio para hacer replicación de las BD sobre un esclavo a partir de los datos que almacena el maestro.

Se trata de un proceso automático que resulta muy adecuado en un entorno de producción real. Implica realizar algunas configuraciones, tanto en el servidor principal como en el secundario.

A continuación se detalla el proceso a realizar en ambas máquinas:

Partimos teniendo clonadas las base de datos en ambas máquinas.

   ![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%205/9.PNG)
   
Lo primero que debemos hacer es la configuración de mysql del maestro. Para ello editamos, como root, el /etc/mysql/my.cnf y modificamos los siguientes parámetros:

Comentamos el parámetro bind-address que sirve para que escuche a un servidor:

	#bind-address 127.0.0.1
	
Le indicamos el archivo donde almacenar el log de errores. Por ejemplo al reiniciar el servicio, si cometemos algún error en el archivo de configuración en el archivo de log nos mostrará con detalle lo sucedido:

	log_error = /var/log/mysql/error.log

Establecemos el identificador del servidor.
	
	server-id = 1
	
El registro binario contiene toda la información que está disponible en el registro de actualizaciones, en un formato más eficiente y de una manera que es segura para las transacciones:

	log_bin = /var/log/mysql/bin.log
	
Guardamos el documento y reiniciamos el servicio:

	/etc/init.d/mysql restart

   ![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%205/10.PNG)

Si no nos da ningún error, vamos a la configuración de mysql el esclavo (mismo archivo).

La configuración es similar a la del maestro, con la diferencia de que el server-id en
esta ocasión será 2.

   ![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%205/11.PNG)
   
   Entramos en mysql y ejecutamos la siguiente sentencia (ojo con la IP del esclavo), para finalizar con la configuración en el maestro obtenemos los datos de la base de datos que vamos a replicar para posteriormente usarlos en la configuración del esclavo:
   
    ![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%205/12.PNG)
    
    Volvemos a la máquina esclava, entramos en mysql y le damos los datos del maestro. Estos datos se pueden introducir desde el archivo de configuración si trabajamos con versiones inferiores a mysql 5.5.
    
        ![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%205/13.PNG)
   
   Para demostrar que todo esto que hemos realizado es verdad y que funciona lo único que tenemos que hacer es irnos al maestro introducir nuevos datos a la base de datos y luego irnos al esclavo y mirar esa misma base de datos y comprobar que las dos máquinas tienen la misma base de datos.
   
   ![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%205/14.PNG)
   
   ![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%205/15.PNG)