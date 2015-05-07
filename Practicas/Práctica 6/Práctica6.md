# Práctica 6. Discos en RAID.
Rubén Jiménez Ortega

Grupo: 3

#Objetivos de la práctica

Los objetivos concretos de esta práctica son:

• Configurar dos discos en RAID 1 (los discos se añadirán a un sistema ya instalado y funcionando).

• Hacer pruebas de retirar y añadir un disco y comprobar que el RAID sigue funcionando correctamente.

#Configuración del RAID por sofware

Como se ha indicado, partimos de una máquina virtual ya instalada y configurada a la
que, estando apagada, añadiremos dos discos del mismo tipo y capacidad.

Ahora arrancamos la máquina y entramos para instalar el software necesario para
configurar el RAID:

![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%206/1.PNG)

Debemos buscar la información de ambos discos:

![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%206/2.PNG)

Ahora ya podemos crear el RAID 1, usando el dispositivo /dev/md0, indicando el
número de dispositivos a utilizar (2), así como su ubicación:

![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%206/3.PNG)

Una vez creado el dispositivo RAID, le damos formato:
	
	sudo mkfs /dev/md0

Ahora ya podemos crear el directorio en el que se montará la unidad del RAID, y comprobamos su estado:
 
 ![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%206/4.PNG)
 
 Para finalizar el proceso, conviene configurar el sistema para que monte el dispositivo RAID creado al arrancar el sistema. Para ello debemos editar el archivo /etc/fstab:
 
 ![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%206/5.PNG)
 
 #Simular un fallo en uno de los discos del RAID (mediante comandos con el mdadm).
 
 Ahora vamos a simular un fallo de disco a propósito:
 
  ![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%206/6.PNG)
  
  Como vemos, uno de los discos ha caído, pero el otro no. Ahora vamos a eliminar el disco caido, esto lo hacemos así:

  ![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%206/7.PNG)
  
Finalmente vamos a añadirlo de nuevo y comprobar que todo esta bien, si nos fijamos esta "rebuilding", es decir sincronizando de nuevo el disco.
 
   ![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%206/8.PNG)
   