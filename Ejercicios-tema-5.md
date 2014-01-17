## EJERCICIO 1
###Instalar los paquetes necesarios para usar KVM. Se pueden seguir estas instrucciones. Ya lo hicimos en el primer tema, pero volver a comprobar si nuestro sistema está preparado para ejecutarlo o hay que conformarse con la paravirtualización.

En primer lugar, probamos si soporta virtualización introduciendo en consola la siguiente línea de comandos:

    egrep -c '(vmx|svm)' /proc/cpuinfo
    
  Y nos muestra lo siguiente:
  
  
  ![Tema5](http://ubuntuone.com/2LNcQHUFLSsMgGu1XqmdOg)
  
  
 Una vez realizado lo anterior, procecemos a instalar los paqetes necesarios para el uso de KVM.

    sudo apt-get install qemu-kvm qemu-system libvirt-bin virtinst virt-manager
    
  ![Tema5](http://ubuntuone.com/6tLLCoDHeLbMABIa7dglMe)



## EJERCICIO 2

### - Crear varias máquinas virtuales con algún sistema operativo libre, Linux o BSD. Si se quieren distribuciones que ocupen poco espacio con el objetivo principalmente de hacer pruebas se puede usar CoreOS (que sirve como soporte para Docker) GALPon Minino, hecha en Galicia para el mundo, Damn Small Linux, SliTaz (que cabe en 35 megas) y ttylinux (basado en línea de órdenes solo).

En primer lugar activamos el módulo del kernel kvm con:

        `sudo modprobe kvm-intel`
        
 Seguidamente, accediendo a las paginas y creamos nuestro disco duro virtual:
 
        `http://www.slitaz.org/en/get/#stable`
        
        `qemu-img create -f raw SliTar-hdd.img 100M`
        
y nos queda: 
        
  ![Tema5](http://ubuntuone.com/7eewNzlYyBjtrYvAI4FxXk)
        
Seguidamente hacemos `qemu-system-x86_64 -hda ./SliTar-hdd.img -cdrom ../Descargas/slitaz-4.0.iso` y hemos terminado.

Ahora procedemos a instalar ttyLinux:

`qemu-img create -f qcow2 ttylinux-hdd.img 500G`
`qemu-system-x86_64 -hda ./ttylinux-hdd.img -cdrom ttylinux-pc_x86_64-16.1.iso`


![Tema5](http://ubuntuone.com/4TlFpsgFsdxdNQKRa3YZAW)



En primer lugar primero creamos nuestro disco virtual para CentOS:

![Tema5](http://ubuntuone.com/47LUNp5fQwRaXhfDovMIDp)


Configuramos ahora VMM como muestran los siguientes volcados de pantalla:

![Tema5](http://ubuntuone.com/2tcbpA4phXYUzPqKXqrcNc)


![Tema5](http://ubuntuone.com/05wdf5uzKMVMEt6DCjdn0g)

![Tema5](http://ubuntuone.com/1LlqGU1XoMFNW79iQdWg9r)


Y ya tenemos instalado bien CentOS:


![Tema5](http://ubuntuone.com/6KAZE50woqePwfXn24K66v)


### - Hacer un ejercicio equivalente usando otro hipervisor como Xen, VirtualBox o Parallels.

Tras instalar virtualBox con `sudo apt-get install virtualbox` , procedemos a crearlo:

![Tema5](http://ubuntuone.com/2FBTdhQINnR7E2jiaYlRND)

![Tema5](http://ubuntuone.com/5FTRvJctE8NLVmdbvEPQB1)

![Tema5](http://ubuntuone.com/52wGZtevlN9wjaXV3m8441)


Y ya vemos ubuntu server funcionando correctamente:

![Tema5](http://ubuntuone.com/0GWsYFZp5Z9YicFwgTD8cu)


## EJERCICIO 3

### Crear un benchmark de velocidad de entrada salida y comprobar la diferencia entre usar paravirtualización y arrancar la máquina virtual simplemente con qemu-system-x86_64 -hda /media/Backup/Isos/discovirtual.img





## EJERCICIO 4

### Crear una máquina virtual Linux con 512 megas de RAM y entorno gráfico LXDE a la que se pueda acceder mediante VNC y ssh.

Inicialmente, nos desargamos Lubuntu puesto que esta distribución ya tiene el entorno gráfico LXDE e introducimos en consola lo que muestra la siguiente captura de pantalla:


`qemu-img create -f qcow2 Lubuntu-hdd.img 8G`
`qemu-system-x86_64 -hda ~/qemu/lubuntu-hdd.img -cdrom ~/qemu/lubuntu-13.10-desktop-i386.iso -m 512M`

![Tema5](http://ubuntuone.com/2ryZvqfCS4F9RE4Ckdlybo)


Intaslamos a continuación Lubuntu con los siguientes pasos:


![Tema5](http://ubuntuone.com/79LMW0OE5PpPllCzieADWt)

y finalmente queda instalado como muestra a continuación el siguiente volcado de pantalla:


![Tema5](http://ubuntuone.com/2cAp8vVBTUrzPUPuQ4dBJw)

Y ahora con ssh hacemos:

`qemu-system-x86_64 -boot order=c -drive file=Lubuntu-hdd.img,if=virtio -m 512M -name lubuntu -redir tcp:2222::22`

Y conectamos por ssh al localhos por el puerto 2222:

`ssh -p 2222 lubuntu@localhost`


![Tema5](http://ubuntuone.com/58ka286k1EVWMlD5o9qAWE)



## EJERCICIO 5

### Crear una máquina virtual ubuntu e instalar en ella un servidor nginx para poder acceder mediante web.

Para ello voy a usar vmware, instalando como hemos hecho anteriormente con ubuntu server en virtual box, dandole 1 procesador y 1024 MB de RAM.

A continuación, procedo a describir el proceso de instalación de nginx en ubuntu server:

PASOS:
        
1. Importamos  la clave del repositorio:
            
                cd /tmp/
                wget http://nginx.org/keys/nginx_signing.key
                apt-key add /tmp/nginx_signing.key
                rm -f /tmp/nginx_signing.key
                
                
 ![Tema5](https://dl.dropbox.com/s/rtrxp46jkz6o2m4/pra2.png)
                
                
2. Añadimos el repositorio editando /etc/apt/sources.list :
                
                echo "deb http://nginx.org/packages/ubuntu/ lucid nginx" >> /etc/apt/sources.list
                echo "deb-src http://nginx.org/packages/ubuntu/ lucid nginx" >> /etc/apt/sources.list
            
3. Procecemos a hacer el update y a instalar nginx con :
                
                sudo apt-get install nginx
                
4. Ahora editamos el fichero de configuración que se encuentra en /etc/nginx.confd/default.conf añadiendo:
            
                upstream apaches {
                    server 192.168.246.128
                    server 192.168.246.130
                }
                
                server{
                    listen 80;
                    server_name miservidor;
                    access_log /var/log/nginx/miservidor.access.log;
                    error_log /var/log/nginx/miservidor.error.log;
                    root /var/www/;
                
                    location /{ 
                        proxy_pass http://apaches;
                        proxy_set_header Host $host;
                        proxy_set_header X-Real-IP $remote_addr;
                        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                        proxy_http_version 1.1;
                        proxy_set_header Connection "";
                    }
                }
               
                
                
![Tema5](https://dl.dropbox.com/s/uh6l32s1ft6kf2h/pra8%28service%20restart%20nginx%29.png)
                
                
                
5. Lanzamos el servicio nginx:
                
                service nginx restart
                
6. Finalmente abrimos nuestro navegador seguido de la ip de nuestra máquina y nos saldra la pagina con el index de nginx.




## EJERCICIO 6

### Usar juju para hacer el ejercicio anterior.



## EJERCICIO 7

### Instalar una máquina virtual Ubuntu 12.04 para el hipervisor que tengas instalado.

Para realizar el ejercicio, debemos instalar los paquetes que siguen a continuación:

`sudo apt-get install ubuntu-vm-builder kvm virt-manager`

![Tema5](http://ubuntuone.com/1B6clESAuXlCrgxWjDo6aP)


A continuación, provisionamos nuestra máquina virtual introduciendo en la consola los siguiente:

![Tema5](http://ubuntuone.com/2f5ufR9UQI8RCexsL8OAYI)


![Tema5]()









