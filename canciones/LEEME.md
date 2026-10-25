# `web/canciones/` · la canción de cada unidad

Aquí va la canción de cada unidad de Castellano 2, la que hace Oscar con Suno.
La ficha de la unidad, en el portal, la enseña con su reproductor en la fila
«Canción de la unidad». Esa fila ocupa el sitio de las del cuaderno en PDF y
de soluciones, que Oscar quitó el 25 de octubre de 2026.

## Cómo se cuelga

1. El MP3 se guarda aquí con **este nombre exacto**: `unidad-01.mp3`,
   `unidad-02.mp3`… Dos dígitos, como los `.md` y como los `.html`.
   **Tal cual lo da Suno**: sin recortarlo, sin convertirlo y sin tocarle las
   etiquetas. Lleva dentro la marca C2PA de que está hecho con IA, y cambiar
   la cabecera la deja sin validar.
2. Su título va en `CANCIONES`, en `_unidad.py` (en la raíz del curso):

   ```python
   CANCIONES = {"01": "Dime qué te gusta", "02": "…"}
   ```

   No se lee del archivo: el título que trae de Suno es el de trabajo
   («Dime qué te gusta — A2 (capa Suno)»).
3. Se pasa el generador de esa unidad:

   ```bash
   python _unidad.py 02
   ```

   `avance()` escribe el título y la ruta en el `AVANCE` de `index.html`, y la
   fila pasa de «Pronto» al reproductor. Si falta el archivo o falta el
   título, la fila se queda en «Pronto» y el generador avisa de qué falta.

Lo que hay que publicar después es `index.html` y el MP3 nuevo. La página de
la unidad no cambia.
