# WalkerFans H2 Rockbox Bluetooth — a49363b515-24bit-261110 Experimental (24-bit wired)

> [!WARNING]
> **Experimental edition — not yet audio-validated on hardware.** For everyday use, install the recommended **Standard edition** [`843986adb6-261110`](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/tag/h2bt-843986adb6-preview). Use this edition only if you want to test 24-bit wired playback and can go back to the Standard edition if something sounds wrong.

**WalkerFans for HIFIWALKER H2 Hi-Fi Player / DAP / MP3 Music Player — Rockbox upgrade with Bluetooth.**

**Tags:** #HIFIWALKER #HIFIWALKERH2 #Rockbox #Bluetooth #DAP #MP3Player #HiFiPlayer #24bit

> **Important — based on HIFIWALKER original firmware V2.3.** This build was developed and tested on an H2 running the original HIFIWALKER firmware **V2.3**. Other firmware versions have not been tested and may not be compatible. If your player runs a different version, back up first and upgrade at your own risk.

## Which edition is this?

| | Standard — recommended | **This release: 24-bit experimental** |
|---|---|---|
| Version | `843986adb6-261110` | **`a49363b515-24bit-261110`** |
| Wired audio | 16-bit | **24-bit kept to the DAC** |
| Bluetooth audio | 16-bit, lossy | 16-bit, lossy |
| Status | running on the development H2 | ⚠️ not yet audio-validated on hardware |

