# WalkerFans H2 Rockbox RX v0.1.4 — Experimental phone receiver + language UI update

**Version:** `H2-RX-v0.1.4-2026-11-12`  
**Source:** `a897b73317c3a677c6ee4bac6d6b2836cc802935`  
**Branch:** `h2-bluetooth-24bit-receiver`  
**Status:** experimental pre-release; not a stable release.

WalkerFans for HIFIWALKER H2 Hi-Fi Player / DAP / MP3 Music Player — Rockbox upgrade with Bluetooth.

**Compatibility:** development and device installation use a HIFIWALKER H2 with original firmware **V2.3** as the baseline. Bluetooth targets **hardware revision 4**. Other original-firmware versions have not been validated on a real player and may be incompatible. This is not a compatibility claim for other HIFIWALKER models.

**Validation:** the RX package has been installed on the development H2 and all written package files were verified. Phone pairing, radio streaming, actual DAC output, long-play stability and the final UI still need hardware validation. Installation and software tests do not establish those results.

**Disclosure:** we are WalkerFans Team, the maintainers and packagers of this build, and our team is affiliated with HIFIWALKER. This is a free community development project, not an official Rockbox release. Development used AI-assisted coding tools.

## What this edition adds

RX extends our experimental 24-bit wired edition with a separate **phone-to-H2 Bluetooth receiver mode**, native language names, a direct Language menu, per-language letter badges and a preferred language order. Existing Standard and 24-bit packages remain separate.

| Edition | Local wired music path | H2 → headphones/speakers | Phone → H2 |
|---|---|---|---|
| [Standard `843986adb6`](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/tag/h2bt-843986adb6-preview) | 16-bit | Transmitter | No |
| [24-bit `a49363b515`](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/tag/h2bt-a49363b515-24bit-preview) | Experimental 24-bit | Transmitter; 16-bit encoder input | No |
| **RX v0.1.4** | Inherited experimental 24-bit | Separate transmitter mode retained | **New SBC receiver mode** |

Transmit and receive modes are mutually exclusive. RX is not a Bluetooth relay.

## Phone receiver

- Open **Settings → Bluetooth Settings → Receive phone audio**. Local playback stops and connected headphones are disconnected before entering receiver mode.
- The player advertises **Rockbox H2 Receiver**. Compare and confirm pairing codes when prompted.
- Receives **SBC at 44.1 or 48 kHz**, decoded to **16-bit PCM** and routed to the wired mixer. Mono input is duplicated to both output channels.
- Provides phone play/pause, phone disconnect and local H2 volume controls. Receiver volume is independent of phone absolute volume.
- Includes bounded buffering, prefill, underrun silence and overflow counters; pause/disconnect flush the buffer. Streaming keeps the player awake.
- Stops reception and Bluetooth before USB handover or shutdown. On exit, the prior Bluetooth on/off state is restored; if previously on, the player attempts to reconnect the last headphones. Local music remains stopped.
- Phone reception does not replace the saved last-headphone reconnect record.

Stay on the receiver screen while receiving audio. These are implemented behaviors with software coverage, not claims of completed phone compatibility testing.

## UI and language changes through v0.1.4

| Revision | Change |
|---|---|
| Initial receiver work | Separate receiver branch and SBC implementation; preserve legacy mixer channel IDs; 14 px top status icons |
| v0.1.1 | Clear dated firmware version; native display names for 48 bundled languages; missing language-name glyphs added to five Noto font sizes |
| v0.1.2 | Move Language directly under Settings and use a blue globe for the entry |
| v0.1.3 | Fix the shared globe appearing on every language row; use per-language letter badges |
| v0.1.4 | Exclude legacy Afrikaans from the picker; pin the requested first ten languages, then sort the rest alphabetically by filename |

**First ten languages:** English (EN) → Español (ES) → Français (FR) → Deutsch (DE) → 日本語 (JA) → 繁體中文 (ZH-T) → Русский (RU) → 한국어 (KO) → Italiano (IT) → العربية (AR).

