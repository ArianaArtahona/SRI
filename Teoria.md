# Teoria de Streaming

## Indice

1. [Descarga directa vs Streaming](#1-descarga-directa-vs-streaming)
2. [Topología de red](#2-topología-de-red)
3. [Capa de transporte: TCP vs UDP](#3-capa-de-transporte-tcp-vs-udp)
4. []()
5. []()
6. []()
7. []()

---

## 1. Descarga directa vs Streaming

**Descarga directa**

- El archivo completo se descarga al cliente.
- Aunque empiece a reproducirse antes de terminar, el servidor envía el archivo entero.
- Si el usuario deja de escuchar, el servidor ya consumió todo el ancho de banda.

**Streaming**
     
- El servidor envía datos en tiempo real.
- No se guarda el archivo completo en el cliente.
- Solo se consume ancho de banda mientras el usuario escucha.

> Streaming ahorra ancho de banda y es más eficiente para contenido que puede abandonarse antes de terminar.


---

## 2. Topología de red

**Unicast**
- Comunicación 1 servidor → 1 cliente.
- Cada usuario recibe su propio flujo.
- Desventaja: Poco escalable. 


**Multicast**

- El servidor envía un solo flujo a una IP multicast.
- Los routers replican solo si hay clientes.
- Desventaja: Routers bloquean paquetes multicast. Solo viable en redes
internas.

---

## 3. Capa de transporte: TCP vs UDP



















