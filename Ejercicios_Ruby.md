## EJERCICIO 1

### Instalar Ruby y usar ruby --version para comprobar la versión instalada. A la vez, conviene instalar también irb, rubygems y rdoc.

Instalamos con apt-get install:

![Ejercicio1](https://dl.dropbox.com/s/nzgq9h754yp6yyn/ruby1.png)


Seguidamente, comprobamos que esta instalado con `ruby --version` el cual nos muestra lo siguiente:


![Ejercicio1](https://dl.dropbox.com/s/kypt0n4j2xspoza/ruby2.png)


También instalamos `irb`, `rubygems` y `rdoc`.


![Ejercicio1](https://dl.dropbox.com/s/h3dw7gqggcua4qq/ruby3.png)



---


## EJERCICIO 2

### Crear un programa en Ruby que imprima los números desde el 1 hasta otro contenido en una variable.

Primero, comprobamos donde está el interprete y prodecemos a crear nuestro programa. Una vez vayamos a ejecutarlo, no tenemos que olvidar de darle permiso de ejecución con `chmod +x ejercicio2.rb`.

![Ejercicio2](https://dl.dropbox.com/s/cdzrixjxbhx189w/ruby4.png)

      PROGRAMA:
      #!/usr/bin/ruby
      #Author: STiago
        for var in 1..20
          puts "Numero = #{var}"
        end
        

`SALIDAS:`

![Ejercicio2](https://dl.dropbox.com/s/g0slzlfxhupfqxr/ruby5.png)


---


## EJERCICIO 3

### ¿Se pueden crear estructuras de datos mixtas en Ruby? Crear un array de hashes de arrays e imprimirlo.

            CÓDIGO:
            #!/usr/bin/ruby
            #Author: STiago
            
            ejercicio = {:semana => ["lunes"=>' IV, ', "martes"=>' DAI, ', "miercoles"=>' TE ', "jueves"=>' DDSI, ', "viernes"=>' FR '],:trabajos=> ["IV"=>' ubuntu, ', "DAI"=>' ubuntu, ', "FR"=>' windows ']}
            
            puts ejercicio.inspect
            
            ejercicio.keys().each do |var|
                  puts ejercicio[var]
            end

Por lo tanto si se pueden crear estructuras de datos mixtas en Ruby siendo el resultado el siguiente:


![Ejercicio3](https://dl.dropbox.com/s/5pkk6w7629455yn/ruby6.png)


---


## EJERCICIO 4

### Crear una serie de funciones instanciadas con un URL que devuelvan algún tipo de información sobre el mismo: fecha de última modificación, por ejemplo. Pista: esa información está en la cabecera HTTP que devuelve

            CÓDIGO
            #!/usr/bin/ruby
            def fecha(url)
                  respuesta = Net::HTTP.get_reponse url,'/'
                  return respuesta['date'].to_s
            end
            
            def servidor(url)
                  respuesta = Net::HTTP.get_reponse url,'/'
                  return respuesta['server'].to_s
            end
            
            url = ARGV[0]
            
            puts "La URL introducida es: " << url
            puts "La fecha de la peticion es: " << fecha()
            puts "Servidor: " << servidor()
            
            puts fecha(url)
            puts servidor(url)

Dando como resultado:

![Ejercicio4](https://dl.dropbox.com/s/sfi5dykme2xil2g/ruby7.png)

---

## EJERCICIO 5

### Ver si está disponible Vagrant como una gema de Ruby e instalarla.

Como he comprobado con `gem search --remote vagrant`, no está instalada la gema, por lo que procedo a instalarla con la siguiente línea de comandos en consola:

`sudo gem install vagrant`

![Ejercicio5](https://dl.dropbox.com/s/v7h57vlx7ha8nea/ruby8.png)







