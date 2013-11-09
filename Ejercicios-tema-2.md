### EJERCICIO 1: Crear un espacio de nombres y montar en él una imagen ISO de un CD de forma que no se pueda leer más que desde él. 
![ejercicio1](https://dl.dropbox.com/s/hd225cfgfwz8iyp/ejercicio1IV2.png)

Primero creamos el espacio de nombres y posteriormente montamos la imagen como se ve en la captura anterior.

### EJERCICIO 2: 
### - 2.1 Mostrar los puentes configurados en el sistema operativo
Como podemos ver en la siguiente captura, mi PC no dispone de ningún puente.

![ejercicio2](https://dl.dropbox.com/s/nj7ka6i41b1qkuw/ejercicio2IV2.png)

### - 2.2 Crear un interfaz virtual y asignarlo al interfaz de la tarjeta wifi, si se tiene, o del fijo, si no se tiene.
![Ejercicio2.2](https://dl.dropbox.com/s/y1r2blz6hwmaeei/ejercicio2.2IV2.png)

Como muestra el anterior volcado de pantalla, primero creamos el puente ya que no disponía de ninguno en mi PC, le asignamos eth0 (tarjeta fija) para finalmente mostrar las interfaces, incluida la que he creado.


### EJERCICIO 3:
### - 3.1 Usar debootstrap (o herramienta similar en otra distro) para crear un sistema mínimo que se pueda ejecutar más adelante.
En primer lugar instalamos debootstrap con sudo apt-get instal debootstrap.

Seguidamente lanzamos la siguiente orden en nuestra consola para instalar la versión quantal: sudo debootstrap --arch=amd64 quantal /home/jaulas/quantal/ http://archive.ubuntu.com/ubuntu
![ejercicio3](https://dl.dropbox.com/s/8yuz8ib9xc2tpfp/tema2.png)

Ahora con chroot cambiamos el root del sistema montado y vemos lo que contiene, o simplemente hacemos ls en el directorio.

![ejercicio3](https://dl.dropbox.com/s/je8xqdj71rutnes/tema2.1.png)


### - 3.2 Experimentar con la creación de un sistema Fedora dentro de Debian usando Rinse.
En primer lugar instalamos rinse con:
sudo apt-get install rinse
Seguidamente visualizamos las distintas distribuciones que tiene.
![ejercicio2](https://dl.dropbox.com/s/nj7ka6i41b1qkuw/ejercicio2V2.png)

Procedemos a instalar la de fedora 7 utilizando rinse con la siguiente linea de comandos:
sudo rinse --arch i386 --distribution fedora-core-7 --directory /home/jaulas/fedora
![ejercicio2](https://dl.dropbox.com/s/nj7ka6i41b1qkuw/ejercicio2I.png)

Finlmente tras la instalación, vemos el contenido haciendo ls.
![ejercicio2](https://dl.dropbox.com/s/nj7ka6i41b1qkuw/ejercicio2IV2.ng)


### EJERCICIO 4:
### Instalar alguna sistema debianita y configurarlo para su uso. Trabajando desde terminal, probar a ejecutar alguna aplicación o instalar las herramientas necesarias para compilar una y ejecutarla.
