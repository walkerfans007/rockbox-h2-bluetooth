# WalkerFans H2 Rockbox Bluetooth — 843986adb6-261110 Standard Preview

**WalkerFans for HIFIWALKER H2 Hi-Fi Player / DAP / MP3 Music Player — Rockbox upgrade with Bluetooth.**

**Tags:** #HIFIWALKER #HIFIWALKERH2 #Rockbox #Bluetooth #DAP #MP3Player #HiFiPlayer

> **Important — based on HIFIWALKER original firmware V2.3.** This build was developed and tested on an H2 running the original HIFIWALKER firmware **V2.3**. Other firmware versions have not been tested and may not be compatible. If your player runs a different version, back up first and upgrade at your own risk.

> **Standard edition — recommended.** This is the 16-bit edition for everyday use. A separate [24-bit experimental edition](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/tag/h2bt-a49363b515-24bit-preview) (`a49363b515-24bit-261110`) keeps 24-bit precision on the wired output but has not yet been audio-validated on hardware. See [Which edition should I install?](https://github.com/walkerfans007/rockbox-h2-bluetooth/#which-edition-should-i-install) and the full [Standard edition changelog](https://github.com/walkerfans007/rockbox-h2-bluetooth/blob/main/CHANGES-843986adb6-standard.md).

A community development build of Rockbox with Bluetooth audio for the HIFI WALKER H2 **hardware revision 4** (original firmware **V1.9–V2.3**). Based on Rockbox master and the BlackIsBlack H2 Bluetooth branch.

## Highlights

- **Bluetooth reliability:** HCI sends time out instead of hanging; corrupt packets no longer crash the player; older hardware gets a clear "needs hardware rev 4" message instead of a failure.
- **Fonts:** the default UI font is Noto Sans SC 20 px, with full Chinese and Japanese coverage. 16/18/22/24 px sizes and the full Rockbox font pack are included.
- **Translations:** Simplified Chinese corrected (61 mistranslations fixed), Traditional Chinese fixes, missing Japanese and French phrases added, and Bluetooth strings in seven languages.
- **Menu layout:** 20-pixel status bar icons with a 10-pixel top margin; menu content starts below the status bar.
- **Reproducible build:** one-step build script with pinned toolchain; the same commit produces the same package.

## Installation

1. The player needs a working Rockbox bootloader. On H2 V2.3 with XT26G01C flash, use a bootloader from 2026-02-03 or later.
2. Back up the `.rockbox` folder on your SD card (settings and Bluetooth pairings live there).
3. Extract `rockbox-h2bt-843986adb6-261110.zip` to the root of the SD card and let it replace `.rockbox`.
4. Safely eject the card and restart the player.

This is not a factory `update.upt` and cannot be installed with the factory updater.

## Known limitations

- Bluetooth works on hardware revision 4 only.
- Audio is processed and output at 16 bits, unchanged from upstream; DSD files are converted to PCM (no native DSD or DoP). For 24-bit wired output, see the separate [24-bit experimental edition](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/tag/h2bt-a49363b515-24bit-preview).
- Tested on one development H2. LDAC, aptX and other codecs have not been tested across headphones, and no codec certification is implied.
- Noto Sans SC does not cover Korean, Arabic, Hebrew, Thai or some Central European letters; for those languages choose 16-GNU-Unifont under Settings → Theme Settings → Font.
- **Controller firmware:** the build includes Broadcom/Cypress Bluetooth controller patch RAM (`BCM4343A1_001.002.009.0122.0538`). No license or redistribution terms for this file were found, and its origin has not been verified.

## Downloads

| File | Description |
|---|---|
| `rockbox-h2bt-843986adb6-261110.zip` | SD card package (518 files) |
| `Walkerfans-H2BT-source-843986adb6-261110.tar.gz` | Complete source (see BUILD.md) |
| `MANIFEST-843986adb6-261110.sha256` | SHA-256 of every file in the package |
| `SHA256SUMS` | Checksums for all files |

See the [manual](https://github.com/walkerfans007/rockbox-h2-bluetooth/blob/main/MANUAL.en.md), [changelog](https://github.com/walkerfans007/rockbox-h2-bluetooth/blob/main/CHANGELOG.md), [build guide](https://github.com/walkerfans007/rockbox-h2-bluetooth/blob/main/BUILD.md) and [provenance notes](https://github.com/walkerfans007/rockbox-h2-bluetooth/blob/main/UPSTREAM-PROVENANCE.txt).

## Credits and licenses

Bluetooth port by Skye Green and Cameron (BlackIsBlack), on top of the Rockbox project. Rockbox is GPL-2.0-or-later; the Bluetooth stack and codecs are Apache-2.0, so binaries are distributed under GPL-3.0. Noto Sans SC is under the SIL Open Font License 1.1. aptX is a Qualcomm trademark and LDAC a Sony trademark.

Maintained and released by **WalkerFans Team**. Not an official Rockbox release and not supported by the Rockbox project.

## Español

> **Importante — basado en el firmware original HIFIWALKER V2.3.** Esta versión se desarrolló y probó en un H2 con el firmware original HIFIWALKER **V2.3**. Otras versiones del firmware no se han probado y podrían no ser compatibles. Si tu reproductor tiene otra versión, haz antes una copia de seguridad y actualiza bajo tu propia responsabilidad.

Versión de desarrollo de Rockbox con audio Bluetooth para el HIFIWALKER H2 con hardware revisión 4 (firmware original V1.9–V2.3). Incluye fuentes más grandes compatibles con chino y japonés, traducciones corregidas y un Bluetooth más fiable. Es la **edición Estándar recomendada**: la salida de audio es de 16 bits y el DSD se convierte a PCM. Para salida por cable de 24 bits existe una [edición experimental de 24 bits](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/tag/h2bt-a49363b515-24bit-preview), aún sin validar en hardware. Consulta el [README en español](https://github.com/walkerfans007/rockbox-h2-bluetooth/blob/main/README.es.md) y el [manual en español](https://github.com/walkerfans007/rockbox-h2-bluetooth/blob/main/MANUAL.es.md).

## Disclaimer

WalkerFans Team is a group of HIFIWALKER fans and geeks. This project is shared for development and community exchange only, and is non-commercial: we make no profit from it. It is not an official Rockbox project release. All trademarks and copyrights belong to their respective owners.

If any content here involves a copyright, patent or other right we are not aware of, please contact us at **walkerfans007@gmail.com** and we will remove it.

— **WalkerFans Team** · walkerfans007@gmail.com