Remaining languages, including Simplified Chinese, regional variants and custom files, follow in case-insensitive original-filename order, independently of ordinary file-browser sorting. Language filenames, loading and saved settings paths are unchanged. A leftover `afrikaans.lng` is hidden by the picker; the new package does not contain it.

The Settings entry keeps its globe. Language rows use letter badges, not national flags; longer labels such as ZH-S, ZH-T, EN-US and PT-BR use two lines in the default icon cell. Unknown custom files use a question-mark badge.

The top status icons are **14 px**; the **20 px list font**, **16 px clock text** and playback-page layout are retained. Language-list icon cells are separate from the top status icons.

Font additions cover the native language names and related Arabic forms while retaining existing glyphs and metrics. This does **not** establish complete text coverage for every menu in every language, or native-speaker review of all translations.

## Audio scope and limits

- Inherits the 24-bit local wired music path from `a49363b515`: DSP, music buffering, crossfade, mixer, software volume and I2S output retain 24-bit precision in 32-bit containers. Software tests cover low-bit preservation; actual DAC/I2S behavior still requires hardware measurement.
- Wired sample-rate ceiling remains **192 kHz**. Receiver input is limited to **44.1/48 kHz**.
- **Phone reception is lossy SBC decoded to 16-bit PCM. It is not lossless or native 24-bit Bluetooth.** Expanding these samples into a 24-bit mixer adds no information.
- No AAC, aptX, aptX HD or LDAC **receiver** support. Existing transmitter codec capabilities do not imply receiver support.
- Transmitter audio still passes through a 16-bit encoder input and lossy encoding. No simultaneous transmit/receive, Bluetooth relay, microphone or phone-call audio is added.
- Voice prompts, beeps, USB audio and plugin interfaces retain their legacy 16-bit compatibility paths.
- DSD remains software-converted to PCM; no native DSD or DoP is added. EQ, volume, resampling and ReplayGain can change samples: no blanket bit-perfect or improved analog-performance claim is made.
- The receiver has no adaptive clock-drift resampling yet. Extended playback, drift, dropouts, battery use and performance need device testing.

## Validation completed

Earlier receiver-development tests exercised the actual SBC encoder/decoder at both supported rates and mono/stereo; ring-buffer boundaries, prefill, underrun/overflow, pause/restart, malformed/truncated packets and late callbacks; pairing/state transitions, USB/shutdown cleanup; and the inherited 24-bit numeric, mixer, volume and Bluetooth conversion paths. AddressSanitizer/UndefinedBehaviorSanitizer coverage is documented with the source tests. These were host tests, not radio/DAC measurements.

For v0.1.4, language order, legacy Afrikaans filtering, native names, badges and original selection paths passed host checks; the cross-build succeeded; the linked firmware's menu and top-ten order were checked. **523 package files** and **12,165 source files against Git blobs** were verified. Later UI changes did not modify the receiver/audio implementation; earlier audio tests are not represented as new hardware tests.

The complete package was installed on the development H2 after a verified backup. All 523 package files matched after writing, other settings/files were preserved, the specified legacy Afrikaans file was removed, and the card was safely ejected. Actual display, pairing, listening, channel/volume checks, reconnect, prolonged streaming and hardware audio measurements remain pending.

## Install, try and roll back

1. Confirm the H2 hardware/original-firmware baseline and an existing compatible native Rockbox bootloader. This ZIP is a Rockbox file update, **not** a factory `update.upt` or a bootloader installer.
2. Back up the SD card, or at least the entire `.rockbox` directory including settings and pairing records. Do not publish pairing files or link keys.
3. Extract the **complete** ZIP to the SD-card root so `.rockbox` is at the root and the package's files replace the older matching files. Do not combine firmware or plugins from different editions. Safely eject and reboot.
4. Check Rockbox Info for `H2-RX-v0.1.4-2026-11-12`, then inspect **Settings → Language**.
5. Connect wired headphones, start at low volume and open **Settings → Bluetooth Settings → Receive phone audio**.
6. On the phone, pair **Rockbox H2 Receiver**, confirm codes if prompted, select it as the media output and start music. Stay on the receiver screen.
7. Test both channels, pause/resume, disconnect/reconnect, phone interruptions, both supported sample rates and at least 30 minutes of playback. After exiting, check local music and headphone transmission.
8. To roll back, restore the complete `.rockbox` backup or install a complete previous edition according to its instructions. This update does not alter the bootloader or factory update file.

