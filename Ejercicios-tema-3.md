## EJERCICIO 1
### Instala LXC en tu versión de Linux favorita. 

Inicialmente, para instalar LXC, cambiamos a modo root con:
  `sudo su`
  
Seguidamente introducimos la contraseña y ya en superusuario, damos paso a la instalación como se muestra en la siguiente captura introduciendo en línea de comandos:
  `apt-get install lxc`

![Ejercicio1](https://dl.dropbox.com/s/dddf9oqxi85if1f/tema3.1.png)


Ahora, con la línea `lxc-checkconfig` comprobamos que todo va correctamente y que podemos crear contenedores.

![Ejercicio1](https://dl.dropbox.com/s/7cwjglzu9ahwg17/tema3.2.png)




## EJERCICIO 2
### Comprobar qué interfaces puente ha creado y explicarlos.

Como muestra la siguiente captura de pantalla, con 'brctl show' nos muestra que se ha creado el puente.

![Ejercicio2](https://dl.dropbox.com/s/ea5cfea8ebb2nl1/ejercicio2.png)


## EJERCICIO 3
 
###- Crear y ejecutar un contenedor basado en Debian.
 
Inicialmente me creo mi contenedor de ubuntu introduciendo en consola lo siguiente:
  `lxc-create -t ubuntu-cloud -n contenedor`   
Seguidamente, tras ejecutar `lxc-start -n contenedor` entramos en nuestro sistema.
Nuestro usuario y password van a ser "ubuntu".
 
###- Crear y ejecutar un contenedor basado en otra distribución, tal como Fedora. Nota En general, clxc-create -t ubuntu-cloud -n contenedorbasado en tu distribución y otro basado en otra que no sea la tuya.

Instalamos curl y yum ya que nos dara un error al crear fedora si no los tenemos instalados.
A continuación, realizamos de igual forma que en el apartado anterior incluyendo `sudo lxc-create -t fedora -n fedora14 -- -R 14` 


## EJERCICIO 4


###-Instalar lxc-webpanel y usarlo para arrancar, parar y visualizar las máquinas virtuales que se tengan instaladas.

Instalamos lxc-webpanel introduciendo en consola la siguiente línea de comandos:
`wget http://lxc-webpanel.github.io/tools/install.sh -O | sudo bash`
seguidamente, comienza el proceso de instalación el cual tarda unos minutos.

Una vez instalado, abrimos una pestaña en nuestro navegador e introducimos `localhost:5000` para poder usarlo.

![Ejercicio4.a](https://dl.dropbox.com/s/kwguek1j11bqtfh/ejercicio4.png)

###-Desde el panel restringir los recursos que pueden usar: CPU shares, CPUs que se pueden usar (en sistemas multinúcleo) o cantidad de memoria.

En primer lugar, para restringir los recursos de cpus pulsamos en el panel de la izquierda sobre el contenedor que elijamos y se nos mostrará un menu como el que se muestra en la siguiente captura.

![Ejercicio4.b](https://dl.dropbox.com/s/nhhrrn6uuqsuw8c/ejercicio4b.png)

## EJERCICIO 5

### Comparar las prestaciones de un servidor web en una jaula y el mismo servidor en un contenedor. Usar nginx.

Para realizar la comparación de las prestaciones, usamos la jaula que creamos en el tema 2 y el contenedor de ubuntu  que hemos creado anteriormente.

Ahora entramos en el contenedor e instalamos nginx. Después con AB hacemos las peticiones concurrentes con la siguiente línea en consola:
  `ab -n 1000 -c 1000 [ip]`

Hecho esto en el contenedor, procedemos a entrar en  la jaula  donde lanzamos nginx, realizando las peticiones con `ab -n 1000 -c 1000 http://localhost/`


## EJERCICIO 6

### Instalar juju y, usándolo, instalar MediaWiki en un táper.

1. INSTALAMOS JUJU
AÑADIR REPOSITORIO PARA PODER REALIZAR SU INSTALACION:

`sudo add-apt-repository ppa:juju/stable`

`sudo apt-get update`

A CONTINUACIÓN INSTALAMOS EL JUJU:
`sudo apt-get install juju-core`

2. LO USAMOS PARA INSTALAR MYSQL
INICIALIZAMOS JUJU
`sudo juju init` 

POSTERIORMENTE ENTRAMOS EN EL FICHERO ~/.juju/environments.yaml Y CAMBIAMOS LA LÍNEA  default:amazon POR default:local
Y ahora hacemos:
> ```
>`juju switch local`
>`juju bootstrap`
>`juju deploy mysql`
>`juju status`
> ```

## EJERCICIO 7

### Destruir toda la configuración creada anteriormente
    
    Para destruirla solo tenemos que realizar lo que muestra la siguiente captura:
    
![Ejercicio7](https://dl.dropbox.com/s/im6khfvo9g18210/ejercicio7.png)
    
    
### Volver a crear la máquina anterior y añadirle mediawiki y una relación entre ellos.
    Sería de la siguiente forma, introduciendo en la consola las siguientes líneas de comandos:
    
    juju bootstrap
    juju deploy mediawiki
    juju deploy mysql
    juju add-relation mediawiki:db mysql
    juju expose mediawiki


### Crear un script en shell para reproducir la configuración usada en las máquinas que hagan falta.

En este ejercicio, reuno todo lo relizado en los ejercicios anteriores en un script para que cuando lo ejecutemos muestre lo mismo. Posteriormente tras guardarlo con la extensión ".sh" cambiamos los permisos con "chmod +x ejercicio.sh" y lo lanzamos como super usuario así "sudo ./ejercicio.sh"
 

    #!/bin/bash
    juju init
    juju switch local 
    juju bootstrap 
    juju deploy mediawiki
    juju deploy mysql 
    juju add-relation mediawiki:db mysql 
    juju expose mediawiki 
    juju status 


## EJERCICIO 8

### Instalar libvirt. Te puede ayudar esta guía para Ubuntu.

Lo instalamos libvirt como muestra la siguiente captura:

![Ejercicio8](https://dl.dropbox.com/s/zbysw2v94dbk5x6/ejercicio8.1.png)


## EJERCICIO 9

### Instalar un contenedor usando virt-install.

Inicialmente, instalamos virt-install como muestra la siguiente captura:

![Ejercicio9](https://dl.dropbox.com/s/x4sv1zbqdpuhh74/ejercicio8.png)

Seguidamente descargamos la imagen de ubuntu server como sigue e instalamos el contenedor:

![Ejercicio9](https://dl.dropbox.com/s/izygc14tllpk8tf/ejercicio9.1.png)

Finalmente, instalamos virt-viewer y continuamos con la instalación.

![Ejercicio9](https://dl.dropbox.com/s/qf3aqickofms1mr/ejercicio9.2.png)



## EJERCICIO 10
### Instalar docker.
Inicialmente hacemos un update y seguidamente hacemos en consola:

sudo apt-get install linux-image-extra-`uname -r' 

Seguidamente introducimos en consola la siguiente orden que muestra la captura:

![Tema5](http://ubuntuone.com/2LRnjEx1bkbxRrpkAqYtI7)

Luego hacemos: 

`sudo sh -c "echo deb http://get.docker.io/ubuntu docker main\ /etc/apt/sources.list.d/docker.list"`

![Tema5](http://ubuntuone.com/1XBiZOu76plXhyzNCYPQRF)

Continuamos en consola haciendo `sudo apt-get install lxc-docker` sin olvidarnos de hacer antes un update:

![Tema5](http://ubuntuone.com/5g4ck6MXepDKCOjaH0G5vs)


Finalmente ya solo tenemos que introducir `sudo docker -d &` y queda instalado docker.

## EJERCICIO 11
### Instalar a partir de docker una imagen alternativa de Ubuntu y alguna adicional, por ejemplo de CentOS.

### Buscar e instalar una imagen que incluya MongoDB.





## EJERCICIO 12
### Crear un usuario propio e instalar nginx en el contenedor creado de esta forma




## EJERCICIO 13
### Crear a partir del contenedor anterior una imagen persistente con commit.



## EJERCICIO 14
### Crear una imagen con las herramientas necesarias para DAI sobre un sistema operativo de tu elección.