See [Which edition should I install?](https://github.com/walkerfans007/rockbox-h2-bluetooth/#which-edition-should-i-install) on the repository homepage.

## What this edition changes

**Version:** `a49363b515-24bit-261110` · **Branch:** `h2-bluetooth-24bit` · **Audio path:** 24-bit wired
**Status:** ⚠️ **experimental pre-release — not yet audio-validated on hardware**
**Package:** `rockbox-h2bt-a49363b515-24bit-261110.zip` (519 files)
**SHA-256:** `025b7dffdab221b0f17e46a9d733455b071626aad3e53cff4d05cb0e09012629`

This edition is the Standard edition `843986adb6-261110` **plus one change: the wired audio path keeps 24-bit precision** from the decoder to the DAC. Fonts, translations, status bar and Bluetooth features are identical to the Standard edition. Bluetooth audio is still 16-bit and lossy.

### Based on
- Standard edition `843986adb6-261110` (all of its changes are included; see its changelog).
- Two additional commits:
  - `0855be3ef4` — separate experimental 24-bit wired PCM pipeline
  - `a49363b515` — keep the older DAC's anti-auto-mute offset in 24-bit software volume

### What changes compared with the Standard edition

#### Audio path
- Music DSP output switched to **24-bit samples stored in 32-bit containers** (8 bytes per stereo frame). The Standard edition outputs 16-bit.
- The music buffer, crossfade, mixer and software volume keep 24-bit precision.
- Wired DMA / I2S sends 24-bit data to the DAC, including on hardware that uses DAC-side volume.
- When dither is enabled on the 24-bit path, it is TPDF dither targeted at the 24-bit least significant bit.
- On older hardware generations that use software volume, the small DC offset the original driver adds to stop the DAC from auto-muting is kept.

#### Compatibility kept at 16-bit
- Voice prompts, beeps, USB audio and plugins still use their original 16-bit interfaces; they are converted up to 24-bit where they enter the mixer.
- **Bluetooth:** audio is converted from 24-bit to 16-bit just before the encoder, with the doubled buffer size handled, then sent through the same SBC / aptX / aptX HD / LDAC encoders as before. Bluetooth is **not** 24-bit and **not** lossless.
- The digital peak meter is scaled to the original 16-bit range.

#### Files
- Added `.rockbox/docs/H2-24BIT.txt` (what this edition changes, its limits and how to test it). This is the one extra file compared with the Standard package.
- Build script builds into separate folders and package names, so the two editions never overwrite each other.

### What does not change
- Wired sample-rate limit remains 192 kHz.
- DSD is still converted to PCM in software; there is no native DSD or DoP output.
- 16-bit source files do not gain any resolution.
- EQ, volume below 0 dB, resampling, ReplayGain and crossfade change sample values, so this is not "bit-perfect" output.
- Bluetooth codec negotiation and the 44.1 kHz per-connection preference are the same as the Standard edition.

### Audio specifications

| Item | Standard `843986adb6` | **24-bit experimental `a49363b515-24bit`** |
|---|---|---|
| Internal processing and wired output | 16-bit | **24-bit (in 32-bit containers)** |
| 24-bit FLAC / WAV on the wired output | reduced to 16-bit | **24-bit kept to the DAC driver** |
| Wired sample-rate limit | 192 kHz | 192 kHz |
| Bluetooth | 16-bit, lossy | 16-bit, lossy (converted before the encoder) |
| DSD | converted to PCM | converted to PCM |

### Validation
- Done on a computer: five test groups run against this branch's production C code with AddressSanitizer and UndefinedBehaviorSanitizer — 24-bit data kept for 8,192 stereo frames down to the lowest bit; mono, 16-bit input, full-scale clipping and buffer edges; mixing 24-bit with 16-bit channels; Bluetooth 24→16-bit conversion, volume and mute; DSP routing and plugin compatibility; software volume and the older DAC offset.
- Done: clean cross-build; all 519 package files verified; package installed on the development H2 (2026-11-09) with every written file verified.
- **Not done:** listening and measurement on hardware. I2S data alignment on different H2 hardware generations, noise, left/right channels, volume steps, battery use and real-time performance at high sample rates have not been verified. Proving that the DAC really receives valid 24-bit data needs a digital capture or electrical measurement; file tags or listening alone are not proof.

### Before you install
- Back up the whole `.rockbox` folder, including `config.cfg` and `bt_config.conf`. Pairing records contain link keys: never publish them.
- Same hardware and bootloader requirements as the Standard edition. Bluetooth requires H2 hardware revision 4.
- Extract the full ZIP to the card root so its `.rockbox` folder replaces the old one. **Do not mix files from the two editions.** Ideally test on a separate SD card first.
- Start with low volume. Check for noise, pops, distortion, wrong playback speed or pitch, and test Bluetooth playback as well.
- After reboot, System → Rockbox Info should show `a49363b515-24bit-261110`.

### Going back
Restore your `.rockbox` backup, or install the full Standard edition package `843986adb6-261110`. This edition does not change the bootloader.

Please report problems with your H2 hardware version, the file format and sample rate, and whether you used wired or Bluetooth output.

## Downloads

| File | Description |
|---|---|
| `rockbox-h2bt-a49363b515-24bit-261110.zip` | SD card package (519 files) |
| `Walkerfans-H2BT-source-a49363b515-24bit-261110.tar.gz` | Complete source of branch `h2-bluetooth-24bit` at `a49363b515` (see BUILD.md) |
| `MANIFEST-a49363b515-24bit-261110.sha256` | SHA-256 of every file in the package |
| `rockbox-info-a49363b515-24bit-261110.txt` | Build information (target, version, toolchain) |
| `SHA256SUMS-a49363b515-24bit-261110` | Checksums for all files above |

Full changelog: [CHANGES-a49363b515-24bit-experimental.md](https://github.com/walkerfans007/rockbox-h2-bluetooth/blob/main/CHANGES-a49363b515-24bit-experimental.md). Build guide: [BUILD.md](https://github.com/walkerfans007/rockbox-h2-bluetooth/blob/main/BUILD.md).

**Controller firmware:** like the Standard edition, this build includes Broadcom/Cypress Bluetooth controller patch RAM (`BCM4343A1_001.002.009.0122.0538`). No license or redistribution terms for this file were found, and its origin has not been verified.

## Credits and licenses

Bluetooth port by Skye Green and Cameron (BlackIsBlack), on top of the Rockbox project. Rockbox is GPL-2.0-or-later; the Bluetooth stack and codecs are Apache-2.0, so binaries are distributed under GPL-3.0. Noto Sans SC is under the SIL Open Font License 1.1. aptX is a Qualcomm trademark and LDAC a Sony trademark.

Maintained and released by **WalkerFans Team**. Not an official Rockbox release and not supported by the Rockbox project.

## Español

> **Edición experimental — audio aún sin validar en hardware.** Para el uso diario, instala la **edición Estándar** recomendada [`843986adb6-261110`](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/tag/h2bt-843986adb6-preview).

> **Importante — basado en el firmware original HIFIWALKER V2.3.** Esta versión se desarrolló y probó en un H2 con el firmware original HIFIWALKER **V2.3**. Otras versiones del firmware no se han probado y podrían no ser compatibles. Si tu reproductor tiene otra versión, haz antes una copia de seguridad y actualiza bajo tu propia responsabilidad.

Esta edición es la edición Estándar `843986adb6-261110` **más un único cambio: la salida de audio por cable mantiene 24 bits** desde el decodificador hasta el DAC (DSP de música, búfer, fundido cruzado, mezclador, volumen por software y salida I2S). Fuentes, traducciones, barra de estado y Bluetooth son idénticos.

- Voz, pitidos, audio USB y plugins siguen en 16 bits; el Bluetooth se convierte a 16 bits antes de codificar y sigue siendo con pérdida.
- Sin DSD nativo/DoP; límite de 192 kHz; no es bit-perfect con ecualizador, volumen o remuestreo activos.
- Probado en ordenador (pruebas con AddressSanitizer/UBSan) e instalado en el H2 de desarrollo, pero **sin escucha ni medición en hardware**.
- Haz una copia de seguridad de `.rockbox` (incluidos `config.cfg` y `bt_config.conf`; nunca publiques los emparejamientos). Descomprime el ZIP completo en la raíz de la tarjeta, no mezcles archivos de las dos ediciones y empieza con volumen bajo.
- Para volver: restaura la copia de `.rockbox` o instala el paquete completo de la edición Estándar.

Consulta el [README en español](https://github.com/walkerfans007/rockbox-h2-bluetooth/blob/main/README.es.md).

## Disclaimer

WalkerFans Team is a group of HIFIWALKER fans and geeks. This project is shared for development and community exchange only, and is non-commercial: we make no profit from it. It is not an official Rockbox project release. All trademarks and copyrights belong to their respective owners.

If any content here involves a copyright, patent or other right we are not aware of, please contact us at **walkerfans007@gmail.com** and we will remove it.

— **WalkerFans Team** · walkerfans007@gmail.com
