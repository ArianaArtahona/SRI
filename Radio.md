# Práctica 1 - Radio 

## Indice

1. [Introducción](#introducción)
2. [Configuracion de la maquina](#1-configuracion-de-la-maquina-virtual)

## Introducción
La **radio online** es la transmisión de audio a través de Internet, permitiendo que oyentes en cualquier lugar del mundo puedan sintonizar un programa en tiempo real. A diferencia de la radio tradicional, que utiliza ondas de radiofrecuencia, la radio online depende de un **servidor de streaming** y un **cliente emisor**.

---

## Componentes principales

1. **Servidor de streaming**  
   - Software que recibe el audio de una fuente y lo distribuye a los oyentes, en este caso **Icecast2**. 
   - Funciones:
     - Gestiona oyentes simultáneos.
     - Administra puntos de montaje (mount points), en este caso:  `/ari`.
     - No genera el contenido, solo lo distribuye.

2. **Cliente emisor (DJ)**  
    - Programa que envía el audio al servidor, en este caso **Mixxx**.
    - Permite reproducir listas de música, transmitir en vivo y controlar la calidad del audio.

---

## 1. Configuración de la maquina virtual
En este caso utilice adaptador puente para más adelante usar la máquina anfitrión como oyente

Por lo que con `ip a` observe la ip y la guarde para despues

---

## 2. Instalación y configuracion de Icecast2:

###  2.1 Instalar Icecast2
```bash
sudo apt update 
sudo apt install icecast2 -y
```
Durante la instalación:

-Seleccionar **Yes** cuando pregunte si desea configurar Icecast2.

-Usar la misma contraseña para todas las opciones.

### 2.2 Configuración básica

Editar archivo de configuración

```bash
sudo nano /etc/icecast2/icecast.xml
```

Cambiar el hostname: `<hostname>icecast_server</hostname>` en mi caso, icecast_server.

Reiniciar el servidor:

```bash
sudo systemctl restart icecast2
sudo systemctl status icecast2
```

Probar en el navegador:
```
http://localhost:8000 #por defecto icecast escucha este puerto
```

---


## 3. Instalación y configuración de Mixxx

### 3.1 Instalar Mixxx

```bash
sudo add-apt-repository ppa:mixxx/mixxx
sudo apt update
sudo apt install mixxx
```

### 3.2 Configurar emisión en Mixxx

Con mixxx abierto:

```
Options → Preferences → Live Broadcasting
```

Configurar los datos de la transmisión:

```bash
Tipo: Icecast2
Servidor: 127.0.0.1
Montar: /ari
Puerto: 8000 #por defecto
Identificación: admin
Contraseña: la misma de icecast
```

Formato recomendado:

```
MP3 - 128 kbps
```

Guardar y luego de poner en vivo un MP3, ir al navegador, en este caso el del anfitrión para probar el streaming

```
http://192.168.1.131:8000/ari
```

Adjunto imagen de como se ve el funcionamiento: [foto](radio.png)

>Resultado esperado:
> - Icecast2 funcionando correctamente
> - Mixxx conectado al servidor
> - Se puede oir al unisono en la maquina anfitrión




















