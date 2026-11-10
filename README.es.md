# WalkerFans H2 Rockbox Bluetooth

**WalkerFans para el reproductor HIFIWALKER H2 Hi-Fi / DAP / MP3 — actualización de Rockbox con Bluetooth.**

**Etiquetas:** #HIFIWALKER #HIFIWALKERH2 #Rockbox #Bluetooth #DAP #MP3Player #HiFiPlayer

> **Importante — basado en el firmware original HIFIWALKER V2.3.** Esta versión se desarrolló y probó en un H2 con el firmware original HIFIWALKER **V2.3**. Otras versiones del firmware no se han probado y podrían no ser compatibles. Si tu reproductor tiene otra versión, haz antes una copia de seguridad y actualiza bajo tu propia responsabilidad.

## ¿Qué edición debo instalar?

Hay **dos ediciones independientes**. Comparten fuentes, traducciones, barra de estado y funciones Bluetooth. **La única diferencia es la salida de audio por cable.**

| | **Estándar** — recomendada | **24 bits experimental** |
|---|---|---|
| Versión | `843986adb6-261110` | `a49363b515-24bit-261110` |
| Publicación | [h2bt-843986adb6-preview](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/tag/h2bt-843986adb6-preview) | [h2bt-a49363b515-24bit-preview](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/tag/h2bt-a49363b515-24bit-preview) |
| ⬇️ **Descarga** (descomprimir en la raíz de la tarjeta SD) | **[rockbox-h2bt-843986adb6-261110.zip](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/download/h2bt-843986adb6-preview/rockbox-h2bt-843986adb6-261110.zip)** (34,7 MB) | **[rockbox-h2bt-a49363b515-24bit-261110.zip](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/download/h2bt-a49363b515-24bit-preview/rockbox-h2bt-a49363b515-24bit-261110.zip)** (34,7 MB) |
| Código fuente (GPL) · sumas | [código .tar.gz](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/download/h2bt-843986adb6-preview/Walkerfans-H2BT-source-843986adb6-261110.tar.gz) · [SHA256SUMS](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/download/h2bt-843986adb6-preview/SHA256SUMS) | [código .tar.gz](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/download/h2bt-a49363b515-24bit-preview/Walkerfans-H2BT-source-a49363b515-24bit-261110.tar.gz) · [SHA256SUMS](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/download/h2bt-a49363b515-24bit-preview/SHA256SUMS-a49363b515-24bit-261110) |
| Audio por cable | 16 bits (igual que el original) | **24 bits hasta el DAC** |
| Audio Bluetooth | 16 bits, con pérdida (SBC / aptX / aptX HD / LDAC) | igual: 16 bits, con pérdida |
| Estado | funcionando en el H2 de desarrollo | ⚠️ audio aún sin validar en hardware |
| Cambios | [CHANGES-843986adb6-standard.md](CHANGES-843986adb6-standard.md) | [CHANGES-a49363b515-24bit-experimental.md](CHANGES-a49363b515-24bit-experimental.md) |

**Qué cambia la edición Estándar** (respecto a la rama Bluetooth original de BlackIsBlack):
- Fuente predeterminada compatible con chino: Noto Sans SC 20 px, además de 16/18/22/24 px y el paquete completo de fuentes de Rockbox.
- Chino simplificado corregido; chino tradicional rehecho con términos de Taiwán; frases japonesas y francesas que faltaban; textos Bluetooth en siete idiomas.
- Barra de estado de menús con iconos de 20 px, a 10 px del borde superior.
- El Bluetooth ya no se bloquea ni falla si falta el controlador o llegan datos erróneos; mensajes claros en hardware no compatible.
- Script de compilación reproducible.
- Procesamiento de audio sin cambios: 16 bits.

**Qué añade la edición de 24 bits experimental** (todo lo anterior, más):
- DSP de música, búfer, fundido cruzado, mezclador, volumen por software y salida I2S por cable mantienen precisión de 24 bits.
- Voz, pitidos, audio USB y plugins siguen en 16 bits; el Bluetooth se convierte a 16 bits antes de codificar.
- Sin DSD nativo/DoP; límite de 192 kHz; no es bit-perfect con ecualizador, volumen o remuestreo activos.

Instale **solo una** edición a la vez y no mezcle archivos de los dos paquetes. Haga primero una copia de `.rockbox`; cualquiera de las dos se reemplaza instalando el paquete completo de la otra.

