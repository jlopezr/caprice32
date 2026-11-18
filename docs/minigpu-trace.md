# Capturas para MiniGPU

Esta rama local añade una captura puntual, reproducible y pensada para
analizar recursos de un cartucho CPC Plus. No sustituye los snapshots ni las
herramientas de desarrollo de Caprice32.

```sh
cap32 -O system.model=3 \
  --trace_dir ../43.fixit/trace \
  --trace_frame 900 --trace_exit \
  ../43.fixit/Fix_It_Felix_version_1_0.cpr
```

Al completar el frame indicado (el primero es el 1), genera
`trace/frame-000900/`:

| Archivo | Contenido |
| --- | --- |
| `screen.png` | Frame compuesto que se ve en Caprice32. |
| `snapshot.sna` | Estado completo de máquina en el formato de snapshot de Caprice32. |
| `ram.bin` | RAM física, contigua, de `ram_bytes` bytes. |
| `asic-sprites.bin` | 16 sprites Plus, 16×16 píxeles, un byte de índice por píxel. |
| `manifest.json` | Versión del formato, frame, banking, paleta y posiciones/ampliación de sprites. |

`--trace_exit` es opcional: sirve para automatización. Sin él Caprice32 sigue
ejecutándose después de escribir el dump.

Los datos están sin convertir deliberadamente. Un conversor externo puede
usar `manifest.json` para validar la paleta y producir recursos RGB565 para
MiniProcessing sin depender del layout interno de un snapshot.
