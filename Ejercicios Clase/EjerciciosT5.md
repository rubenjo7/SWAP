#Ejercicios Tema 5.

##Rubén Jiménez Ortega.

**5.1 Buscar información sobre cómo calcular el número de conexiones por segundo.**

Nginx tiene un módulo, llamado HttpStubStatusModule, el cual nos ofrece la posibilidad de obtener un status de nginx, por lo que nos muestra entre una de otras cosas, el número de conexiones por segundo.

Se modifica el archivo nginx.conf y lo dejamos:

 	location /nginx_status {
       	 # Turn on stats
        	stub_status on;
        	access_log   off;
        	# only allow access from 192.168.1.5 #
        	allow 192.168.1.5;
       	deny all;
   	}

Guardamos y actualizamos el servidor nginx. Seguidamente abrimos un navegador y escribimos la url seguida de /nginx_status

* Numero de todas las conexiones abiertas = 578
* Conexiones aceptadas = 9582123
* Conexiones manejadas = 9582123
* Peticiones manejadas = 21897523


Una vez que tenemos esto, para calcular las conexiones por segundo quedaría calcular:

*Las solicitudes por conexión = peticiones manejadas / conexiones manejadas = 21897523/9582123 = 2,29 conexiones por segundo


**5.2 Revisar los análisis de tráfico que se ofrecen en: [http://bit.ly/1g0dkKj](http://www.monografias.com/trabajos93/protocolos-analisis-trafico-y-simulaciones-red/protocolos-analisis-trafico-y-simulaciones-red.shtml).**

Aparecen varios apartados:
	
	* ARP (Address Resolution Protocol).
	* TCP (Transmission Control Protocol).
	* Consulta ARP.
	* Consulta DNS.
	* Sesión TCP.
	* Cierre de Conexión.
	* Tráfico Total v/s Tráfico TCP.	

**5.3 Buscar información sobre características, disponibilidad para diversos SO, etc de herramientas para monitorizar las prestaciones de un servidor.**

Pplications Manager ofrece herramientas de monitorización y análisis específico para más de 50 servidores, aplicaciones, bases de datos, ERP, programas "middleware", servidores y tecnologías web, servidores de Exchange, sistemas virtuales, recursos de nube pública, etc.; todo desde una sola consola de administración integrada.

*Administración de rendimiento de aplicaciones y sistemas*

Applications Manager ofrece una monitorización exhaustiva de todos los componentes de sus aplicaciones, servidores y sistemas críticos. Ofrece herramientas para el análisis de las causas raíz y permite una adecuada planificación de capacidades, para los centros de datos heterogéneos.

*Vista global, con mapeo automático de relaciones y dependencias*

La visibilidad que aporta Applications Manager permite entender lo que está ocurriendo en todo momento en los complejos entornos de TI. Aporta una vista global de sus recursos, con la detección automática de recursos y el mapeo automático de las relaciones y dependencias entre las aplicaciones.

*Monitorización de rendimiento*

Obtenga métricas de rendimiento exhaustivas del conjunto completo de aplicaciones y servidores. Elimine los cuellos de botella y optimice el rendimiento de las aplicaciones en toda la empresa e Internet. Applications Manager le avisará automáticamente si detecta cualquier anomalía.

*Monitorización de la experiencia del usuario final*

Mida el rendimiento de las aplicaciones desde la perspectiva del usuario final. Asegúrese de que sus aplicaciones web se comportan de la manera esperada en todo momento.

*Monitorización de las transacciones web, desde la URL hasta la consulta de SQL*

Applications Manager permite identificar todos los cuellos de botella en las transacciones de negocio de punta a punta, comenzando desde una URL hasta llegar a la consulta SQL.