## Acerca de este repositorio

**Versión de desarrollo comunitaria · dos ediciones: Estándar `843986adb6-261110` (recomendada) y 24 bits experimental `a49363b515-24bit-261110` · versión preliminar** · [English](README.md)

Mantenido y empaquetado por **WalkerFans Team**, basado en Rockbox y en la rama Bluetooth de BlackIsBlack. No es una versión oficial de Rockbox y no implica ninguna certificación de códecs.

Dispositivo compatible con Bluetooth: **HIFI WALKER H2 con hardware revisión 4, firmware original V1.9–V2.3**. Que la herramienta de restauración admita versiones antiguas no significa que el Bluetooth funcione en hardware antiguo del H2.

## Novedades

- **Bluetooth más fiable:** los envíos HCI tienen tiempo límite en lugar de bloquearse; los paquetes dañados ya no bloquean el reproductor; el hardware antiguo muestra un mensaje claro en lugar de un error.
- **Fuentes:** la fuente predeterminada es Noto Sans SC de 20 px, con chino y japonés completos. Incluye tamaños 16/18/22/24 px y el paquete de fuentes de Rockbox.
- **Traducciones:** chino simplificado corregido (61 errores de traducción), correcciones en chino tradicional, frases añadidas en japonés y francés, y textos de Bluetooth en siete idiomas, incluido el español.
- **Menús:** iconos de la barra de estado de 20 px con un margen superior de 10 px; el contenido del menú empieza debajo de la barra.
- **Compilación reproducible:** un solo script con herramientas fijadas; el mismo commit produce el mismo paquete.

## Instalación

1. El reproductor necesita un cargador de arranque de Rockbox que funcione. En el H2 V2.3 con memoria flash XT26G01C, usa un cargador del 2026-02-03 o posterior.
2. Haz una copia de seguridad de la carpeta `.rockbox` de la tarjeta SD (ahí están los ajustes y los emparejamientos Bluetooth).
3. Descomprime `rockbox-h2bt-843986adb6-261110.zip` en la raíz de la tarjeta SD y deja que reemplace `.rockbox`.
4. Expulsa la tarjeta de forma segura y reinicia el reproductor.

No es un `update.upt` de fábrica y no se instala con el actualizador de fábrica. Consulta el [manual en español](MANUAL.es.md).

## Limitaciones conocidas

- El Bluetooth solo funciona en hardware revisión 4.
- Los archivos DSD se convierten a PCM; no hay salida DSD nativa. La edición Estándar emite 16 bits; la edición experimental emite 24 bits por cable (el Bluetooth sigue en 16 bits).
- Probado en un H2 de desarrollo. LDAC, aptX y otros códecs no se han probado con una amplia gama de auriculares.
- Noto Sans SC no cubre coreano, árabe, hebreo, tailandés ni algunas letras de Europa central; para esos idiomas elige 16-GNU-Unifont en Settings → Theme Settings → Font.
- **Firmware del controlador:** la compilación incluye el parche de RAM del controlador Bluetooth Broadcom/Cypress (`BCM4343A1_001.002.009.0122.0538`). No se encontraron condiciones de licencia ni de redistribución para este archivo y su origen no se ha verificado.

## Créditos y licencias

Adaptación Bluetooth de Skye Green y Cameron (BlackIsBlack), sobre el proyecto Rockbox. Rockbox se distribuye bajo GPL-2.0-or-later; la pila Bluetooth y los códecs, bajo Apache-2.0, por lo que los binarios se distribuyen bajo GPL-3.0. Noto Sans SC usa la SIL Open Font License 1.1. aptX es marca de Qualcomm y LDAC, de Sony.

## Aviso legal

WalkerFans Team es un grupo de aficionados y entusiastas de HIFIWALKER. Este proyecto se comparte solo para desarrollo e intercambio en la comunidad, sin fines comerciales: no obtenemos ningún beneficio económico. No es una versión oficial del proyecto Rockbox. Todas las marcas y derechos de autor pertenecen a sus respectivos propietarios.

Si algún contenido afecta a derechos de autor, patentes u otros derechos que desconozcamos, escríbenos a **walkerfans007@gmail.com** y lo retiraremos.

— **WalkerFans Team** · walkerfans007@gmail.com
