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

-Para una máquina servidora se ha ejecutado ab -n 100000 -c 100 http://192.168.169.128/ >>resultados_ab_contra192168169128.txt
 
Para la maquina balanceadora nginx se ha ejecutado ab -n 100000 -c 100 http://192.168.169.131/ >>resultados_ab_contra192168169131.txt
 
Para la maquina balanceadora haproxy a se ha ejecutado ab -n 100000 -c 100 http://192.168.169.128/ >>resultados_ab_contra192168169128.txt

- Media

| **Máquina** | Time taken for tests(s) | Requests per second |Time per request(ms) |Failed requests |
| ---------- | --------------- | ----------------- | --------------- | ------------ |

|192.168.2.128|   33,1528      |       3025,638     |   0,3316         |  0  |

|192.168.2.130| 40,2122        |       2487,07   |    0,402         |   0  |

|192.168.2.131| 33,2198        |    3012,284      |    0,3322       |   0  |

-Desviación estandar

|**Máquina**|Time taken for tests(s)|Requests per second|Time per request(ms)|Failed requests|
|:----------:|:---------------:|:-----------------:|:---------------:|:------------:|
|192.168.2.128|  2,137423145  | 180,6480005 | 0,021243823 |  0  |
|192.168.2.130| 0,471661637  |  29,49641504     | 0,00484768  |  0  |
|192.168.2.131| 0,985280011  |  86,39511578  |   0,009705668   |   0  |



| Columna 1     | Columna 2     |
| ------------- | ------------- |
| Celda 1, col1 | Celda 2, col2 |
| Celda 3, col1 | Celda 3, col2 |