For reports, include the hardware revision, original firmware version, RX build, phone model/OS, receive/transmit/wired mode, sample rate, exact reproduction steps and relevant counters/errors. Redact personal information and pairing keys.

## Assets and source

**Source download:** use the attached `rockbox-h2bt-H2-RX-v0.1.4-2026-11-12-source.tar.gz` for the complete firmware source at the source commit above. This repository hosts release documentation; its release tag and GitHub-generated “Source code” archives refer to the publication documents, not the firmware source tree.

- `rockbox-h2bt-H2-RX-v0.1.4-2026-11-12.zip` — complete SD-card package.
- `rockbox-h2bt-H2-RX-v0.1.4-2026-11-12-source.tar.gz` — source snapshot of the commit above.
- `SHA256SUMS-H2-RX-v0.1.4-public.txt` — release-asset checksums.
- `MANIFEST-H2-RX-v0.1.4-2026-11-12.sha256` — per-package-file checksums.
- `rockbox-info-H2-RX-v0.1.4-2026-11-12.txt` — build information.

```text
1aa33e9cebd451350c691a152553a3137320173784ffb535eff9fced2f3a701f  rockbox-h2bt-H2-RX-v0.1.4-2026-11-12.zip
3dceadc35760cfe2ca63658f425f9b0289922b1388dee0a4b95bc5070e68a71b  rockbox-h2bt-H2-RX-v0.1.4-2026-11-12-source.tar.gz
```

The date in the version is UTC (November 12), corresponding to November 11 in Pacific time. Rebuild instructions and test entry points are in `docs/H2-BT-RECEIVER.md`; `tools/h2bt/build.sh` builds this branch.

## Credits and controller firmware notice

