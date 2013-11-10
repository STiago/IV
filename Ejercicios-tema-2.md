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

Seguidamente lanzamos la siguiente orden en nuestra consola para instalar la versión quantal: sudo debootstrap --arch=amd64 saucy /home/jaulas/quantal/ http://archive.ubuntu.com/ubuntu

![ejercicio3](https://dl.dropbox.com/s/8yuz8ib9xc2tpfp/tema2.png)

Ahora con chroot cambiamos el root del sistema montado y vemos lo que contiene, o simplemente hacemos ls en el directorio.

![ejercicio3](https://dl.dropbox.com/s/je8xqdj71rutnes/tema2.1.png)


### - 3.2 Experimentar con la creación de un sistema Fedora dentro de Debian usando Rinse.
En primer lugar instalamos rinse con:
sudo apt-get install rinse
Seguidamente visualizamos las distintas distribuciones que tiene.

![ejercicio3](https://dl.dropbox.com/s/je2tniqkq9o5ud5/e.png)

Procedemos a instalar la de centos 6 utilizando rinse con la siguiente linea de comandos:
sudo rinse --arch i386 --distribution centos-6 --directory /home/jaulas/cuatro

Finlmente tras la instalación, vemos el contenido haciendo ls.

![ejercicio3](https://dl.dropbox.com/s/40iyd1jfar7i3v7/centos.png)


### EJERCICIO 4:
### Instalar alguna sistema debianita y configurarlo para su uso. Trabajando desde terminal, probar a ejecutar alguna aplicación o instalar las herramientas necesarias para compilar una y ejecutarla.
Inicialmente, aprovechando el sitema centos-6 instalado anteriormente, voy a realizar el trabajo sobre el.

A continuación, accedemos a la jaula de nuestro sistema operativo ejecutando "chroot /ruta de la jaula"
![ejercicio4](https://dl.dropbox.com/s/c90rrbdg5t3947k/ejj.png)

Ahora, muestro la instalación (instalamos nano)de una aplicación que calcula si un numero es par o es impar dentro del sistema enjaulado.
![ejercicio4](https://dl.dropbox.com/s/uudt48kmd7lpskx/nano.png)

Aplicación:
![ejercicio4](https://dl.dropbox.com/s/8bi6tnu0qz23fp7/parimpar.png)

Como hemos observado, funciona nano en el sistema, por lo tanto queda el objetivo de instalar la aplicacion y que funcione al ejecutarla.

### EJERCICIO 5:
### Instalar una jaula chroot para ejecutar el servidor web de altas prestaciones nginx.

Como en el ejercicio anterior, vamos a usar la máquina de centos que hemos instalado anteriormente para ejecutar nginx.
Pimero lo instalamos con el paquete "apt-get install wget" con el cual nos vamos a descargar desde internet nginx "wget http://nginx.org/download/nginx-1.4.0.tar.gz"
![ejercicio5](https://dl.dropbox.com/s/diz9fwr7rv7t0sx/nginx.png)

Ahora vamos a entrar en el directorio y lo configuramos instalando previamente lo siguiente:

    apt-get install gcc 
    apt-get install libpcre3 libpcre3-dev
    apt-get install zlib1g-dev
    apt-get install make
    ./configure

Seguidamente instalamos nginx con lo que sigue a continuación:

    make
    make install

Tras instalarlo, procedemos a hacerlo funcionar. CON curl desde consola hacemos que muestre el contenido de la página principal del servidor.
![ejercicio5](https://dl.dropbox.com/s/m4p0f8p4571sp7q/ngi.png)


### EJERCICIO 6:
###



