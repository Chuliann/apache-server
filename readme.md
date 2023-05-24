En este archivo voy a indicar las instrucciones para crear y configurar un servidor apache en ubuntu, considerando que lo hosteamos desde nuestra propia casa

1) Creamos y configuramos nuestro nombre dns (opcional)
En este caso vamos a usar https://www.noip.com, que nos provee uno gratuito

2) Hay que configurar el equipo
    *Si es una maquina virtual -> Configuracion red -> Adaptador puente
    (Para que considere la maquina virtual como un equipo mas de nuestra red privada)

3) Comprobar la resolucion de los dns
    *Comprobar que tenemos internet -> networkctl status
    *Podemos comprobar que los dns funcionan con nslookup *dominio*, y que la direccion es la misma que nos aparece en la interfaz de noip
    *clear

Es posible que el router de casa no posea una ip estatica, si no que sea dinamica y frecuentemente cambie, si esto pasa, noip va a estar apuntando el nombre de dominio a una ip antigua, esto se puede solucionar varias maneras

4) Configurar el router/equipo para que se actualize
    *Configuracion del servidor de nombres dinamicos (DynDNS)
    *Instalar el cliente no-ip en ubuntu

5) Instalar apache
    * sudo apt-get update
    * sudo apt-get install apache2

6) Configurar pagina web
    Por default, el apache ya corre y vamos a editar el index.html
        * ls /var/www/html/
        * sudo nano /var/www/html/index.html
    Mas tarde agregamos nuestro sitio web


Ahora, cuando le llega una peticion de afuera al router, le llega por el puerto 80, pero el router no sabe que hacer con la peticion.
Le tenemos que decir al router que cada peticion que llegue por el puerto 80, la rediriga al equipo que tiene el servidor web.

7) Configurar el router
    * COnfigurar la tabla NAT del router
    * Configurar el firewall
        *Verificar que el puerto 80 no esta bloqueado
    * Comprobar puertos de entradas
        * ss -ltpan
        * nmap julianberton.hopto.org -p 80
               * sudo apt-get install nmap

La documentacion para configurar el servidor apache se encuentra en:
    * cat /usr/share/doc/apache2/README.Debian
