#Ejercicios Tema 7.

##Rubén Jiménez Ortega.

**7.1 ¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 0 a partir de dos discos de 100 GB y 100 GB?**
	
	Con dos discos de 100GB se obtiene un RAID 0 de 200GB.

**¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 0 a partir de tres discos de 200 GB cada uno?**
	
	Con estos tres discos se obtiene un RAID 0 de 600GB de capacidad.

**7.2 ¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 1 a partir de dos discos de 100 GB y 100 GB? .**

	Al ser un RAID 1 se tratan como hardware independientes, por tanto sería 100GB.

**¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 1 a partir de tres discos de 200 GB cada uno? **

	Al ser un RAID 1 se tratan como hardware independientes, por tanto sería 200GB.

**7.3 ¿Qué tamaño de unidad de unidad RAID se obtendrá al configurar un RAID 5 a partir de tres discos de 120 GB cada uno? .**

	Al ser un RAID 5, se utiliza 1 para paridad de los datos. Por tanto, seria 120 + 120 = 240GB, siendo el último 120 que se queda para paridad de los datos.

**7.4 Buscar información sobre los sistemas de ficheros en red más utilizados en la actualidad y comparar sus características. Hacer una lista de ventajas e inconvenientes de todos ellos, así como grandes sistemas en los que se utilicen.**

NFS permite compartir datos entre varios ordenadores de una forma sencilla. Por ejemplo, un usuario validado en una red no necesitará hacer login a un ordenador específico: vía NFS, accederá a su directorio personal (que llamaremos exportado) en la máquina en la que esté trabajando. 

Pero NFS no es un protocolo demasiado eficiente y es muy lento para conexiones mediante módem. Está diseñado para redes locales, siendo muy flexible. Ofrece muchas posibilidades tanto a usuarios como a administradores.