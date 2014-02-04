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


## EJERCICIO 7
### Crear un script para provisionar `nginx` o cualquier otro servidor
web que pueda ser útil para alguna otra práctica

## EJERCICIO 8
### Configurar tu máquina virtual usando vagrant con el provisionador
ansible
