
Primero que nada, vamos a hacer un repaso teórico sobre los distintos tipos de firewalls y la importancia de los mismos. Si el caso de la visita es la implementación y configuración pueden saltear al siguiente archivo donde empieza la guía practica. 

<h1> Firewalls </h1>

Un firewall es un sistema de seguridad que actúa como una barrera entre una red interna confiable y redes externas no confiables, como internet. El propósito principal es filtrar y controlar el tráfico de red basándose en un conjunto de reglas o políticas predefinidas. Este proceso ayuda a proteger los sistemas de accesos no autorizados, ataques maliciosos, y otras amenazas.
El mecanismo de filtrado agrega una capa adicional de seguridad al diseño general de la infraestructura, trabajando junto con otros mecanismos de protección, como antivirus y sistemas de detección de intrusos.

La protección contra accesos no autorizados evita que actores maliciosos puedan conectarse a tu servidor desde redes externas. Ayuda a bloquear ataques como DDoS, spoofing, y escaneos de puertos, que intentan descubrir vulnerabilidades en el servidor.
Tiene un gran control sobre servicios expuestos, ya que, permite decidir qué servicios son accesibles desde la red externa, por ejemplo HTTP limitando lo que puede ser explotado.
_______________________________________

Los firewalls pueden clasificarse de acuerdo con la forma en que manejan y filtran el tráfico.



El filtrado de paquetes / Packet Filtering

Examina cada paquete de datos que pasa a través de la red. Evalúa la dirección IP de origen y destino, el puerto y el protocolo. Dependiendo de las reglas configuradas, permite o bloquea el tráfico.
Es rápido y sencillo, sin mucho procesamiento pero, no tiene conocimiento de la conexión completa (no sabe si el paquete pertenece a una conexión legítima o no).




Inspección con estado / Stateful Inspection

A diferencia del filtrado de paquetes, los firewalls stateful mantienen el estado de las conexiones. Monitorean el estado completo de las sesiones, permitiendo que solo los paquetes que pertenecen a conexiones válidas sean aceptados.
Se caracteriza por tener mayor seguridad que el filtrado de paquetes, ya que puede seguir el estado de las conexiones, aunque requiere más recursos del sistema para gestionar el estado de cada conexión.




Proxy Firewall
Un firewall proxy actúa como intermediario entre el cliente y el servidor. Este tipo de firewall reenvía las solicitudes de conexión después de inspeccionarlas y asegurarse de que son seguras.
Es exageradamente seguro y da cierta capa de anonimato, oculta la verdadera red interna y puede realizar filtrado profundo de contenido. El costo de tal seguridad esta en que puede ser más lento, ya que analiza el contenido de las conexiones.




El famoso Web Application Firewall (WAF)

El WAF está diseñado específicamente para proteger aplicaciones web. Se enfoca en inspeccionar las solicitudes HTTP/HTTPS para detectar y bloquear amenazas comunes, como inyección SQL, Cross-Site Scripting (XSS) y ataques de denegación de servicio (DoS).
Protege directamente las aplicaciones web de vulnerabilidades específicas. Pero deja de proteger otras partes de la infraestructura
Como se explica deja cubiertos únicamente servicios web.
________________________________________



Firewalls en Linux

UFW (Uncomplicated Firewall)

UFW es una herramienta de firewall sencilla y fácil de usar en Ubuntu. Está diseñada para usuarios que no necesitan configuraciones avanzadas y desean gestionar sus reglas de firewall de manera rápida.
Cuenta con una Interfaz sencilla para usuarios novatos y queda Ideal para administradores que solo necesitan habilitar o deshabilitar puertos o servicios, sumado a que su configuración es rápida para reglas básicas.
A tener en cuenta de forma negativa  es la falta de flexibilidad en configuraciones avanzadas y que no ofrece tantas opciones de personalización como iptables o nftables.




Iptables

iptables es la herramienta tradicional y poderosa para configurar firewalls en Linux. Permite crear reglas detalladas de filtrado de tráfico, controlando cómo se maneja el tráfico entrante, saliente y redirigido.
Es bastante flexible  y da control detallado sobre el tráfico de red. puede filtrar por IP, puerto, protocolos, interfaces y mucho más. Ademas permite crear configuraciones complejas y altamente personalizadas. Requiere más conocimientos técnicos para configurarlo correctamente, ya que, la configuración suele ser más compleja, lo que puede generar errores si no se maneja adecuadamente.




Nftables

nftables es una herramienta de firewall introducida en versiones recientes de Linux para reemplazar iptables. Ofrece un enfoque más moderno y eficiente, con una sintaxis más simple y mejor rendimiento.
Actualmente reemplaza a iptables y es más eficiente en términos de rendimiento. Cuenta con una sintaxis más sencilla y flexible y como si fuera poco es compatible con iptables, por lo que facilita la migración de configuraciones antiguas.
