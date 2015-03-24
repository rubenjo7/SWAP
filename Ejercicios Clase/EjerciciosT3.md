#Ejercicios Tema 3.

##Rubén Jiménez Ortega.

**3.1 Buscar con qué órdenes de terminal o herramientas gráficas
podemos configurar bajo Windows y bajo Linux el
enrutamiento del tráfico de un servidor para pasar el
tráfico desde una subred a otra.**

En Linux encontramos el comando echo "1" > /proc/sys/net/ipv4/ip_forward para activar el enrutamiento, este se activa al poner dicha variable a 1, acto seguido habría que configurar el filtrado de paquetes para que acepte el redireccionamiento desde dentro hacia fuera de nuestra red. Suele configurarse utilizando dos tarjetas de red y empleandose reglas de tipo iptables como por ejemplo: // Haciendo NAT en el servidor sudo iptables -A FORWARD -j ACCEPT sudo iptables -t nat -A POSTROUTING -s 10.0.0.0/8 -o eth0 -j MASQUERADE

Para Windows nuevamente es recomendable el uso de dos tarjetas de red y para su configuración basta con acceder a las Herramientas Administrativas y configurar paso a paso ( es guiado ) el Servicio de Enrutamiento y Acceso Remoto de Windows Server 2008. Comandos como route -p add [destino] [mask ] [puerta de enlace] [metric ] [if ] (para IPv4) o netsh interface ipv6 add route [prefix=]/ [interface=][[nexthop=]] [[siteprefixlength=]] [[metric=]] [[publish=]] [[validlifetime=]|infinite] [[preferredlifetime=]] [[store=]] tambien son utilizables si se desea por la opción manual que es mucho mas tediosa bajo Microsoft.

**3.2 Buscar con qué órdenes de terminal o herramientas gráficas podemos configurar bajo Windows y bajo Linux el filtrado y bloqueo de paquetes.**

En  Linux/Unix un breve resumen de los comandos es el siguiente:

	iptables –F : flush de reglas
	iptables –L : listado de reglas que se estan aplicando
	iptables –A : añadir regla
	iptables –D : borrar una regla o varias, etc…
	
En Windows según su página oficial accediendo a Configuración del equipo\Directivas\Configuración de Windows\Configuración de seguridad\Firewall de Windows con seguridad avanzada\Firewall de Windows se puede configurar manualmente el filtrado y bloqueo de paquetes. En relación a comandos realmente no viene claro su uso.