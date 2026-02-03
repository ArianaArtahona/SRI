# Práctica de Video Streaming

## Indice
1. [Introducción](#1-introducción)
2. [Instalacion y configuración de FFmpeg](#2-instalacion-y-configuración-de-ffmpeg)
3. [Comprobar los datos](#3-comprobar-los-datos)
4. [Cambio de contenedor](#4-cambio-de-contenedor)
5. [Cambios de codecs](#5-cambios-de-codecs)

## 1. Introducción

En esta práctica se va trabajar con archivos de vídeo para explorar de manera práctica cómo afectan los contenedores, los códecs y el bitrate al tamaño de los archivos, a la calidad de imagen y al uso de recursos. A través de distintos ejercicios se analizará y comparará los resultados.

## 2. Instalacion y configuración de FFmpeg

### 2.1 Instalación
Se instala con : `sudo apt install ffmpeg -y`

---

## 3. Comprobar los datos

```bash
ffprobe -v error -show_streams video.mp4
```

Lo mas importante del resultado:
```
- width=1920
- height=1080
- duration=30.000000
- avg_frame_rate=24/1       
- codec_name=H264           
- bits_per_raw_sample=8
```

---

## 4. Cambio de contenedor

```bash
ffmpeg -i video.mp4 -c:v copy -c:a copy video.mkv
```
Con este comando se cambia de mp4 a mkv el archivo, haciendo que tenga un cambio menor en el peso del archivo pero no afecta en el contenido original y para la cpu esto no es ningun problema por lo que va rápido como normalmente lo hace

---

## 5. Cambios de codecs

Crear el archivo H.264

```bash
ffmpeg -i video.mp4 -c:v libx264 -b:v 2M -c:a copy h264_2mbps.mp4
```

```
-i video.mp4 → indica el archivo original.
-c:v libx264 → codifica el vídeo en H.264.
-b:v 2M → bitrate de 2 Mbps (controla la calidad/tamaño).

```

El archivo h264_2mbps.mp4 pesa mas que original y consume bastante cpu y lo hace mucho mas lento que la anterior copia

```bash
ffmpeg -i video.mp4 -c:v libx265 -b:v 2M -c:a copy h265_2mbps.mp4
```
Este archivo h265_2mbps.mp4 pesa aun mas que el h264 y tardó mucho más en crear la copia ya que uso mas recursos de la cpu

Y he aqui la imagen de ambas copias puestas en comparacion, [comparacion](comparacion.png) el h264_2mbps.mp4 se nota un poco más pixeleado en partes del video donde hay más movimiento que con h265_2mbps.mp4 ya que `H.265 (HEVC) usa técnicas de compresión más avanzadas que H.264 (AVC)`

