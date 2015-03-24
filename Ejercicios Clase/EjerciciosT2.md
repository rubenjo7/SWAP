#Ejercicios Tema 2.

##Rubén Jiménez Ortega.

**2.1 Calcular la disponibilidad del sistema si tenemos dos réplicas de cada elemento (en total 3 elementos en cada subsistema).**

1.Disponibilidad Web

	Disponibilidad Web1 = 85%
	Disponibilidad Web2 = 85%+(1-85%)*85% = 97.75%
	Disponibilidad Web3 = 97.75%+(1-97.75%)*85% = 99.6625%
2.Application

	Application1 = 90%
	Application2 = 90%+(1-90)*90% = 99%
	Application3 = 99%+(1-99%)*90% = 99.9%
3.Database

	Database1 = 99.9%
	Database2 = 99.9%+(1-99.9%)*99.9% = 99.9999%
	Database3 = 99.9999%+(1-99.9999%)*99.9% = 99.99999999%
4.DNS

	DNS1 = 98%
	DNS2 = 98%+(1-98%)*98% = 99.96%
	DNS3 = 99.96%+(1-99.6%)*98% = 99.9992%
5.Firewall

	Firewall1 = 85%
	Firewall2 = 85%+(1-85%)*85% = 97.75%
	Firewall3 = 97.75%+(1-97.75%)*85% = 99.6625%
6.Switch

	Switch1 = 99%
	Switch2 = 99%+(1-99%)*99% = 99.99%
	Switch3 = 99.99%+(1-99.99%)*99% = 99.9999%
7.Data center

	Data Center1 = 99.99%
	Data Center2 = 99.99%+(1-99.99%)*99.99% = 99.999999%
	Data Center3 = 99.999999%+(1-99.999999%)*99.99% = 100%
8.ISP

	ISP1 = 95%
	ISP2 = 95%+(1-95%)*95% = 99.75%
	ISP3 = 99.75%+(1-99.75%)*95% = 99.9875%
	
Disponibilidad total:
 
 	Disponibilidad total = 99.6625% \* 99.9% \* 99.99999999% \* 99.9992% \* 99.6625% \* 99.9999% \* 100% \* 99.9875% = 99.21351663%

**2.2 Buscar frameworks y librerías para diferentes lenguajes que permitan hacer aplicaciones altamente disponibles con relativa facilidad. Como ejemplo, examina PM2 https://github.com/Unitech/pm2 que sirve para administrar clústeres de NodeJS.**

JGroups es un toolkit (multi-plataforma) escrito en Java que permite el intercambio de mensajes confiable(no se pierde ningún mensaje), se puede usar para crear clusters donde sus nodos pueden mandar mensajes entre ellos, sus características principales son:
	
	- la creación y eliminación de clusters, los nodos de los cluster pueden anclarse a través de LAN y WAN
	- Altas y bajas de los clusterse      
	- Detección de Membresía y notificación sobre nodos que  se han unido , dejado o que se han caído del cluster
	- Detección y eliminación de nodos caidos.

**2.3 ¿Cómo analizar el nivel de carga de cada uno de los subsistemas en el servidor? Buscar herramientas y aprender a usarlas. ...¡o recordar cómo usarlas!**

“Nagios es un sistema de monitorización de redes ampliamente utilizado, de código abierto, que vigila los equipos (hardware) y servicios (software) que se especifiquen, alertando cuando el comportamiento de los mismos no sea el deseado. Entre sus características principales figuran la monitorización de servicios de red (SMTP, POP3, HTTP, SNMP...), la monitorización de los recursos de sistemas hardware (carga del procesador, uso de los discos, memoria, estado de los puertos...), independencia de sistemas operativos, posibilidad de monitorización remota mediante túneles SSL cifrados o SSH, y la posibilidad de programar plugins específicos para nuevos sistemas.” 
	
	- fuente: https://es.wikipedia.org/wiki/Nagios

** 2.4 Buscar ejemplos de balanceadores software y hardware (productos comerciales). Buscar productos comerciales para servidores de aplicaciones. Buscar productos comerciales para servidores de almacenamiento.** 

Balanceadores Software:
	
	-ZVA64 EE 3110 Virtual Appliance (Zen Load Balancer) --> 
		http://www.zenloadbalancer.com/products/zva64-ee3110-virtual-appliance/
Balanceadores Hardware:
	
	-NetScaler de citrix  -->
		http://www.citrix.com/products/netscaler-application-delivery-controller/tech-info.html
	-BIG-IP de F5 --> 
		https://f5.com/products/platforms/appliances
