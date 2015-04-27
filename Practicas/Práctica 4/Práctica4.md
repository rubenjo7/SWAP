# Práctica 4. Comprobar el rendimiento de servidores web.
Rubén Jiménez Ortega

Grupo: 3

#Solución

Para medir el rendimiento de un servidor necesitaremos una herramienta que ejecutar en los clientes para crear una carga HTTP específica. En algunos casos, las medidas se realizan con benchmarks como SPECweb o WebStone para simular un número determinado de clientes.

Existen diversas herramientas para comprobar el rendimiento de servidores web. Las
hay basadas en interfaz de línea de comandos y de interfaz gráfica. Entre las más
utilizadas destacan:
	
	• Apache Benchmark
	• httperf
	• openwebload
	• the grinder
	• OpenSTA
	• JMeter

Lo habitual es usar programas de línea de comandos que sobrecarguen lo mínimo posible las máquinas que estamos usando. En esta práctica usaremos las siguientes herramientas para comprobar el rendimiento de nuestra granja web recién configurada.

##Pruebas AB
###Comandos:

-Para una máquina servidora se ha ejecutado **ab -n 100000 -c 100 http://192.168.169.128/**
 
-Para la maquina balanceadora nginx se ha ejecutado **ab -n 100000 -c 100 http://192.168.169.131/**
 
-Para la maquina balanceadora haproxy a se ha ejecutado **ab -n 100000 -c 100 http://192.168.169.128/** 

- Media

|**Máquina**|Time taken for tests(s)|Requests per second|Time per request(ms)|Failed requests|
|:----------:|:---------------:|:-----------------:|:---------------:|:------------:|
|192.168.169.128|   33,1528      |       3025,638     |   0,3316         |  0  |
|192.168.169.129| 40,2122        |       2487,07   |    0,402         |   0  |
|192.168.169.131| 33,2198        |    3012,284      |    0,3322       |   0  |

- Desviación estandar

|**Máquina**|Time taken for tests(s)|Requests per second|Time per request(ms)|Failed requests|
|:----------:|:---------------:|:-----------------:|:---------------:|:------------:|
|192.168.169.128|  2,137423145  | 180,6480005 | 0,021243823 |  0  |
|192.168.169.129| 0,471661637  |  29,49641504     | 0,00484768  |  0  |
|192.168.169.131| 0,985280011  |  86,39511578  |   0,009705668   |   0  |

![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%204/1.PNG)

##Pruebas HTTPERF

**Comandos:**

-Para una máquina servidora se ha ejecutado **httperf --server 192.168.169.128 --port 80 --uri /index.html --rate 150 --num-conn 27000 --num-call 1 --timeout 5**
 
-Para la maquina balanceadora **nginx** se ha ejecutado **httperf --server 192.168.169.129 --port 80 --uri /index.html --rate 150 --num-conn 27000 --num-call 1 --timeout 5**
 
-Para la maquina balanceadora **haproxy** a se ha ejecutado **httperf --server 192.168.169.131 --port 80 --uri /index.html --rate 150 --num-conn 27000 --num-call 1 --timeout 5**

Se han realizado 5 medidas para cada máquina siendo su media y su desviación las indicadas en la tabla:

- Media

|**Máquina**|Total connections|replies|Request rate( req/s )|Errors total|
|:----------:|:---------------:|:-----------------:|:---------------:|:--------:|
|192.168.169.128|   27000      |       27000     |    150         | 0 |
|192.168.169.129| 27000      |      27000   |    150         | 0 |
|192.168.169.131| 27000        |    27000      |    150       | 0 |

- Desviación estandar

|**Máquina**|Total connections|replies|Request rate( req/s )|Errors total|
|:----------:|:---------------:|:-----------------:|:---------------:|:---------:|
|192.168.169.128|  0       |       0      |  0         |  0 |
|192.168.169.129| 0          |       0     |    0        |  0  |
|192.168.169.131| 0          |       0      |    0      |   0  |

![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%204/2.PNG)

##Pruebas OPENLOAD

**Comandos:**

-Para una máquina servidora se ha ejecutado **openload 192.168.169.128 10**
 
-Para la maquina balanceadora **nginx** se ha ejecutado **openload 192.168.169.129 10**
 
-Para la maquina balanceadora **haproxy** a se ha ejecutado **openload 192.168.169.131 10**

Se han realizado 5 medidas para cada máquina siendo su media y su desviación las indicadas en la tabla:

- Media

|**Máquina**|Total TPS|Avg. Response time(s)|Max Response time(s)|
|:----------:|:---------------:|:-----------------:|:---------------:|
|192.168.169.128|   8230,504      |       0,0034     |   0,0558
|192.168.169.129| 2043,68      |       0,005   |   0,12         | 
|192.168.169.131| 228,716        |    0,043      |    0,0578      | 

 - Desviación estandar

|**Máquina**|Total Request|Avg. Response time(s)|Max Response time(s)|
|:----------:|:---------------:|:-----------------:|:---------------:|
|192.168.169.128|  12272,60969      |       0,000894427       |   0,04844791         | 
|192.168.169.129| 52,35157209         |       0      |   0,182658151         | 
|192.168.169.131| 0,708822968         |       0.0      |   0,001788854        | 


![img](https://github.com/rubenjo7/SWAP/blob/master/Practicas/Pr%C3%A1ctica%204/3.PNG)

##Conclusiones:
**AB:**
En estas mediciones donde se ha usado una página estática básica como web se obtiene unos resultados *Time taken for tests* , *Requests per second* y *Time per requests* muy parecidos para una sola máquina y el balanceador *haproxy*, siendo peores para el balanceador *nginx*.

**HTTPERF:**
En este caso los resultados no son nada convincentes, tras haber consultado al profesor he decidido dejarlos por su indicación ya que hay muchos compañeros con el mismo resultado, este no es otro que obtener el mismo numero de *Total connections*, *replies*, *Request rate( req/s )* y *Errors total* en las tres casos estudiados. 

**OpenLoad:**
En este caso el resultado es favorable para una máquina sola, registrandose un mayor número de *Transactions Per Second* en esta, pero tambien obteniendose una mayor desviación. 
