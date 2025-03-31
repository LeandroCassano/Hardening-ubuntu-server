<h1>Firewalls en linux</h1>

Vamos a empezar esta guía para fortalecer nuestro servidor por medio del firewall, para ello vamos a usar Nftables.
En mi caso uso la consola del servidor desde mi Kali Linux por medio del protocolo ssh (Solo por comodidad), ya que, nombramos este protocolo vamos a empezar por ahí.

El puerto 22 es donde corre el protocolo ssh / secure Shell, este protocolo esta diseñado para acceder y administrar dispositivos de forma remota de manera segura y cifrada. 
Teniendo en cuenta esto entendemos lo peligroso que es tenerlo desprotegido.
La manera correcta de utilizarlo es denegar todo acceso salvando la ip del dispositivo que usemos para conectarnos.. 
de esta manera solo esa dirección va a poder tener acceso, para eso vamos a usar nftables.
_____
