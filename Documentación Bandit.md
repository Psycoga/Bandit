## Level 0
Conectarse por ssh a la máquina, con el nombre de usuario bandit0, la contraseña es igual. 
El comando se vería así: 
- `ssh bandit0@bandit.labs.overthewire.org -p 2220`
Pide la contraseña después de este comando, una vez se pone ya estaríamos dentro de la máquina.
## Level 0 ---> Level 1

Para este nivel, nos logeamos con el siguiente comando: 
`ssh bandit1@bandit.labs.oberthewire.org -p 2220`
La contraseña  es:  `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

## Level 1 ---> Level 2

Una vez estemos dentro de la maquina hacemos lo siguiente:

Miramos con ls, y vemos que el archivo es "-".
Como linux **no lo reconoce** como un archivo tal cual, **poniendo la ruta**
absoluta, si se puede ver el contenido, es el siguiente: 

CONTRASEÑA: `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`

Con esta contraseña nos logeamos en la siguiente maquina. 

## Level 2 ---> Level 3

Para este nivel dos, tenemos un archivo que se llama "spaces in this filename", para verlo, **ponemos el nombre del archivo entre comillas**, así: 
`cat "spaces in this filename"`

CONTRASEÑA: `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`

## Level 3 ---> Level 4

El archivo donde se guarda la contraseña está oculto, para ello ponemos el siguiente comando: 
`cat ...Hiding-From-You`

Ya podemos ver la contraseña.

CONTRASEÑA: `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`

## Level 4 ---> Level 5

Para este nivel vamos a coger la ayuda del comando **file**, seguido de la ruta completa del archivo, porque como hemos visto anteriormente, **los archivos que empiezen por "-", no los interpreta como un archivo normal**, por lo cual, si ponemos el siguiente comando: 
`find ./*`

Veremos que el resultado es el siguiente: 
```
bandit4@bandit:~/inhere$ file ./*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```

Nos muestra de forma clara, cual es el **archivo legible para el humano**.
En el se encuentra la contraseña, para verlo utilizamos el siguiente comando: 
`cat ./-file07

CONTRASEÑA: `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`

## Level 5 ---> Level 6

Para este nivel, hay que buscar algo **MUY CONCRETO**, por lo cual vamos a usar el comando **find**, de forma que **filtremos de la forma que queremos**; 
- **find** busca todo tipo de cosas, le añadimos un **"."**  para que busque en esa misma carpeta.
- Filtramos **el tipo de archivo**, en este caso es tipo **file**. en el comando esta parte se pone así: `-type f` 
- Y por último el tamaño del archivo, en nuestro caso es 1033 bytes, el comando sería: `-size 1033c`, en este caso es **"c"** , ya que buscamos **"bytes"** o **"caracteres"** . 

El comando completo quedaría tal que así: 
`find . -type f -size 1033c`

Nos muestra que el archivo se encuentra en;
`./maybehere07/.file2`

Si le hacemos un **"cat"** con la ruta completa tendríamos la contraseña.
`cat ./maybehere07/.file2

CONTRASEÑA: `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`


## Level 6 ---> Level 7

Lo primero que nos especifica en el ejercicio, es el **usuario** y el **grupo** en el que tenemos que buscar.

![[Screenshot from 2024-10-02 18-56-24.png]]
Nos pone que el archivo es **dueño del** usuario **bandit7** y el **grupo bandit6** y que el **tamaño del archivo** es de **33 bytes**, por lo cual, aplicando todo esto en un comando sería el siguiente:
`find / -user bandit7 -group bandit6 -size 33c 2>/dev/null`

Paso a paso sería: 
- **find /** para buscar desde la raíz de nuestro sistema.
- **-user bandit7** para especificar el usuario al que queremos que pertenezca ese archivo.
- **-group bandit6** para que busque el grupo al que pertenece.
- **-size 33c** para especificar el tamaño del archivo.
**IMPORTANTE** , esta parte del código es para filtrar TODOS los codigos de error que da, para encontrar el justo que necesitamos: 
- **2>/dev/null**
- 
- **`2>`**: Indica que estás redirigiendo la salida de error estándar.
- **`/dev/null`**: Es el dispositivo donde se descarta cualquier cosa que se envíe allí.
- **Uso**: Mantiene la salida limpia y evita que aparezcan mensajes de error innecesarios.
CONTENIDO DEL ARCHIVO: 

CONTRASEÑA: `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`




## Level 7 ---> Level 8

En este ejercicio nos dice que la contraseña, se encuentra en el archivo **data.txt**, en el cual hay mas contraseñas, en este caso nos dice que esta al lado de una palabra, **"millionth"** , ejecutamos el comando : 
`grep "millionth" data.txt

Nos saldrá lo siguiente: 

`bandit7@bandit:~$ grep "millionth" data.txt 
`millionth	dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc

CONTRASEÑA: `dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc`

## Level 8 ---> Level 9

Para este ejercicio se utiliza una linea de comandos un poco mas dificil de entender, **nos dice que la contraseña se encuentra en un archivo data.txt, y que dentro del montón de ellas, la correcta es la que solo se repite una vez**
Para ello utilizamos el comando `uniq`, pero este no va a funcionar si lo ponemos tal cual no va funcionar, nos va a sacar todos las contraseñas igual. Para ello lo tendremos que ordenarlo con el comando `sort`, una lo pongamos con este comando ya funcionara. 

CONTRASEÑA: `4CKMh1JI91bUIZZPXDqGanal4xvAg0JM

## Level 9 ---> Level 10

Dentro de un data.txt que esta lleno de contenido no leible para el ser humano, esta la contraseña que necesitamos. Vamos a utilizar el comando `strings` para que nos filtre el contenido que nosotros podemos leer, y luego utilizamos un **grep para filtrar por iguales, ya que en el ejercicio nos pone que va seguido de los mismos**, el comando seria el siguiente: 
`strings data.txt | grep "==="`

CONTRASEÑA: `FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

## Level 10 ---> Level 11

Archivo data.txt, encodeado en base64, ponemos el comando: 
`base64 -d data.txt`

Nos muestra lo siguiente: 
`The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr`

CONTRASEÑA: `dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr`

## Level 11 ---> Level 12

Para el siguiente nivel nos ponen que la contraseña esta encondeada en **ROT13**. Podemos utilizar dos herramientas, la consola de comando, con el siguiente comando `cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'`, o de la forma sencilla,
ya que sabemos la forma de encondearlo porque nos lo pone en la descripción del ejercicio, podemos utiliazar **cyberchef**, con la herramienta de **ROT13**, añadiendo tanto las **mayúsculas como las minúsculas**, si copiamos el
contenido del archivo: `Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4`, nos lo traduce a lo siguiente: `The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`. **Las dos formas de hacerlo dan el mismo resultado**.
- CONTRASEÑA:`7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4`

## Level 12 ---> Level 13

Este nivel consta de:
- 1: Pasarlo de hexdump, a binario.
- Descpmprimirlo **REPEDITAMENTE**, muy repetidamente, hasta llegar a data8.tar, donde esta el archivo el cual necesitamos, su contenido es:


Un script para hacerlo mucho mas cómodo sería el siguiente: 
```
import os
import subprocess

def main():
    # Step 1: Convertir el hexdump a binario
    subprocess.run(['xxd', '-r', 'data.txt', 'newdata.txt'])
    print("Convertido el hexdump a nuevo archivo: newdata.txt")

    # Step 2: Renombrar y descomprimir el archivo gzip
    os.rename('newdata.txt', 'newdata.tar.gz')
    subprocess.run(['gunzip', 'newdata.tar.gz'])
    print("Descomprimido: newdata.tar.gz a newdata.tar")

    # Step 3: Renombrar y descomprimir el archivo bzip2
    os.rename('newdata.tar', 'newdata.bz2')
    subprocess.run(['bunzip2', 'newdata.bz2'])
    print("Descomprimido: newdata.bz2 a newdata")

    # Step 4: Renombrar y descomprimir el archivo gzip nuevamente
    os.rename('newdata', 'newdata.tar.gz')
    subprocess.run(['gunzip', 'newdata.tar.gz'])
    print("Descomprimido: newdata.tar.gz a newdata.tar")

    # Step 5: Descomprimir el archivo tar
    subprocess.run(['tar', '-xf', 'newdata.tar'])
    print("Descomprimido: newdata.tar a data5.bin")

    # Step 6: Descomprimir data5.bin
    subprocess.run(['tar', '-xf', 'data5.bin'])
    print("Descomprimido: data5.bin a data6.bin")

    # Step 7: Renombrar y descomprimir el archivo bzip2
    os.rename('data6.bin', 'data6.bz2')
    subprocess.run(['bunzip2', 'data6.bz2'])
    print("Descomprimido: data6.bz2 a data6")

    # Step 8: Descomprimir data6
    subprocess.run(['tar', '-xf', 'data6'])
    print("Descomprimido: data6 a data8.bin")

    # Step 9: Renombrar y descomprimir el archivo gzip
    os.rename('data8.bin', 'data8.tar.gz')
    subprocess.run(['gunzip', 'data8.tar.gz'])
    print("Descomprimido: data8.tar.gz a data8.tar")

    # Step 10: Mostrar el contenido de data8.tar que debería contener la contraseña
    with open('data8.tar', 'r') as f:
        content = f.read()
        print("Contenido de data8.tar (la contraseña del siguiente nivel):")
        print(content)

if __name__ == "__main__":
    main()
```
CONTRASEÑA: `The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn` 

## Level 13 --> Level 14

En este ejercicio no nos va a dar una contraseña como tal, sino que tenemos que meternos por ssh, para ello en la maquina de bandit13 nos da una clave privada, ¿cómo la vamos a utilizar?
Vamos a utilizar el siguiente comando: 

`ssh -i sshkey.private -p 2220 bandit14@localhost`

El -i es para poder utilizar la clave privada al conectarnos en la máquina de bandit14, en este caso el archivo de la clave privada se llama **sshkey.private**, el resto es el puerto, **-2220** , que es el de bandit, y nos conectamos en la misma maquina con **localhost**.

## Level 14 --> Level 15

En este nivel vamos a necesitar dos cosas, lo primero de todo mirar la contraseña del nivel actual, la cual esta en `/etc/bandit_pass/bandit14`,. Vamos a utilizar nc (netcat), lo cuál nos sirve para que nos de información en ese puerto con la contraseña correcta. 
El comando sería el siguiente: 
`nc localhost 30000`, si ponemos bien la contraseña de este nivel, nos da la del siguiente.

CONTRASEÑA: `8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo`

## Level 15 --> Level 16

Para este nivel vamos a tener que saber algo de SSL/TLS. Para conectarse con este protocolo vamos a utilizar el comando openssl.
### ¿Qué hace el comando `openssl`

Indica que vamos a utilizar este método para comunicarnos, en este caso, con el localhost en el puerto 30001. Vamos a acompañar el comando de los siguientes argumentos: 
`openssl s_client -connect localhost:30001`

- s_client, nos especifica que vamos a usar la función de cliente de SSL/TLS
- -connect localhost:30001, vamos a conectarnos en el localhost, especificamente en el puerto 30001, el que nos indica el ejercicio, y para recibir la información que necesitemos vamos a tener que poner la contraseña del nivel actual,`8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo`. 
La contraseña que nos da es la siguiente: 
CONTRASEÑA: `kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx`

## Level 16 --> Level 17 

En este nivel vamos a hacer exactamente lo mismo que el anterior. Primero tenemos que encontrar el puerto que esta abierto, que utilize SSL/TLS, para ello vamos a analizar los puertos con el comando: `nmap -p 31000-32000 localhost`, entre otros muchos que se pueden usar. Nos lo reduce a 4, si vamos probando entre ellos, al final el que no nos repite lo que ponemos, y nos da algo diferente es el 51790. Nos muestra en pantalla KEYUPDATE, luego nos cierra sesion, si ponemos la contraseña correcta. 
Vamos a añadirle a nuestro comando anterior el siguiente argumento: 
`openssl s_client -connect localhost:31790 -ign_eof`, 
- `-ign_eog`, este argumento hace que la sesion no se cierre despues del keyupdate.
Lo siguiente que nos da es una clave privada, la guardamos y le damos chmod 600. Entramos por ssh al siguiente nivel utilizando la misma. 
**Clave para entrar al 17, `ssh -i private_key.pem bandit17@localhost`**, si la hemos **guardado**, y le damos los **permisos adecuados**, ya estaríamos dentro de la nueva máquina.

## Level 17 --> Level 18






`




