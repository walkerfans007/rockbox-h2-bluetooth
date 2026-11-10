# WalkerFans H2 Bluetooth — Manual rápido

> **Importante — basado en el firmware original HIFIWALKER V2.3.** Esta versión se desarrolló y probó en un H2 con el firmware original HIFIWALKER **V2.3**. Otras versiones del firmware no se han probado y podrían no ser compatibles. Si tu reproductor tiene otra versión, haz antes una copia de seguridad y actualiza bajo tu propia responsabilidad.

Versión `843986adb6-261110`. El Bluetooth es para el **H2 con hardware revisión 4 (firmware original V1.9–V2.3)**. Este ZIP actualiza una instalación existente de Rockbox erosqnative; no es un `update.upt` de fábrica. Instala primero el cargador de arranque de Rockbox correcto. Las unidades V2.3 con la memoria flash nueva necesitan un cargador HW4 del 2026-02-03 o posterior.

## Instalación

Haz una copia de seguridad de toda la carpeta `.rockbox`, incluidos `config.cfg` y `bt_config.conf`. Los registros de emparejamiento contienen claves de enlace: no los publiques nunca. Descomprime el ZIP y combina su carpeta `.rockbox` directamente en la raíz de la tarjeta, reemplazando los archivos del programa sin crear una carpeta adicional. Verifica los archivos, expulsa la tarjeta de forma segura, desconecta y reinicia. Comprueba que aparece `843986adb6-261110` en la información del sistema.

## Emparejar auriculares

Pon los auriculares en modo de emparejamiento. Ve a Settings → Bluetooth Settings → Devices, selecciona el dispositivo y pulsa Play. Sigue las indicaciones si se pide un código. La compatibilidad depende de los auriculares. Si falla la conexión o el audio, desconecta otros teléfonos y prueba con SBC. Activa Debug Logging solo mientras reproduces un problema y elimina los datos sensibles antes de compartir el registro.

## Fuentes y menús

Fuente predeterminada: 20-NotoSansSC; se incluyen tamaños 16/18/22/24 y el paquete de fuentes de Rockbox. Los iconos de estado del menú miden 20 px con un margen superior de 10 px. Si la fuente predeterminada no cubre tu idioma, usa 16-GNU-Unifont. Las mejoras de traducción aún necesitan revisión por hablantes nativos.

## Limitaciones de audio

Los archivos DSD64/128/256 (DSF y DFF sin comprimir) se decodifican por software a PCM; no hay salida DSD nativa ni DoP. Las pruebas de DSD en el ordenador no equivalen a pruebas de rendimiento en tiempo real en el H2. La salida actual del DSP/mezclador es PCM de 16 bits. La salida por cable admite hasta 192 kHz según los ajustes. El Bluetooth usa códecs con pérdida negociados con los auriculares, no transmite los archivos de alta resolución sin cambios. No se declara ninguna certificación de códecs ni compatibilidad amplia con dispositivos.

## Volver atrás y soporte

Para volver atrás, restaura la copia de seguridad de la carpeta `.rockbox`. La restauración de fábrica requiere el paquete del firmware original correspondiente; WalkerFans H2 Tools incluye por ahora solo la V2.3. Para informar de un fallo, indica las versiones, el modelo de auriculares y los pasos para reproducirlo, pero elimina las claves de emparejamiento, las direcciones y los registros privados.

Publicación y documentación: **WalkerFans Team**. Se conservan los autores originales y los avisos de licencia de cada componente. Esta es una versión preliminar de desarrollo. El origen y las condiciones de redistribución del firmware del controlador Bluetooth no se han verificado.

Proyecto comunitario sin fines comerciales de WalkerFans Team. Si algún contenido afecta a derechos de autor o patentes que desconozcamos, escribe a walkerfans007@gmail.com y lo retiraremos.