Based on [Rockbox](https://github.com/Rockbox/rockbox), the [BlackIsBlack H2 Bluetooth branch](https://github.com/BlackIsBlack/rockbox-h2-bluetooth), and our preceding 24-bit branch. Original contributor credits, copyrights and licenses are retained. Fonts and other third-party components retain their own license terms.

**Controller firmware:** this edition retains the Broadcom/Cypress controller Patch RAM used by the earlier builds. Its origin and redistribution terms have not been verified; no redistribution clearance is claimed. This notice does not grant permission to redistribute it.

We share this software for development and community exchange and make no profit from this software release. For bugs or copyright/patent concerns, contact **walkerfans007@gmail.com**; we will remove material involving rights we were unaware of.

— **WalkerFans Team**

#HIFIWALKER #HIFIWALKERH2 #Rockbox #Bluetooth #DAP


---

# WalkerFans H2 Rockbox RX v0.1.4 — Receptor experimental para el móvil y mejoras de idiomas

**Versión:** `H2-RX-v0.1.4-2026-11-12`  
**Código fuente:** `a897b73317c3a677c6ee4bac6d6b2836cc802935`  
**Rama:** `h2-bluetooth-24bit-receiver`  
**Estado:** versión preliminar experimental, no estable.

WalkerFans para HIFIWALKER H2, reproductor Hi-Fi / DAP / MP3: actualización de Rockbox con Bluetooth.

**Compatibilidad:** el desarrollo y la instalación en el dispositivo toman como referencia el **HIFIWALKER H2 con firmware original V2.3**. Bluetooth está destinado a la **revisión de hardware 4**. Otras versiones del firmware original no se han validado en un reproductor real y pueden ser incompatibles. Esto no confirma compatibilidad con otros modelos de HIFIWALKER.

**Validación:** el paquete RX se ha instalado en el H2 de desarrollo y se han verificado sus archivos. Aún están pendientes las pruebas físicas de vinculación con teléfonos, recepción por radio, salida del DAC, reproducción prolongada y aspecto final de la interfaz. Instalar los archivos y superar pruebas de software no demuestra esos resultados.

**Declaración:** somos WalkerFans Team, responsables del mantenimiento y empaquetado de esta compilación, y nuestro equipo está vinculado a HIFIWALKER. Es un proyecto comunitario gratuito, no una versión oficial de Rockbox. Se han utilizado herramientas de programación asistida por IA.

## Diferencias entre las ediciones

RX añade un modo independiente de recepción **móvil → H2** a la edición experimental de audio por cable de 24 bits. También actualiza los nombres de idiomas, el menú Language, sus iconos y el orden de la lista. Los paquetes anteriores siguen siendo independientes.

| Edición | Música local por cable | H2 → auriculares/altavoces | Móvil → H2 |
|---|---|---|---|
| [Standard `843986adb6`](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/tag/h2bt-843986adb6-preview) | 16 bits | Transmisión | No |
| [24-bit `a49363b515`](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/tag/h2bt-a49363b515-24bit-preview) | 24 bits experimentales | Transmisión; entrada del codificador de 16 bits | No |
| **RX v0.1.4** | Conserva la ruta experimental de 24 bits | Conserva un modo de transmisión separado | **Nuevo modo receptor SBC** |

No se puede transmitir y recibir simultáneamente. RX no funciona como repetidor Bluetooth.

## Nuevo modo receptor

- Abra **Settings → Bluetooth Settings → Receive phone audio**. Se detiene la música local y se desconectan los auriculares antes de cambiar al modo receptor.
- El nombre visible para el móvil es **Rockbox H2 Receiver**. Compare y confirme los códigos de vinculación cuando se solicite.
- Recibe **SBC a 44,1 o 48 kHz**, decodificado a **PCM de 16 bits**, y lo envía al mezclador de salida por cable. La entrada mono se duplica en ambos canales.
- Ofrece reproducción/pausa del móvil, desconexión y volumen local del H2. El volumen del receptor es independiente del volumen absoluto del teléfono.
- Incluye un búfer limitado, precarga, silencio cuando faltan datos y contadores de desbordamiento. Pausar o desconectar vacía el búfer; la reproducción mantiene despierto el equipo.
- Detiene la recepción y Bluetooth antes de pasar a USB o apagarse. Al salir, restaura el estado previo de Bluetooth y, si estaba encendido, intenta reconectar los últimos auriculares. La música local permanece detenida.
- La recepción del móvil no sustituye el registro de reconexión de los últimos auriculares.

Mantenga abierta la pantalla del receptor mientras escucha. Son comportamientos implementados y probados por software, no una garantía de compatibilidad física con todos los teléfonos.

## Interfaz e idiomas hasta v0.1.4

| Revisión | Cambios |
|---|---|
| Desarrollo inicial | Rama receptora independiente, recepción SBC, conservación de los identificadores antiguos del mezclador e iconos superiores de 14 px |
| v0.1.1 | Versión con fecha completa, nombres nativos para 48 idiomas incluidos y caracteres adicionales en cinco tamaños de fuente Noto |
| v0.1.2 | Language pasa directamente a Settings y su entrada utiliza un globo azul |
| v0.1.3 | Corrige el globo repetido en todas las filas; cada idioma utiliza una abreviatura |
| v0.1.4 | Excluye Afrikaans del selector y fija diez idiomas al principio; ordena el resto por nombre de archivo |

**Primeros diez:** English (EN) → Español (ES) → Français (FR) → Deutsch (DE) → 日本語 (JA) → 繁體中文 (ZH-T) → Русский (RU) → 한국어 (KO) → Italiano (IT) → العربية (AR).

Los demás idiomas, incluido el chino simplificado, las variantes regionales y los archivos personalizados, siguen en orden alfabético por su nombre de archivo original, sin distinguir mayúsculas. Este orden no depende de la configuración del explorador de archivos. No se modifican los nombres `.lng`, su carga ni las rutas de configuración.

Un `afrikaans.lng` heredado de una instalación antigua queda oculto en el selector. El paquete nuevo no lo incluye. El globo se mantiene solo en la entrada de Language; las filas usan abreviaturas, no banderas nacionales. ZH-S, ZH-T, EN-US y PT-BR se distribuyen en dos líneas; los idiomas personalizados desconocidos usan un signo de interrogación.

Los iconos superiores son de **14 px**. Se mantienen la fuente de lista de **20 px**, el reloj de **16 px** y el diseño de la pantalla de reproducción. Las celdas de iconos del selector de idiomas son independientes de los iconos superiores.

Se han añadido los caracteres necesarios para los nombres nativos y ciertas formas árabes, conservando los glifos y métricas existentes. Esto **no** garantiza todos los caracteres de todos los menús ni una revisión de todas las traducciones por hablantes nativos.

## Audio y limitaciones

- Conserva de `a49363b515` la ruta local por cable de 24 bits: DSP, búfer, fundido, mezclador, volumen por software e I2S mantienen precisión de 24 bits en contenedores de 32 bits. Las pruebas de software comprueban los bits menos significativos; el comportamiento real del DAC/I2S necesita mediciones físicas.
- El límite por cable sigue siendo **192 kHz**; el receptor acepta **44,1/48 kHz**.
- **La recepción es SBC con pérdidas, decodificado a PCM de 16 bits. No es Bluetooth sin pérdidas ni recepción nativa de 24 bits.** Ampliar esas muestras para el mezclador no crea información.
- No se añade recepción AAC, aptX, aptX HD ni LDAC. Los códecs del transmisor no implican soporte en el receptor.
- La transmisión mantiene la entrada de 16 bits al codificador y la compresión con pérdidas. No se añaden recepción/transmisión simultáneas, repetidor, micrófono ni audio de llamadas.
- Voz, avisos, audio USB e interfaces de plugins conservan su compatibilidad de 16 bits.
- DSD se convierte a PCM por software; no hay DSD nativo ni DoP nuevos. EQ, volumen, remuestreo y ReplayGain pueden alterar las muestras: no se promete salida bit-perfect ni mejor sonido analógico sin mediciones.
- Aún no hay remuestreo adaptativo para compensar la deriva del reloj. La estabilidad prolongada, los cortes, el consumo y el rendimiento requieren pruebas físicas.

## Pruebas realizadas

Durante el desarrollo del receptor se probaron el codificador/decodificador SBC real en ambas frecuencias y mono/estéreo; límites, precarga, falta/exceso de datos, pausa y reinicio del búfer; paquetes dañados o truncados y eventos tardíos; vinculación, cambios de estado y limpieza al entrar en USB o apagar; y las rutas heredadas de 24 bits, mezcla, volumen y conversión Bluetooth. La cobertura de AddressSanitizer/UndefinedBehaviorSanitizer se documenta en los tests del código fuente. No fueron mediciones de radio o DAC.

En v0.1.4 se verificaron el orden de idiomas, la exclusión de Afrikaans, los nombres, abreviaturas y rutas originales. Se completaron la compilación cruzada, la inspección del menú y del orden real en el firmware enlazado, la verificación de **523 archivos del paquete** y de **12.165 archivos fuente contra los objetos de Git**. Los cambios posteriores de interfaz no alteraron la implementación del receptor/audio; las pruebas anteriores no se presentan como nuevas pruebas físicas.

Se instaló el paquete completo en el H2 de desarrollo tras verificar una copia de seguridad. Los 523 archivos escritos coincidieron, se conservaron los demás archivos y ajustes, se retiró el archivo antiguo de Afrikaans indicado y se expulsó la tarjeta de forma segura. La pantalla, vinculación, sonido, canales, volumen, reconexión, reproducción prolongada y mediciones físicas siguen pendientes.

## Instalación, uso y vuelta a la versión anterior

1. Confirme el hardware, el firmware original y un cargador nativo de Rockbox compatible ya instalado. Este ZIP actualiza archivos: **no** es `update.upt` ni instala el cargador de arranque.
2. Guarde la tarjeta o al menos toda la carpeta `.rockbox`, incluidos ajustes y vinculaciones. No publique archivos de vinculación ni claves.
3. Extraiga el ZIP **completo** en la raíz de la tarjeta, con `.rockbox` en la raíz, sustituyendo los archivos correspondientes del paquete anterior. No mezcle firmware o plugins de distintas ediciones. Expulse la tarjeta y reinicie.
4. Confirme `H2-RX-v0.1.4-2026-11-12` en Rockbox Info y revise **Settings → Language**.
5. Conecte auriculares por cable, empiece con volumen bajo y abra **Settings → Bluetooth Settings → Receive phone audio**.
6. Vincule **Rockbox H2 Receiver** desde el móvil, confirme los códigos, selecciónelo como salida multimedia y reproduzca música. Mantenga abierta la pantalla receptora.
7. Pruebe ambos canales, pausa, desconexión/reconexión, interrupciones del teléfono, ambas frecuencias y al menos 30 minutos de reproducción. Al salir, revise la música local y la transmisión a auriculares.
8. Para volver atrás, restaure la copia completa de `.rockbox` o instale una edición anterior completa según sus instrucciones. Esta actualización no cambia el cargador ni el archivo de actualización original.

Al informar de errores, indique revisión de hardware, firmware original, versión RX, teléfono/sistema, modo de audio, frecuencia, pasos y contadores o mensajes de error. Elimine datos personales y claves.

## Archivos y código fuente

**Descarga del código:** utilice el archivo adjunto `rockbox-h2bt-H2-RX-v0.1.4-2026-11-12-source.tar.gz` para obtener todo el código del firmware. La etiqueta de este repositorio y los archivos “Source code” generados por GitHub corresponden a los documentos de publicación, no al árbol del firmware.

- `rockbox-h2bt-H2-RX-v0.1.4-2026-11-12.zip`: paquete completo para la tarjeta.
- `rockbox-h2bt-H2-RX-v0.1.4-2026-11-12-source.tar.gz`: código del commit indicado.
- `SHA256SUMS-H2-RX-v0.1.4-public.txt`: sumas de los archivos de publicación.
- `MANIFEST-H2-RX-v0.1.4-2026-11-12.sha256`: sumas individuales de los archivos del paquete.
- `rockbox-info-H2-RX-v0.1.4-2026-11-12.txt`: información de compilación.

```text
1aa33e9cebd451350c691a152553a3137320173784ffb535eff9fced2f3a701f  rockbox-h2bt-H2-RX-v0.1.4-2026-11-12.zip
3dceadc35760cfe2ca63658f425f9b0289922b1388dee0a4b95bc5070e68a71b  rockbox-h2bt-H2-RX-v0.1.4-2026-11-12-source.tar.gz
```

La fecha de la versión usa UTC: 12 de noviembre, correspondiente al 11 de noviembre en horario del Pacífico. Consulte `docs/H2-BT-RECEIVER.md` para reproducir las pruebas y `tools/h2bt/build.sh` para compilar.

## Créditos y firmware del controlador

Basado en [Rockbox](https://github.com/Rockbox/rockbox), la [rama Bluetooth de BlackIsBlack](https://github.com/BlackIsBlack/rockbox-h2-bluetooth) y nuestra rama previa de 24 bits. Se conservan créditos, derechos y licencias originales. Las fuentes y otros componentes mantienen sus propias licencias.

**Aviso:** se conserva el Patch RAM del controlador Broadcom/Cypress usado en las ediciones anteriores. Su origen y condiciones de redistribución no se han verificado; no se afirma disponer de autorización para redistribuirlo. Este aviso no concede dicha autorización.

Compartimos este software gratuitamente para desarrollo e intercambio comunitario, sin obtener beneficios de esta publicación. Para errores o cuestiones de derechos de autor/patentes, contacte con **walkerfans007@gmail.com**; retiraremos material que afecte a derechos de los que no teníamos conocimiento.

— **WalkerFans Team**

#HIFIWALKER #HIFIWALKERH2 #Rockbox #Bluetooth #DAP
