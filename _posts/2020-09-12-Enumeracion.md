---
title: Enumeracion
published: true
---

# [](#header-1)Enumeracion

1.-Crear una carpeta para tener el proceso documentado.

2.-Con la orden mkt, definida anteriormente, creamos las 4 carpetas necesarias para poder trabajar.

3.-Le hacemos un ping a la maquina que queramos enumerar para saber si esta activa y si tenemos conexion:

	- ping -c 10.10.10.233
3.1.-Con el ttl que obtenemos de este ping podemos saber que tipo de SO usa la maquina:
	
	OS	TTL
	
	Linux	64
	Windows	128
	Solaris	254

3.2.- Con el parametro -R podemos ver la ruta de nuestro ping a traves de la red.

4.-Enumeracion de los puertos abiertos de la maquina con nmap:

	- nmap 10.10.10.233 -p- --open -T5 -v -n -oG allPorts
	
-Leyenda

	-p- = Para escanear todos los puertos, si no se pone se escanean los 1000 puertos mas comunes.
	--open = Para devolver unicamente los puertos abiertos.
	-T5 = Cuanto mayor sea el numero mayor es la velocidad del escaneo pero a su vez mas ruidoso es este.
	-v = Vervose, muestra por pantalla el estado del escaneo, si no se pone los resultados no se ven hasta el final.
	-n = Evita que se use DNS, lo que agiliza el proceso.
	-oG = Exporta los resultados en formato grepeable al fichero allPorts

5.-Extraemos la informacion relevante del fichero allPorts con la herramienta extractPorts

6.-Deteccion de version y servicios con nmap:

	-nmap -sC -sV -p"puertos" 10.10.10.233 -oN targeted

-Leyenda

	-sC = Lanza scritps basicos de numeracion.
	-sV = Detecta la version y servicios de los puertos.
	-p = Indica los puertos que quieres escanear.
	-oN = Exporta los resultados en formato nmap.  
