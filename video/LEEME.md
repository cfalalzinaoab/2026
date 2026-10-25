# `web/video/` · los vídeos de clase

Aquí van los vídeos que salen en CAS y en PAU +25, debajo de los días de
clase y de la liga bodegueril. Cada uno se pinta como una prueba de imprenta
—el fotograma con sus marcas de corte, la marca de registro de la materia y
la cuña de tono— y al pulsarlo se abre el MP4 en otra pestaña, con el
reproductor del navegador.

Hoy hay uno: **Las interrogativas indirectas** (10 min 13 s, 1920 × 1080),
de la pieza 3 del dossier de PAU +25. Sale en las dos materias.

## Qué lleva cada vídeo

Tres archivos con el mismo nombre de base:

| archivo | qué es |
|---|---|
| `nombre.mp4` | el vídeo, tal cual sale del montaje pero con el índice delante (`+faststart`), para que empiece a verse antes de bajarse entero |
| `nombre-noche.webp` | un fotograma de una diapositiva **oscura**, para el taller de noche |
| `nombre-dia.webp` | un fotograma de una diapositiva **clara**, para el taller a plena luz |

Los dos fotogramas van a 1280 × 720. Son dos y no uno porque una imagen
oscura sobre el papel crema se lee como una mancha, y a esta no se le puede
bajar el tono: tiene que parecerse a lo que se ve al pulsar. Conviene que no
lleven «PAU +25» escrito si el vídeo sale también en CAS.

## Cómo se cuelga otro

`ffmpeg` no está en el PATH: es el de imageio-ffmpeg, en
`C:\Users\Oscar\AppData\Local\Programs\Python\Python311\Lib\site-packages\imageio_ffmpeg\binaries\ffmpeg-win-x86_64-v7.1.exe`.

1. El vídeo, sin volver a comprimirlo:

   ```bash
   ffmpeg -i "salida/montaje.mp4" -map 0 -c copy -movflags +faststart video/nombre.mp4
   ```

   GitHub avisa por encima de 50 MB y rechaza por encima de 100. El de las
   interrogativas pesa 54 MB y entra con aviso.

2. Los dos fotogramas, eligiendo el segundo de cada uno:

   ```bash
   ffmpeg -ss 3.5 -i video/nombre.mp4 -frames:v 1 -vf scale=1280:720:flags=lanczos -c:v libwebp -quality 82 video/nombre-noche.webp
   ffmpeg -ss 66 -i video/nombre.mp4 -frames:v 1 -vf scale=1280:720:flags=lanczos -c:v libwebp -quality 82 video/nombre-dia.webp
   ```

3. Su entrada en `index.html`, al lado de `VIDEO_INTERROGATIVAS`, y su nombre
   en la lista de cada materia que lo lleve:

   ```js
   const VIDEOS = {
     cas:[VIDEO_INTERROGATIVAS],
     pau:[VIDEO_INTERROGATIVAS, VIDEO_NUEVO]
   };
   ```

   Los campos son `rotulo`, `titulo`, `pie`, `duracion`, `url`, `noche` y
   `dia`. El orden de la lista es el orden en la página.

Lo que hay que publicar después es `index.html` y los tres archivos nuevos.
