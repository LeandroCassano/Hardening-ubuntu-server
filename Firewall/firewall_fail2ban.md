<h1>Fail2ban contra ataques de fuerza bruta</h1>

Primero que nada, que es un ataque de fuerza bruta?
Un ataque de fuerza bruta es un método por el cual un atacante prueba combinaciones de manera sistemática hasta encontrar la correcta. 
Usan programas automatizados con un “diccionario” en formato .txt cargado de contraseñas filtradas y millones de palabras y combinaciones. 
Como vimos en el post pasado, configuramos con nftables el puerto 22 para que solo nuestra maquina tenga acceso. Pero que pasa si necesitamos que nuestro servidor maneje distintas conexiones ssh de distintas direcciones ip? O queremos protegernos de un ataque de fuerza bruta con un spoofing de nuestra ip permitida?

_______

Para eso tenemos Fail2ban, esta herramienta revisa los logs de distintos servicios como por ejemplo ssh, buscando intentos de logeo con sus respectiva ip. 
Realiza un conteo de intentos fallidos y en una determinada cantidad aplica una regla de fiewall y bloquea el trafico entrante de esa dirección (clásico baneo de ip)




Una vez instalado vamos a habilitarlo y revisamos el estado (Si esta corriendo o desactivado) `sytemctl status fail2ban`

![](https://i.ibb.co/fz8pr7Z2/status-fail2ban.jpg)


Fail2ban funciona con "`jails`" (reglas para servicios específicos). Asique vamos a configurar uno para ssh
El archivo predeterminado de configuración es `/etc/fail2ban/jail.conf`, pero vamos a crear una copia local 
`sudo cp /etc/fail2ban/jail.conf    /etc/fail2ban/jail.local`


Abrimos el archivo de configuración con nano
`sudo nano /etc/fail2ban/jail.local`

Y buscamos el apartado `ssh` 
Desde este archivo vamos a escribir los parámetros correspondientes



![](https://i.ibb.co/23ffkQp4/nano-config-fail2ban.jpg)



>Algunas claraciones:
>
>maxretry = 3       Intentos fallidos antes de bloquear
>
>bantime = 1h      Tiempo de bloqueo (1 hora)
>
>findtime = 10m   Ventana de tiempo para contar intentos
>


En el apartado de Ignoreip agregamos las direcciones ip las cuales van a ser ignoradas a esta regla, no lo recomiendo ya que nos volveríamos a quedar vulnerables a un spoofing.

Reiniciamos `systemctl restart fail2ban`

Para ver las ip baneadas usamos `sudo fail2ban-client status sshd`



![](https://i.ibb.co/21hXcKH1/regla-jail-ssh-fail2ban.jpg)



En el caso de tener ips baneadas aca podríamos verlas.
Asi como hacemos con este puerto podemos asegurar el resto de servicios que creamos necesarios en nuestro servidor editando el jail.
