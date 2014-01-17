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




### - Hacer un ejercicio equivalente usando otro hipervisor como Xen, VirtualBox o Parallels.




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



## EJERCICIO 6

### Usar juju para hacer el ejercicio anterior.



## EJERCICIO 7

### Instalar una máquina virtual Ubuntu 12.04 para el hipervisor que tengas instalado.



