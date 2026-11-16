# Fundamentos: SWITCH
## Diferencia entre Hub y Switch
* Hub: Es un dispositivo básico de la *capa física*. Cuando recibe un paquete de datos, **lo reqplica y lo envía a todos los puertos** conectados, sin importar quién sea el destinatario. Esto satura el ancho de banda, genera colisiones de tráfico y ofrece una seguridad muy baja porque todos los equipos ven la información.
* Switch: Es un dispositivo inteligente de la *capa de enlace de datos*. Utiliza una tabla de direcciones físicas (direcciones MAC) para identificar a qué puerto está conectado cada equipo. Cuando recibe datos, **los envía únicamente al puerto del dispositivo destinatario**.

## Tabla CAM (*Content Addressable Memory*)
Es la base de datos interna que utiliza un Switch para saber hacia qué puerto físico debe enviar una trama Ethernet.
Se le conoce habitualmente como **Tabla de direcciones MAC**.
### Funcionamiento
1. **Aprendizaje**(Learning): Cuando un switch recibe una trama por uno de sus puertos revisa la **dirección MAC de origen** de esa trama y la anota en la tabla CAM junto con el número de puerto por el que entró y la VLAN correspondiente.
2. **Reenvío**(Forwarding): Cuando el switch recibe una trama con una **dirección MAC de destino** específica, busca esa MAC en su tabla CAM.
    * Si la encuentra: Envía la trama únicamente por el puerto asociado a esa MAC.
    * No la encuentra (Flooding): Si el destino no está registrado, el switch copia y reenvía la trama por todos sus puertos (excepto por elq ue la recibió) para intentar que llegue al equipo correcto.
3. **Tiempo de expiración** (Aging Time): Las entradas en la tabla no son permanentes (por defecto suelen durar 300 segundos en equipos como Cisco). Si un dispositivo deja de enviar tráfico durante ese tiempo, su entrada se borra para mantener la tabla limpia y adaptada a cambios en la topología.

## Protocolo ARP (Address Resolution Protocol)
Es un protocolo de comunicaciones que traduce direcciones IP (capa de red) a direcciones MAC (capa de enlace de datos física) en redes locales.
### Funcionamiento
1. **Consulta inicial**: Cuando un equipo de la red local quiere comunicarse con otro, revisa su caché ARP para ver si ya conoce la dirección MAC asociada a la IP de destino.
2. **Petición por difusión** (ARP Request): Si no la conoce, envía un mensaje de difusión (broadcast, con MAC `FF:FF:FF:FF:FF:FF`) a toda la red preguntando: «¿Quién tiene esta dirección IP? Dígame su MAC».
3. **Respuesta** (ARP Reply): El dispositivo que posee esa IP responde directamente (unicast) al remitente con su propia dirección MAC.
4. **Almacenamiento**: El equipo emisor guarda esa relación (IP - MAC) en su tabla o caché ARP temporalmente para futuras comunicaciones.