## EJERCICIO 1

### ¿Cómo tienes instalado tu disco duro? ¿Usas particiones? ¿Volúmenes lógicos?
Instalo GParted para ver que hay intalado y que particiones y volúmenes hay, teniendo como resultado lo siguiente:


![Ejercicio5](https://dl.dropbox.com/s/pf6ygzx1xvixg0o/ejercicio1.png)

---
    
#### Si tienes acceso en tu escuela o facultad a un ordenador común para las prácticas, ¿qué almacenamiento físico utiliza?

Los ordenadores de la facultad, usan un sistema de ficheros remoto.

---

## EJERCICIO 2

### Usar FUSE para acceder a recursos remotos como si fueran ficheros locales. Por ejemplo, sshfs para acceder a ficheros de una máquina virtual invitada o de la invitada al anfitrión.

Para realizar el ejercicio vamos a usar el contenedor de ubuntu que cree en el tema anterior, instalandolo con `sudo apt-get install sshfs`.
A continuación añadimos al grupo FUSE el usuario, lo haremos insertando en consola `usermod -a -G fuse Ubuntu`
Procedemos a crear un directorio con un archivo para probar todo  lo anterior, tanto en el contenedor como en el sistema anfitrion. Salvo que en el sistema anfitrion sera dond s montara el directorio remoto.
Le introducimos contenido usando `sshfs Ubuntu@10.0.3.246:/home/ubuntu/carpeta /home/Victoria/carpPrueba`.

Finalmente, vemos que si abrimos la carpeta va a estar el mismo archivo que el del contenedor.



---


## EJERCICIO 3

### Crear imágenes con estos formatos (y otros que se encuentren tales como VMDK) y manipularlas a base de montarlas o con cualquier otra utilidad que se encuentre

Partimos la realización del ejercicio desde una imagen con formato raw ya que lo admiten la mayoría de los sistemas operativo. Para ello usamos `fallocate -l 5M miimagen.img`
Seguidamente la visualizamos con `ls -lks miimagen.img` y `ls -lks miimagen1.img`.

Creamos otra imagen en formato qcow2, para ello hacemos `qemu-img create -f qcow2 fichero-cow.qcow2 5M`

Finalmente creamos otra imagen en formato vmdk usando QEMU y la creamos al igual que hemos hecho con las de qcow2. Luego montamos las imagenes usando `mount -o loop, offset=35456 miimagen-vmdk /mnt/mountpoint` y como dispositivo NBD sería como sigue a continuacion en los siguientes pasos:

        sudo modprobe nbd max_part=16
        sudo qemu-nbd -c /dev/nbd0 miimagen-vmdk.vmdk
        sudo partprobe /dev/nbd0/
        sudo mount /dev/nbd0 /mnt/miimagen

---


## EJERCICIO 4

### Crear uno o varios sistema de ficheros en bucle usando un formato que no sea habitual (xfs o btrfs) y comparar las prestaciones de entrada/salida entre sí y entre ellos y el sistema de ficheros en el que se encuentra, para comprobar el overhead que se añade mediante este sistema

Creamos las imágenes con quemu con `quemu-img create -f raw xfs.img 512M` y  `qemu-img create -f raw btrfs.img 512M`.
Seguidamente, las convertimos en sistema de ficheros en loop con `sudo losetup -v -f xfs.img` y  `sudo losetup -v -f btrfs.img`. Ahora le damos formato con `mkfs.xfs /dev/loop3` y `mkfs.btrfs /dev/loop4`.
Luego los montamos con `mount /dev/loop3 /mnt/loop3/` y `mount /dev/loop4 /mnt/loop4/`.
Comprobamos que estan montados en el sistema insertando en consola `df -h`. Y ya solo nos queda crear el archivo  para ver cuanto tarda en copiarse el archivo que tenemos en nuestro sistema en cada uno de los loop haciendo lo siguiente:

    `dd if=/dev/urandom of=archivo bs=100 count=150000`

Lo copiamos finalmente a los loop con `time cp archivo /mnt/loop3/archivo_xfs` y `time cp archivo /mnt/loop4/archivo_btrfs`


---


## EJERCICIO 5

### Instalar ceph en tu sistema operativo.

Para instalarlo basta con poner en consola lo siguiente:

![Ejercicio5](https://dl.dropbox.com/s/xgw57m27b5l2awn/ejercicio5.png)


---



## EJERCICIO 6

### Crear un dispositivo ceph usando BTRFS o XFS

En este ejrcicio solo nos quedaria configurar el dispositivo ya que lo hemos creado n el ejercicio de antes. Inicialmente, creamos un directorio para almacenar su información, para ello usamos `mkdir -p /srv/ceph/{osd,mon,mds}`.
Una vez realizado lo anterior, creamos y rellenamos el fichero de configuración. Seguidamente, creamos un sistema loop en xfs como hicimos en el ejercicio anterior y posteriormente, creamos el directorio del servidor de objetos usando `mkdir /srv/ceph/osd/osd.0` y el sistema de ficheros de objetos con `/sbin/mkcephtfs -a -c /etc/ceph/ceph.conf`.

Posteriormente, iniciamos el servicio y comprobamos el estado de ceph con :
    `sudo /etc/init.d/ceph -a start`
    `sudo ceph -s`
inalmente solo nos queda crear el directorio conde vamos a montarlo y lo montamos con :
    `mkdir /mnt/ceph`
    `mount -t ceph Ubuntu:/ /mnt/ceph`
    


## EJERCICIO 7

### Almacenar objetos y ver la forma de almacenar directorios completos usando ceph y rados.

En primer lugar creamos la piscina para rados con `rados mkpool piscina`. Introducimos nuestro fichro en la piscina que hemos creado (todo en modo superusuario) con `rados put -p piscina objeto ejemplo.img`.

Si quisiesemos subir una carpeta completa, bastaría con comprimir la misma y subirla comprimida, para ello realizamos los siguientes pasos:


    `tar -zcvf ejemplo.tar.gz InfVirt`
    `sudo rados put -p piscina carpeta ejemplo.tar.gz`
    `sudo rados df`
    `sudo rados ls -p piscina`


---


## EJERCICIO 8

### Tras crear la cuenta de Azure, instalar las herramientas de línea de órdenes (Command line interface, cli) del mismo y configurarlas con la cuenta Azure correspondiente

---



## EJERCICIO 9

### Crear varios contenedores en la cuenta usando la línea de órdenes para ficheros de diferente tipo y almacenar en ellos las imágenes en las que capturéis las pantallas donde se muestre lo que habéis hecho.

Vamos a empezar creando un contenedor para imágenes con `azure storage container create imagenes -p blob`
Seguidamente subimos una imagen cualquiera al contenedor usando:

`azure storage blob upload ~/Documentos/Imágenes/imagen.jpg`

Y con ello queda subido archivo a la cuenta que he hecho en el ejercicio de antes.



---



## EJERCICIO 10

### Desde un programa en Ruby o en algún otro lenguaje, listar los blobs que hay en un contenedor, crear un fichero con la lista de los mismos y subirla al propio contenedor. Muy meta todo.
Para poder realizarlo en Ruby con Azure, debemos de instalar en primer lugar la gema de ruby para azure usando:

    `sudo gem install azure`
    
    
Y finalmente, realizamos el siguiente código:



    #!/usr/bin/ruby
    require "azure"
    azure_blob_service = Azure::BlobService.new
    containers = azure_blob_service.list_containers()
    containers.each do |container|
        name = container.name + ".txt"
        
    File.open(name, "w") do |list|
        list.puts container.name + ":"
        list.puts "=" * container.name.length
    blobs = azure_blob_service.list_blobs(container.name)
        blobs.each do |blob|
                    list.puts "\t" + blob.name
        end
    end
    content = File.open(name, "rb") { |file| file.read }
    blob = azure_blob_service.create_block_blob(container.name, name, content)
    end
    
    
---










