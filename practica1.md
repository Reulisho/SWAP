# Práctica 1: Preparación de las herramientas.
## Introducción.
Para esta práctica hemos utilizado VirtualBox para llevar a cabo la virtualización de las dos máquinas con Ubuntu Server 18.
Lo primero que hay que hacer es descargar una imagen de Ubuntu Server. En mi caso, la he descargado desde la página oficial de Ubuntu:
http://www.ubuntu.com/download/server
Una vez descargada la imagen, habría que configurar las máquinas virtuales, para ello realizamos una instalación básica de VirtualBox, teniendo en cuenta que hay que añadir una red **NAT** y una **Host-Only** para cada máquina virtualizada. 
Esto hace que tengamos conexión tanto interna, como con la máquina anfitrión.
## Configuración de las máquinas.
Ahora voy a mostrar paso a paso, las tareas que he tenido que realizar, en cada máquina virtual, para dejarlo todo correctamente montado.

**1. Instalación de  Apache.**

Para ello he utilizado el comando que viene en el pdf:

> sudo apt-get install apache2 mysql-server mysql-client

**2. Configurar la red de internet.**

Para hacer esto he tenido que crear un fichero nuevo en **/etc/netplan**, con la estructura que aparece en la siguiente figura:

![Figura 1](https://i.ibb.co/9c5v09H/netplan.png)

Una vez configurado el fichero, ejecutamos el siguiente comando:
> Netplan apply
>  
Ahora mediante el comando:
> Ifconfig
> 
Podemos ver el estado actual de los dispositivos de red que tenemos conectados a la máquina.
En nuestro caso aparece **enp0s8** en ambas máquinas con las ips que le hemos configurado previamente (192.168.56.**102**/**103**)

![Figura 2](https://i.ibb.co/NN8P1t1/ips.png)

**3. Curl.**

Vamos a probar que mediante el comando *Curl* podemos acceder tanto a la página web de nuestra máquina, como a la página web de la otra máquina.
Para ello ejecutamos el siguiente comando (caso de M1 a M2):
> curl http:/192.168.56.102/ejemplo.html

En la siguiente imagen, muestro como accedo desde M1 a la página de M2 y viceversa.

![](https://i.ibb.co/M8jVzSv/ejemplo-curl.png=150x150)

Y ahora probamos a verlas desde el anfitrión.

![](https://i.ibb.co/0c49sKd/curl-anfitrion.png)

**4.  Ping.**

Ahora vamos a probar mediante el comando *Ping* a comprobar que la conexión funciona correctamente.
Para ello ejecutamos el siguiente comando:
> ping (dirección ip que queremos hacer ping)

Primero vemos el ping hecho desde las 2 máquinas virtuales:

![](https://i.ibb.co/tDx4yXM/ping-maquinas.png)

Y ahora vemos el ping hecho desde la máquina anfitrión a M1 y M2:

![](https://i.ibb.co/Mk4L0xd/ping-anfitrion.png)

**5. SSH.**

Por último, vamos a comprobar que podemos acceder mediante SSH correctamente entre las 3 máquinas que tenemos.
Para ello hay que ejecutar el siguiente comando:

> ssh (usuario de la red)@(dirección ip a la que acceder)

Una vez ejecutado el comando, introducimos la contraseña del usuario y podremos acceder a la máquina sin problema.
Vamos a ver primero el acceso entre las dos máquinas virtuales:

![](https://i.ibb.co/3CL6vMC/acceso-ssh.png)

Y ahora vemos el acceso desde la máquina anfitrión a ambas máquinas virtuales:

![](https://i.ibb.co/q0t6tty/ssh-anfitrion-m1.png)
![](https://i.ibb.co/vVg4T80/ssh-anfitrion-m2.png)

