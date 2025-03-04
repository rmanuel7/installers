# Instalar Apache

Para poder ejecutar Apache en tu ordenador Windows lo único que necesitas es el paquete de software adecuado para tu sistema operativo. En su página web, sin embargo, la fundación Apache Software solo pone a disposición el código fuente. 

Los archivos binarios ejecutables para Windows se encuentran en páginas como [Apache Lounge](https://www.apachelounge.com/download/). Este tutorial se basa en la versión 2.4.20 para sistemas de 64 bits descargada en el Apache Lounge (la versión disponible para descargar es siempre la más actual). Para utilizar Apache con Windows no necesitas instalar el programa.

![image](https://github.com/user-attachments/assets/c47e4d32-42a0-4d16-8750-aee2fbd61dd4)

<br />

1. Guarda el archivo `.zip` con el paquete de software en una carpeta de tu ordenador local.
2. Descomprime el archivo haciendo doble clic sobre el icono de la carpeta.
3. Copia la carpeta `Apache24` en `C:\`.

Ahora, todos los archivos que necesitas para la puesta en funcionamiento de tu servidor web Apache local se encuentran en `C:\Apache24`.

## Comprobar la instalación
Tras la instalación es recomendable realizar una prueba. Para ello, dirígete a `C:/Apache24` y abre la carpeta `bin`. Aquí se encuentra la aplicación `httpd`. Haciendo doble clic se inicia Apache.


## Error del sistema httpd.exe
Si instalas Apache en tu ordenador por primera vez, probablemente el sistema te hará saber que no se puede iniciar el servidor web porque no se ha encontrado el archivo `VCRUNTIME140.dll`.

Este problema tiene solución y es precisamente la instalación de los componentes que faltan. Al estar escrito en C++, Apache necesita un entorno de ejecución adecuado, en este caso Visual C++. También conocido como Microsoft Visual C++, se trata de un entorno de desarrollo integrado para aplicaciones en C, C++ y C++/CLI en el entorno Windows. Con los denominados [Visual C++ Redistributable Packages](https://www.microsoft.com/es-es/download/details.aspx?id=48145), se pueden instalar aquellos componentes del entorno de ejecución que falten, disponibles de forma gratuita en la página principal de Microsoft. Se instalan localmente haciendo doble clic en el archivo .exe.


## Error Apache AH00558
An Apache `AH00558: Could not reliably determine the server's fully qualified domain name` message is generated when Apache is not configured with a global `ServerName` directive. The message is mainly for informational purposes, and an AH00558 error will not prevent Apache from running correctly.

```
# Include the virtual host configurations:
IncludeOptional sites-enabled/*.conf

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet
ServerName 127.0.0.1
```

```
apachectl configtest
```
