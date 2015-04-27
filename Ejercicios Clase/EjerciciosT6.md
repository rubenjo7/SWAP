#Ejercicios Tema 6.

##Rubén Jiménez Ortega.

**6.1 Aplicar con iptables una política de denegar todo el tráfico en una de las máquinas de prácticas. Comprobar el funcionamiento. Aplicar con iptables una política de permitir todo el tráfico en una de las máquinas de prácticas. Comprobar el funcionamiento.**

iptables -F

iptables -X

iptables -Z

iptables -t nat -F

// Establecemos politica por defecto: DROP!!!

iptables -P INPUT DROP

iptables -P OUTPUT DROP

iptables -P FORWARD DROP

Con esto se aplica que se deniegue todo lo entrante/saliente, solo es necesario aplicar este iptable en la máquina deseada.* Aplicar con iptables una política de permitir todo el tráfico en una de las máquinas de prácticas.Comprobar el funcionamiento.

// FLUSH de reglas

iptables -F

iptables -X

iptables -Z

iptables -t nat -F

// Establecemos politica por defecto

iptables -P INPUT ACCEPT

iptables -P OUTPUT ACCEPT

iptables -P FORWARD ACCEPT

iptables -t nat -P PREROUTING ACCEPT

iptables -t nat -P POSTROUTING ACCEPT

Con esto se aplica que se acepte todo lo entrante/saliente, solo es necesario aplicar este iptable en la máquina deseada.

**6.2 Comprobar qué puertos tienen abiertos nuestras máquinas,
su estado, y qué programa o demonio lo ocupa.**

[https://github.com/rubenjo7/SWAP/blob/master/Ejercicios%20Clase/6.2.PNG](https://github.com/rubenjo7/SWAP/blob/master/Ejercicios%20Clase/6.2.PNG)

**6.3 Buscar información acerca de los tipos de ataques más comunes en servidores web, en qué consisten, y cómo se pueden evitar.**

Algunos ataques más comunes identificados son:

Keyloggers y Spyware. Dichos ataques permiten instalarse silenciosamente en la PC con el fin de enviar datos sobre la información que la víctima teclea o almacena en el sistema, incluso, sobre sus hábitos en Internet.

Backdoor o puerta trasera. Estas herramientas dan acceso remoto para controlar los sistemas infectados y, cuando son ejecutados, corren encubiertamente.

Inyección SQL. Es una técnica de ataque utilizada para explotar vulnerabilidades en páginas Web que tienen una ruta de comunicación con bases de datos.

Abuso al sistema vía acceso privilegiado. Es el abuso deliberado de recursos, accesos o privilegios concedidos a una persona por una organización.

Acceso no autorizado con credenciales predeterminadas. Son los métodos a través de los cuales los atacantes obtienen acceso a un dispositivo o sistema protegido con contraseñas y nombres de usuario predeterminados o estandarizados.

Violación de usos aceptables y otras políticas. En realidad, este ataque no distingue si fue cometido de manera accidental o premeditada, la violación a una política fue tener graves consecuencias.

Acceso no autorizado mediante listas de control de acceso débiles o mal configuradas (ACL). Cuando hay las condiciones el atacante puede accesar a recursos y llevar a cabo acciones sin que la víctima se dé por enterada.

Sniffers. Estas herramientas monitorean y capturan información a través de una red.