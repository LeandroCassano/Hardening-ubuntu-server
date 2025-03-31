<h1>Firewalls en linux</h1>

Vamos a empezar esta guía para fortalecer nuestro servidor por medio del firewall, para ello vamos a usar Nftables.
En mi caso uso la consola del servidor desde mi Kali Linux por medio del protocolo ssh (Solo por comodidad), ya que nombramos este protocolo, vamos a empezar por ahí.

El puerto 22 es donde corre el `protocolo ssh / secure Shell`, este protocolo esta diseñado para acceder y administrar dispositivos de forma remota de manera segura y cifrada. 
Teniendo en cuenta esto entendemos lo peligroso que es tenerlo desprotegido.
La manera correcta de utilizarlo es denegar todo acceso salvando la ip del dispositivo que usemos para conectarnos.. 
de esta manera solo esa dirección va a poder tener acceso, para eso vamos a usar nftables.
_____
Desde la shell con el comando *`sudo ufw status numbered`* vamos a listar las reglas con un numero, eso nos va a ayudar a especificar reglas.

![](https://i.ibb.co/Tx48YDmG/ssh-reglas-sin-editar.jpg) 

Como vemos no hay ninguna restriccion cuanto a las conexiones en puerto 22 tanto para ipv4 como ipv6, vamos a cambiar esto.
Con el comando *`Sudo ufw delete`* eliminamos reglas, usamos los numeros que fueron listados con el comando anterior 

*`sudo ufw delete 3`* y *`sudo ufw delete 6`* para eliminarlas ya que son las que contemplan el puerto 22 y creamos las nuevas, en mi caso voy a configurar solo
ipv4 (En el caso de no usar ipv6 denegar todo acceso)

*`sudo ufw allow from "192.168.1.100" to any port 22`* Vamos a desglosar el comando..

>sudo: Ejecuta el comando con permisos de administrador (necesario para modificar reglas del firewall).

>ufw: Es el comando principal de Uncomplicated Firewall.

>from 192.168.1.100: Solo permite conexiones desde la IP 192.168.1.100 (un host específico).

>to any: El tráfico puede dirigirse a cualquier interfaz/dirección IP del servidor.

>port 22: Se refiere al puerto 22 (SSH), que es el puerto de administración remota por defecto en Linux.



Ya creada la regla vamos a listar nuevamente con el comando *`sudo ufw status numbered`* y revisar que se haya aplicado

![](https://i.ibb.co/rfs62Rdg/ssh-regla-editada.jpg)

Ahora tenemos el puerto 22 /ssh controlado, en el apartado de `from` visualizamos la direccion ip del dispositivo del que nos vamos a conectar y administrar el servidor.

Con esto logramos que el puerto 22 no solo acepte trafico de nuestra direccion ip denegando conexiones de cualquier otro dispositivo sino que tambien esta libre de scaneos e intentos de acceso no autorizados
