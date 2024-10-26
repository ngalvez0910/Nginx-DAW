## NATALIA.COM

Creamos una carpeta “conf” donde metemos el fichero nginx.conf de nuestro sistema de Linux.

<img src="imgs/conf.png">
 
Creamos el directorio sites-available, donde se guardan todos los archivos de configuración de los sitios disponibles para Nginx.

<img src="imgs/sites-natalia.png">
 
Creamos la estructura básica del sitio web para natalia.com en una carpeta websites. Cuenta con una página principal (index.html) que los usuarios verán al ingresar al dominio, y una página personalizada de error 404 (error404.html).

<img src="imgs/websites-natalia.png">
 
En el archivo natalia.conf, debemos configurar varios parámetros para nuestro servidor web.
1.	listen: especifica el puerto en el que se ejecutará el sitio web.
2.	server_name: define el nombre del dominio principal para el servidor y su alias.
3.	root: define el directorio raíz desde donde se servirán los archivos para este dominio. En este caso /var/www/natalia.com.
4.	index: especifica que el archivo index.html será el archivo predeterminado que se cargará cuando un usuario acceda al dominio.
5.	location: especifica una página personalizada para errores 404
6.	error_log: define la ubicación donde se almacenarán los logs de errores.
7.  access_log: define la ubicación donde se almacenarán los logs de acceso.

<img src="imgs/natalia-conf.png">
 
Creamos un fichero docker-compose. Debe de lucir de la siguiente forma:

<img src="imgs/dockerCompose.png">
 
Debemos tener una carpeta scripts con nuestro fichero entrypoint.sh

<img src="imgs/scripts.png">
 
En nuestro entrypoint.sh debemos añadir los siguientes comandos para automatizar la creación de nuestro servicio con su configuración. 
1.	ln -s: crea enlaces simbólicos de los archivos de configuración de sites-available a sites-enabled.
2.  nginx -s reload: recarga la configuración de Nginx.
3.  nginx -g 'daemon off;': inicia Nginx en primer plano.

<img src="imgs/entrypoint-natalia.png">
 
En nuestro fichero hosts debemos añadir nuestro dominio con la IP de nuestro localhost.
 
<img src="imgs/hosts-natalia.png">


## GONZALEZ.COM

En el directorio sites-available, agregamos el archivo gonzalez.conf.

<img src="imgs/sites-gonzalez.png">
 
En el archivo gonzalez.conf, debemos configurar varios parámetros para nuestro servidor web.

<img src="imgs/gonzalez-conf.png">
 
Creamos la estructura básica del sitio web para gonzalez.com en la carpeta websites. Cuenta con una página principal (index.html) que los usuarios verán al ingresar al dominio, y una página personalizada de error 404 (error404.html).
 
<img src="imgs/websites-gonzalez.png">

Añadimos el enlace simbólico del archivo .conf al fichero entrypoint.sh.

<img src="imgs/entrypoint-gonzalez.png">
 
En nuestro fichero hosts debemos añadir nuestro dominio con la IP de nuestro localhost.
 
<img src="imgs/hosts-gonzalez.png">


## SEGURO.NET

En el directorio sites-available, agregamos el archivo seguro.conf.

<img src="imgs/sites-seguro.png">
 
En el archivo seguro.conf, debemos configurar varios parámetros para nuestro servidor web. En el puerto 80:
1.	listen: especifica el puerto en el que se ejecutará el sitio web.
2.	server_name: define el nombre del dominio principal para el servidor.
3.	return 301: redirige todas las url que estén con http a la página segura de https.

<img src="imgs/seguro1-conf.png">

En el puerto 443:
1. listen: especifica el puerto en el que se ejecutará el sitio web y su alias.
2. server_name: define el nombre del dominio principal para el servidor.
3. ssl_certificate y ssl_certificate_key: especifican la ubicación del certificado SSL y de la clave privada necesarios para establecer conexiones seguras.
4. ssl_protocols y ssl_ciphers: define los protocolos de seguridad que serán aceptados y los cifrados específicos para mantener la seguridad y compatibilidad con navegadores modernos. Además, ssl_prefer_server_ciphers asegura que el servidor dé prioridad a sus propios cifrados.
5. root: define el directorio raíz desde donde se servirán los archivos para este dominio. En este caso /var/www/seguro.net.
6. location: especifica una página personalizada para errores 401, 403, 404 y 500; y una página privada que solo se mostrará a los usuarios verificados.

<img src="imgs/seguro2-conf.png">
<img src="imgs/seguro3-conf.png">
 
Creamos la estructura básica del sitio web para seguro.net en la carpeta websites. Cuenta con una página principal (index.html) que los usuarios verán al ingresar al dominio, y una página personalizada de error 404 (error404.html), error 401 (error401.html), error 403 (error403.html) y error 500 (error500.html). Aparte, cuenta con una página única para usuarios aptos
 
<img src="imgs/websites-seguro.png">

Añadimos el enlace simbólico del archivo .conf al fichero entrypoint.sh.

<img src="imgs/entrypoint-seguro.png">

Creamos las carpetas certs y htpasswd

<img src="imgs/seguridad.png">

Ejecutamos el comando openssl passwd. Ponemos la contraseña que queramos.

<img src="imgs/comando-htpass.png">

Copiamos la contraseña a un archivo .htpasswd con el nombre del usuario.

<img src="imgs/contraseña.png">

En la consola de OpenSSL, ponemos el comando openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout seguro.key -out seguro.crt.
Ahora registraremos el país, provincia, localidad, organización, nombre, dominio y email.

<img src="imgs/comandoKey.png">
 
En nuestro fichero hosts debemos añadir nuestro dominio con la IP de nuestro localhost.
 
<img src="imgs/hosts-seguro.png">

Ejecutamos el Docker.

<img src="imgs/comando-docker.png">

Al final de todo, nuestro directorio debe tener la siguiente estructura:

<img src="imgs/carpetas.png">