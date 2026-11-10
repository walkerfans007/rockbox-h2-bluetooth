# WalkerFans H2 Rockbox Bluetooth

**WalkerFans para el reproductor HIFIWALKER H2 Hi-Fi / DAP / MP3 — actualización de Rockbox con Bluetooth.**

**Etiquetas:** #HIFIWALKER #HIFIWALKERH2 #Rockbox #Bluetooth #DAP #MP3Player #HiFiPlayer

> **Importante — basado en el firmware original HIFIWALKER V2.3.** Esta versión se desarrolló y probó en un H2 con el firmware original HIFIWALKER **V2.3**. Otras versiones del firmware no se han probado y podrían no ser compatibles. Si tu reproductor tiene otra versión, haz antes una copia de seguridad y actualiza bajo tu propia responsabilidad.

**Versión de desarrollo comunitaria · 843986adb6-261110 · versión preliminar** · [English](README.md)

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
- Los archivos DSD se convierten a PCM; la salida de audio es de 16 bits. No hay salida DSD nativa ni de 24 bits.
- Probado en un H2 de desarrollo. LDAC, aptX y otros códecs no se han probado con una amplia gama de auriculares.
- Noto Sans SC no cubre coreano, árabe, hebreo, tailandés ni algunas letras de Europa central; para esos idiomas elige 16-GNU-Unifont en Settings → Theme Settings → Font.
- **Firmware del controlador:** la compilación incluye el parche de RAM del controlador Bluetooth Broadcom/Cypress (`BCM4343A1_001.002.009.0122.0538`). No se encontraron condiciones de licencia ni de redistribución para este archivo y su origen no se ha verificado.

## Créditos y licencias

Adaptación Bluetooth de Skye Green y Cameron (BlackIsBlack), sobre el proyecto Rockbox. Rockbox se distribuye bajo GPL-2.0-or-later; la pila Bluetooth y los códecs, bajo Apache-2.0, por lo que los binarios se distribuyen bajo GPL-3.0. Noto Sans SC usa la SIL Open Font License 1.1. aptX es marca de Qualcomm y LDAC, de Sony.

## Aviso legal

WalkerFans Team es un grupo de aficionados y entusiastas de HIFIWALKER. Este proyecto se comparte solo para desarrollo e intercambio en la comunidad, sin fines comerciales: no obtenemos ningún beneficio económico. No es una versión oficial del proyecto Rockbox. Todas las marcas y derechos de autor pertenecen a sus respectivos propietarios.

Si algún contenido afecta a derechos de autor, patentes u otros derechos que desconozcamos, escríbenos a **walkerfans007@gmail.com** y lo retiraremos.

— **WalkerFans Team** · walkerfans007@gmail.com
