#Ejercicios Tema 4.

##Rubén Jiménez Ortega.

**4.1 Buscar información sobre cuánto costaría en la actualidad un mainframe. Comparar precio y potencia entre esa máquina y una granja web de unas prestaciones similares.**

Del siguiente enlace [IBM zEnterprise](http://www.inservice.com.ar/ibm-lanza-el-servidor-mainframe-zenterprise-mas-escalable-de-la-historia/) encuentro información sobre un nuevo mainframe que han sacado al mercado por la módica cantidad de 400 mil dolares. Es un ejemplo de lo caro que puede llegar a ser adquirir un mainframe. 

**4.2 Buscar información sobre precio y características de balanceadores hardware específicos. Compara las prestaciones que ofrecen unos y otros.**

A continuación diferentes [balanceadores](http://kemptechnologies.com/es/server-load-balancing-appliances/product-matrix.html) de la marca Barracuda con sus características y su correspondiente precio, es obvio y se observa que a mayor prestaciones mayor precio del producto. 

**4.3 Buscar información sobre los métodos de balanceo que implementan los dispositivos recogidos en el ejercicio 4.2.**

La familia de los Enterprise acepta los siguientes algoritmos de balanceo:

Scheduling and Balancing Methods: -Round Robin -Weighted Round Robin -Least Connection -Weighted Least Connection -Agent-based Adaptive -Chained Failover (Fixed Weighting)

La familia de los LM utiliza:

-Round Robin -Weighted Round Robin -Least Connection -Weighted Least Connection -Agent-based Adaptive -Chained Failover (Fixed Weighting) -Source-IP Hash

**4.4 Instala y configura en una máquina virtual el balanceador ZenLoadBalancer.**

Procedemos a instalar Zen Load Balancer basado en Debian

![img](https://github.com/rubenjo7/SWAP/blob/master/Ejercicios%20Clase/Ejercicio%204.4/1.PNG)

Le ponemos por ejemplo como IP 192.168.1.103

![img](https://github.com/rubenjo7/SWAP/blob/master/Ejercicios%20Clase/Ejercicio%204.4/2.PNG)

La configuración se realiza a través de un entorno web. Organizando los servidores entorno a grupos (granjas en este caso) y permite configurar las opciones típicas, protocolos, puertos, ips virtuales, etc.

Una vez insalado para acceder a la configuración accederemos a la url: https://192.168.1.103:444

![img](https://github.com/rubenjo7/SWAP/blob/master/Ejercicios%20Clase/Ejercicio%204.4/3.PNG)

Introducimos usuario y contraseña que por defecto es admin / admin y veremos el dashboard de nuestro nuevo balanceador:

![img](https://github.com/rubenjo7/SWAP/blob/master/Ejercicios%20Clase/Ejercicio%204.4/4.PNG)

Seguidamente configuramos una granja de balanceo:

Seleccionamos el nombre, el protocolo a balancear, la ip virtual de la granja y el puerto a balancear:

![img](https://github.com/rubenjo7/SWAP/blob/master/Ejercicios%20Clase/Ejercicio%204.4/5.PNG)

Ya tendríamos creada nuestra granja a falta de incluir los servidores miembros y configurar las opciones de balanceo:

![img](https://github.com/rubenjo7/SWAP/blob/master/Ejercicios%20Clase/Ejercicio%204.4/6.PNG)

Estas son algunas de las opciones de balanceo ofrecidas:

![img](https://github.com/rubenjo7/SWAP/blob/master/Ejercicios%20Clase/Ejercicio%204.4/7.PNG)


Tanto la instalación como la configuración me han parecido más fácil que con nginx y haproxy.


**4.5 Probar las diferentes maneras de redirección HTTP. ¿Cuál es adecuada y cuál no lo es para hacer balanceo de carga global? ¿Por qué?.**

Principalmente hay 2 tipos de redirecciones:

* Redireccionamiento 301: Se puede definir este tipo de redireccion como “PERMANENTE”. Esto indica que todo contenido de una URL antigua se mueva de forma permanente a la URL nueva. De esta manera los buscadores dejarán de tener en cuenta la antigua URL y le traspasarán “aproximadamente” el 90% de la fuerza SEO a la nueva Web.

* Redireccionamiento 302: Se puede definir este tipo de redirección como “TEMPORAL”. Esto indica que todo el contenido de una URL antigua se mueva de forma temporal a la URL nueva. De esta manera redirigimos a los buscadores y usuarios de la antigua URL a la nueva pero no traspasamos la fuerza del SEO de una a otra.

**4.6 Buscar información sobre los bloques de IP para los distintos países o continentes. Implementar en JavaScript o PHP la detección de la zona desde donde se conecta un usuario .**

A continuación pongo varios enlaces en los que hay diversa información acerca de esta cuestión:

* http://www.monografias.com/trabajos28/geotargeting-mostrar-contenidos-pais-visitante/geotargeting-mostrar-contenidos-pais-visitante.shtml

* http://www.genbeta.com/actualidad/las-ultimas-direcciones-ipv4-se-han-agotado-ipv6-es-la-solucion


**4.7 Buscar información sobre métodos y herramientas para implementar GSLB.**

A continuación pongo dos enlaces en los que hay diversa información acerca de esta cuestión:

* http://www.clm.com.pe/productos/a10/ax-global-server-load-balancing.htm
* http://luisarizmendi.blogspot.com.es/2013/11/arquitectura-multidatacenter.html