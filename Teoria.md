# Teoria de Streaming

## Indice

1. [Descarga directa vs Streaming](#1-descarga-directa-vs-streaming)
2. [Topología de red](#2-topología-de-red)
3. [Capa de transporte: TCP vs UDP](#3-capa-de-transporte-tcp-vs-udp)
4. [QoS: Jitter, Buffer](#4-qos-jitter-buffer)
5. [Protocolos de Streaming](#5-protocolos-de-streaming)
6. [Icecast](#6-icecast)
7. [Códecs](#7-códecs)
8. [Cálculo de peso](#8-cálculo-de-peso)

---

## 1. Descarga directa vs Streaming

**1.1 Descarga directa**

- El archivo completo se descarga al cliente.
- Aunque empiece a reproducirse antes de terminar, el servidor envía el archivo entero.
- Si el usuario deja de escuchar, el servidor ya consumió todo el ancho de banda.

**1.2 Streaming**
     
- El servidor envía datos en tiempo real.
- No se guarda el archivo completo en el cliente.
- Solo se consume ancho de banda mientras el usuario escucha.

> Streaming ahorra ancho de banda y es más eficiente para contenido que puede abandonarse antes de terminar.


---

## 2. Topología de red

**2.1 Unicast**
- Comunicación 1 servidor → 1 cliente.
- Cada usuario recibe su propio flujo.
- Desventaja: Poco escalable. 


**2.2 Multicast**

- El servidor envía un solo flujo a una IP multicast.
- Los routers replican solo si hay clientes.
- Desventaja: Routers bloquean paquetes multicast. Solo viable en redes
internas.

---

## 3. Capa de transporte: TCP vs UDP

**3.1 TCP**
- Fiable: retransmisión de paquetes perdidos.
- Orden correcto garantizado.
- Más latencia.

**3.2 UDP**

- No hay retransmisión.
- Menos latencia.
- Puede haber pérdidas

> Streaming bajo demanda → TCP
>
> Tiempo real (videollamada, juegos) → UDP

---

## 4. QoS: Jitter, Buffer

**4.1 Jitter (Fluctuación)**

Variación del tiempo de llegada de paquetes.
Si es alto → cortes.

**4.2 Buffer**

Memoria temporal que guarda segundos de audio/vídeo.

- Buffer grande → más estabilidad
- Buffer grande → más latencia

Si el jitter supera el buffer → Buffer Underrun

> Buffer underrun: Cuando el buffer se vacía → se corta el audio.

**4.3 Burst-on-Connect**

Técnica donde el servidor envía datos iniciales a alta velocidad para llenar rápidamente el buffer del cliente y que el audio empiece casi de inmediato.

Proceso:

- Cliente conecta
- Servidor envía ráfaga
- Buffer se llena
- Empieza audio
- Velocidad vuelve a normal

Reduce el Time To First Byte.

---

## 5. Protocolos de Streaming

**5.1 HTTP Legacy (Icecast)**

- TCP
- Flujo continuo
- Formatos MP3, OGG, AAC
- Latencia media (10–30 s)

**5.2 HTTP Adaptativo (HLS, DASH)**

- TCP
- Vídeo dividido en trozos (chunks)
- Calidad adaptativa

**5.3 Real-Time**

- `RTMP (Real-Time Messaging Protocol)`: funciona sobre TCP, esta obsoleto para el usuario final pero se usa para enviar videos al servidor
- `RTSP (Real-Time Streaming Protocol)`: funciona sobre UDP para los datos y TCP para control, usado en camaras de seguridad.
- `WebRTC`: para videoconferencia. P2P, cifrado, UDP, funciona en
navegador sin plugins (Google Meet, Discord)

>Netflix, HBO, Disney+, etc utilizan HTTP adaptativo. Al ver una película se estan
>descargando pequeños chunks, trozos del vídeo, secuencialmente vía TCP. 
>
>Spotify y Apple Music también usa TCP.
>
>Twitch (del lado del receptor): usa TCP. Por eso hay un delay.
>
>La radio online también es TCP
>
>Cuando se necesita interactuar con la otra parte el delay no es admisible y por
>tanto se utiliza UDP.

---

## 6. Icecast

Servidor de streaming de audio.

- No genera audio.
- Funciona como una antena virtual
-  Usa HTTP/ICY.
- Maneja oyentes.
-  Permite varios puntos de montaje

---

## 7. Códecs

Un códec es un algoritmo que permite:

- Comprimir un archivo de audio o vídeo.
- Descomprimirlo posteriormente para reproducirlo.

`El objetivo es reducir el tamaño del archivo y el ancho de banda necesario manteniendo la mayor calidad posible.`

Ejemplos de códecs de audio

- MP3, AAC, Vorbis, WAV

Ejemplos de códecs de vídeo

- H.264, H.265 (HEVC), AV1

---

**7.1 Frecuencia de muestreo**

Número de veces por segundo que se “fotografía” la onda sonora.
Se mide en Hz.

Estándar de calidad CD: 44.100 Hz (44.1kHz)

Cuanto mayor frecuencia → mayor fidelidad.

>La frecuencia de muestreo indica cuántas muestras por segundo se toman de una señal >analógica para digitalizarla.

---

**7.2 Profundidad de bits**

Cantidad de bits usados para representar cada muestra.
Define la precisión de cada “foto”.

Estandar de calidad CD: 16 bits

>La profundidad de bits determina la resolución de cada muestra de audio; a mayor >profundidad, mayor calidad.

---

**7.3 Canales**
Número de pistas de audio independientes.

- Mono → 1 canal
- Estéreo → 2 canales
- Surround → más de 2

Más canales → más tamaño.

---

**7.4 Códecs con pérdida vs sin pérdida**

- Códecs con pérdida:  reducen peso sacrificando información que
puede ser imperceptible por el oído humano.
Al comprimirlo dicha información se pierde y es irrecuperable.
Ejemplo: MP3. 

- Códecs sin pérdida:  comprime el fichero como lo haría un .zip
pero sin eliminar información. Al descomprimir el flujo de bits es
idéntico al original.
Ejemplo: FLAC, WAV. 

---

## 8. Cálculo de peso






















