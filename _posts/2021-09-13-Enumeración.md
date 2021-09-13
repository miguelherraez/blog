---
title: Enumercación
published: true
---

# [](#header-1) Fuzzing

El fuzzing es una tecnica de reconocimiento web que trata de descubrir paths usando fuerza bruta.

-NMAP : Con nmap podemos hacer fuzzing con el script http-enum, este metodo usa un diccionario de tan solo 1000 entradas por 
	lo que esta bien como reconocimiento inicial pero se deben usar otros metodos en caso de no encontrar nada interesante,
	el comando que hay que usar es el siguiente:
	
	-nmap -p80 10.10.10.233 --script http-enum -oN webScan

-Leyenda

	-p80 = Se escanea el puerto 80 ya que este es el que utiliza el protocolo http
	-oN = El resultado se guarda en formato nmap en el archivo webScan

-WFUZZ :Es una herramienta de fuzzing mucho mas completa que nmap, con esta podemos usar cualquier diccionario que tengamos, el
	comando para hacer fuzzing con esta herraemienta es el siguiente:
	
	-wfuzz -c -L -t 400 --hc=404 -w /usr/share/wordlist/dirbuster/directory-list-2.3-medium.txt http://10.10.10.233/FUZZ

-Leyenda

	-c = Para poner a color la salida.
	-L = Este parametro se usa para que cuando haya un codigo 301, que es un redirect a otra pagina, WFUZZ siga esta ruta.
	-t = Indica el numero de hilos que usaremos para hacer el ataque.
	--hc = Hide code, este parametro se usa para filtrar la salida, en este caso esconde todas las salidas con codigo = a 404
		tambien se puede usar hl para esconder las salidas con el numero de lineas especificado o sc para solo mostrar las 
		salidas con codigo = al especificado. 
	-w = Indica el diccionario que usaremos para el aaque por fuerza bruta.
	-http:// = Indica el servidor hacia el que queremos lanzar el fuzzing.
	-FUZZ = Palabra reservada de WFUZZ para indicar en que posicion se usaran las palabras del diccionario.

-GOBUSTER : Esta herramienta desarrollada en go trabaja muy bien con sockets.

  	-gobuster dir -u http://´ip´/ -w directory-list-2.3-medium.txt 
  
-Leyenda
  
   	-u = URL 
   	-w = Indica el diccionario que usara gobuster para el ataque por fuerza bruta.
   
Si con esto no encontramos nada de donde tirar podemos probar a buscar subdominios con gobuster se haria de la siguiente manera:

  	-gobuster vhost -u http://´ip´/ -w subdomains-top1million-110000.txt
 
Este diccionario no esta por defecto en parrot pero podemos descargarlo desde su repositorio de github.

# [](#header-1) Reconocimiento Wordpress

-WPSCAN : Es una herramienta que nos permite escanear una url para detectar posibles vulnerabilidades ademas de otros datos 
	  potencialmente interesantes.
	
	- wpscan --url http://url.com -e vp,u

-Leyenda

	--url = Indica la url a escanear.
	-e = Indica que queremos enumerar despues de escanear la url. Vp, vulnerabilities. U, possible users.

-WPSEKU.PY : Esta herramienta no esta instalada en parrot por defecto y habria que descargarla desde su repositorio en github
	     Para usarla vale con ejecutar el siguiente comando:

	   - python3 wpseku.py -u http://url.com 

-wp/wp-content/ : Todos los servidores wordpress tienen este directorio donde estan los distintos plugins instalados, 
		  no tiene permisos de lectura pero si no devuelve codigo de error significa que existe. Este directorio se puede 
		  fuzzear con wpscan o de forma manual usando wfuzz y un diccionario de plugins de wp.








