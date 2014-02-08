## EJERCICIO 1
### Instalar chef en la máquina virtual que vayamos a usar.
En primer lugar nos aseguramos de que nuestra máquina virtual, en mi caso ubuntu server, tiene instalado ruby. Para ello hacemos lo siguiente si no está instalado:

![Tema6](http://ubuntuone.com/03kj6twlbMFEx93l6hZBoh)


Y una vez comprobado que esta insalado, procedemos a instalar chef con `gem install ohai chef`:

![Tema6](http://ubuntuone.com/0LgmXYqd3KeqlYXXyKKBxx)

o simplemente ejecutamos en nuestra máquina la siguiente línea:

`curl -L https://www.opscode.com/chef/install.sh | bash`

## EJERCICIO 2
### Crear una receta para instalar nginx, tu editor favorito y algún directorio y fichero que uses de forma habitual.

En primer lugar, creamos nuestra estructura de carpetas como solemos hacer (con el comando mkdir seguido del nombre que le vayamos a dar a los directorios), después dentro ya de nuestro directorio, procedemos a crearnos el archivo "miReceta.rb" el cual contendrá nuestra receta, contenido que se corresponde con la siguiente captura de pantalla:

![Tema6](http://ubuntuone.com/75fpt3NPBBW6AyEMFQBLac)

El siguiente paso es crear en el nivel de chef el archibo en json y el archivo solo.rb (el primero refiere nuestra receta y el segundo indica donde está la receta y el archivo json, y además se encarga de ejecutar la receta)

![Tema6](http://ubuntuone.com/5H0GEw7mp872tWM3fG6b7r)

![Tema6](http://ubuntuone.com/6YTTZPyAUhLd5UDGG3Zc3g)

Seguidamente lanzamos la orden `sudo chef-solo -c chef/solo.rb` la cual nos mostrará lo siguiente si se han realizado correctamente todos los pasos anteriores.

![Tema6](http://ubuntuone.com/7EhyqPlWblkO2Ie40dYklZ)

Ya estaría todo terminado, solo nos queda probar que la receta funciona y nos instala todo lo que hemos introducido en ella correctamente.

![Tema6](http://ubuntuone.com/7T3e9W3XrQ9Yl2MEwg4n9r)




## EJERCICIO 3
### Escribir en YAML la siguiente estructura de datos en JSON:
{ uno: &#39;dos&#39;,tres: [ 4, 5, &#39;Seis&#39;, { siete: 8, nueve: [Object] } ] }

En YAML sería de la siguiente forma:

> ```
> --- # 
>  tres:
>    - 4
>    - 5
>    - "Seis"
>    -
>      siete: 8
>      nueve:
>        - "Object"
>  uno: "dos"

> ---
> ```


## EJERCICIO 4
### Desplegar los fuentes de la aplicación de DAI o cualquier otra aplicación que se encuentre en un servidor git público en la máquina virtual Azure (o una máquina virtual local) usando ansible.

El primer paso que tenemos que realizar es instalarnos Ansible en nuestra máquina anfitriona, primero añadiendo el repositorio, luego haciendo un update y finalmente instalando con `sudo apt-get install ansible` como se muestra a continuación:

![Tema6](http://ubuntuone.com/1ADYpCoerrWUWIXBfLDO7O)


Tras instalar Ansible, nos creamos el fichero ansible_host en el cual debemos de introducir las máquinas que vamos a controlar, en mi caso sería:

`[azure]`
`victoriasantiago.cloudapp.net`

![Tema6](http://ubuntuone.com/3k61J2ofJemgBsOovQpS7y)

A continuación, cambiamos el valor de ANSIBLE_HOSTS y hacemos un ping a nuestra máquina de Azure comprobando que nos conecta mediante ansible.

![Tema6](http://ubuntuone.com/5ODQV45JN9xwfutpFDzQ2S)

A continuación instalamos git en la máquina de azure y tras su instalación, ya en nuestra máquina anfitriona, procedemos a hacer el despliegue de los fuentes de nuestra aplicación de DAI como se muestra en la siguiente captura:

![Tema6](http://ubuntuone.com/7Wef1yaLAyYHJ9yP4p802U)

Finalmente, para ver que se ha realizado todo correctamente, basta con hacer en la máquina un ls o tree que nos muestre que el despliegue se ha llevado a cabo bien.

![Tema6](http://ubuntuone.com/4Ch1wWfQXFdzs6fgrHBMlo)


## EJERCICIO 5
### Desplegar la aplicación de DAI con todos los módulos necesarios usando un playbook de Ansible.

En primer lugar, nos creamos el archivo playbook con extensión yml en el cual introducimos lo siguiente:

![Tema6](http://ubuntuone.com/4UaSuda6ZvE1pf8nrkhexu)

Seguidamente, en nuestra máquina anfitriona introducimos lo siguiente:

`export ANSIBLE_HOSTS=~/ansible_hosts`
`ansible-playbook playbook.yml --ask-pass -u victoria`

Quedando de la siguiente forma:

![Tema6](http://ubuntuone.com/14pxhjeWeBbmbrHWLWdhXm)


Y finalmente, abrimos nuestro navegador y podremos ver que nuestra aplicación se encuentra ejecutandose:

![Tema6](http://ubuntuone.com/0alDyvrQbLTdFcRmAWr7fS)


## EJERCICIO 6
Instalar una máquina virtual Debian usando Vagrant y conectar con ella.

Inicialmente, nos instalamos en nuestra máquina anfitriona vagrant usando:

`sudo apt-get install vagrant`

Tras instalarlo, procedemos a realizar los siguientes pasos:

`vagrant box add {title} {url}`
`vagrant init {title}`
`vagrant up`

y nos quedaria finalmente como se muestra en las siguientes volcados:

![Tema6](http://ubuntuone.com/1bFtNiLMltht4iXj2nMhjY)

Y conectar a la máquina con ssh :

`vagrant ssh`

![Tema6](http://ubuntuone.com/5T8AJ8E7A6mcuZNsEB4rw0)


## EJERCICIO 7
### Crear un script para provisionar `nginx` o cualquier otro servidor
web que pueda ser útil para alguna otra práctica

En primer lugar, editamos el fichero ***Vagrantfile** dejandolo como se muestra a continuación:

``` 
 # -*- mode: ruby -*-
 # vi: set ft=ruby :

 Vagrant.configure("2") do |config|
 config.vm.box = "victoria"
  config.vm.provider "virtualbox" do |v|
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
  end
  config.vm.provision "shell",
    inline: "sudo apt-get install -y nginx && sudo service nginx restart && sudo service nginx status"

 end
``` 

Tras realizas las modificaciones anteriores, ejecutamos en nuestra máquina `vagrant provision` y con ello se ejecutan los comandos que se van a aprovisionar.

![Tema6-ejercicio7](https://dl.dropbox.com/s/tecldglnf22x481/ejejerciio7.png)


## EJERCICIO 8
### Configurar tu máquina virtual usando vagrant con el provisionador

Comenzamos la configuración añadiendo en el fichero ansible_host la IP de nuestra máquina como se muestra a continuación:

```
[vagrant]
192.168.1.36
```
El siguiente paso es indicarle a Ansible que tiene que usar este fichero usando `export ANSIBLE_HOSTS=~/ansible_hosts` y posteriormente introduciendo la linea `config.vm.network :private_network, ip: "192.168.1.36" ` con una IP desde la que podamos acceder desde nuestro ordenador todo ello en el fichero Vagrantfile.

Por lo tanto el fichero Vagrant quedará como sigue:

![Tema6-ejercicio7](http://ubuntuone.com/2Wre8oX4Zpj2HOGECb2hLs)

Ahora, nos creamos el playbook para que Ansible que nos instale en la máquina Nginx. El fichero playbook quedaría con el siguiente contenido:

![Tema6-ejercicio7](http://ubuntuone.com/0xtBuucj4cN88DN0nSdsAs)


A continuación, procedemos a aprovisionar la máquina al igual que hemos hecho en el ejercicio anterior, lanzando por línea de comandos:

`vagrant provision`

![Tema6-ejercicio7](https://dl.dropbox.com/s/rtrqp4xlw9vsf1s/ejercicio8_tema6_3.png)

Y ya finalmente, solo queda acceder a nuestro navegador introduciendo la IP y veremos como nos muestra Nginx funcionando correctamente:

![Tema6-ejercicio7](https://dl.dropbox.com/s/m226nqn6hmnnvq4/pant.png)



