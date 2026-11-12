# WalkerFans H2 Rockbox Bluetooth

**WalkerFans for HIFIWALKER H2 Hi-Fi Player / DAP / MP3 Music Player — Rockbox upgrade with Bluetooth.**

**Tags:** #HIFIWALKER #HIFIWALKERH2 #Rockbox #Bluetooth #DAP #MP3Player #HiFiPlayer

> **Important — based on HIFIWALKER original firmware V2.3.** This build was developed and tested on an H2 running the original HIFIWALKER firmware **V2.3**. Other firmware versions have not been tested and may not be compatible. If your player runs a different version, back up first and upgrade at your own risk.

## Experimental RX edition: phone reception and language UI

**H2-RX-v0.1.4-2026-11-12** adds a separate **phone → H2 SBC receiver mode** to the experimental 24-bit wired branch. It also adds native language names, Settings → Language, per-language badges, a preferred language order and 14 px top status icons.

**Status:** installed on the development H2 with file verification; new radio reception, actual audio output, long-play stability and final UI still await hardware validation. Development/device-installation baseline: **original firmware V2.3; Bluetooth hardware revision 4**. Other original-firmware versions may be incompatible.

| Edition | Wired music path | Bluetooth transmission | Phone reception |
|---|---|---|---|
| [Standard preview](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/tag/h2bt-843986adb6-preview) | 16-bit | Yes | No |
| [24-bit experimental](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/tag/h2bt-a49363b515-24bit-preview) | Experimental 24-bit | Yes; 16-bit encoder input | No |
| RX v0.1.4 — [Release / Downloads](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/tag/h2-rx-v0.1.4-preview) | Inherits experimental 24-bit | Separate mode | SBC, 44.1/48 kHz, decoded to 16-bit PCM |

Receiver audio is lossy, not native 24-bit Bluetooth. There is no simultaneous transmit/receive or relay. Use one complete edition at a time and keep a backup for rollback. See the RX release notes for installation, test status and the unresolved controller-firmware redistribution notice.

**[Download RX v0.1.4 ZIP](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/download/h2-rx-v0.1.4-preview/rockbox-h2bt-H2-RX-v0.1.4-2026-11-12.zip)** · [Complete firmware source](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/download/h2-rx-v0.1.4-preview/rockbox-h2bt-H2-RX-v0.1.4-2026-11-12-source.tar.gz)

## Which edition should I install?

There are **three separate editions**. RX adds experimental phone reception and an updated language UI; the following comparison describes the two earlier transmit-only editions.

| | **Standard** — recommended | **24-bit experimental** |
|---|---|---|
| Version | `843986adb6-261110` | `a49363b515-24bit-261110` |
| Release | [h2bt-843986adb6-preview](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/tag/h2bt-843986adb6-preview) | [h2bt-a49363b515-24bit-preview](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/tag/h2bt-a49363b515-24bit-preview) |
| ⬇️ **Download** (unzip to the SD card root) | **[rockbox-h2bt-843986adb6-261110.zip](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/download/h2bt-843986adb6-preview/rockbox-h2bt-843986adb6-261110.zip)** (34.7 MB) | **[rockbox-h2bt-a49363b515-24bit-261110.zip](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/download/h2bt-a49363b515-24bit-preview/rockbox-h2bt-a49363b515-24bit-261110.zip)** (34.7 MB) |
| Source code (GPL) · checksums | [source .tar.gz](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/download/h2bt-843986adb6-preview/Walkerfans-H2BT-source-843986adb6-261110.tar.gz) · [SHA256SUMS](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/download/h2bt-843986adb6-preview/SHA256SUMS) | [source .tar.gz](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/download/h2bt-a49363b515-24bit-preview/Walkerfans-H2BT-source-a49363b515-24bit-261110.tar.gz) · [SHA256SUMS](https://github.com/walkerfans007/rockbox-h2-bluetooth/releases/download/h2bt-a49363b515-24bit-preview/SHA256SUMS-a49363b515-24bit-261110) |
| Wired audio | 16-bit (same as upstream) | **24-bit kept to the DAC** |
| Bluetooth audio | 16-bit, lossy (SBC / aptX / aptX HD / LDAC) | same: 16-bit, lossy |
| Bluetooth direction | **Transmit only** (H2 → headphones/speakers). The H2 is not discoverable and cannot receive audio from a phone; phone pairing fails. Use the original firmware for receiver mode. | same: transmit only |
| Status | running on the development H2 | ⚠️ not yet audio-validated on hardware |
| Changes | [CHANGES-843986adb6-standard.md](CHANGES-843986adb6-standard.md) | [CHANGES-a49363b515-24bit-experimental.md](CHANGES-a49363b515-24bit-experimental.md) |

**What the Standard edition changes** (compared with the upstream BlackIsBlack Bluetooth branch):
- Chinese-capable default font: Noto Sans SC 20 px, plus 16/18/22/24 px and the full Rockbox font pack.
- Corrected Simplified Chinese; Traditional Chinese rebuilt with Taiwan wording; missing Japanese and French strings added; Bluetooth strings in seven languages.
- Menu status bar with 20 px icons, 10 px from the top.
- Bluetooth no longer freezes or crashes on a missing controller or bad data; clear messages on unsupported hardware.
- Reproducible build script.
- Audio processing unchanged: 16-bit.

**What the 24-bit experimental edition adds** (everything above, plus):
- Music DSP, buffer, crossfade, mixer, software volume and wired I2S output keep 24-bit precision.
- Voice, beeps, USB audio and plugins stay 16-bit; Bluetooth is converted to 16-bit before encoding.
- No native DSD/DoP, sample-rate limit still 192 kHz, not bit-perfect when EQ/volume/resampling are active.

Install **one** edition at a time and never mix files from different packages. Back up `.rockbox` first; an edition can be replaced by another by installing its full package.

## About this repository

**Community development builds · Standard, 24-bit experimental and RX v0.1.4 · pre-releases**

Maintained and packaged by **WalkerFans Team**, based on Rockbox and the BlackIsBlack Bluetooth branch. Preserve all upstream author credits. This is not an official Rockbox release and does not imply codec certification.

Bluetooth target: **HIFI WALKER H2 hardware revision 4, original firmware V1.9–V2.3**. Do not generalize the Bluetooth feature to older H2 hardware just because the recovery tool supports older versions.

Changes include Bluetooth fault handling, larger CJK-capable fonts, reviewed Chinese translations, additional translated Bluetooth/menu strings, and 20-pixel menu status icons with a 10-pixel top margin. The menu content starts below the status bar; the existing playback page layout is retained.

The package contains 518 files and has been copied/verified on the development H2 while preserving settings and pairing records. That confirms package delivery, not broad headphone compatibility, continuous playback stability or audio-output measurement.

Read [the manual](MANUAL.en.md), [changes](CHANGELOG.md) and release notes ([Standard](RELEASE.md) · [24-bit experimental](RELEASE-a49363b515-24bit.md)). **Español:** [README](README.es.md) · [Manual](MANUAL.es.md). The build script and provenance notes are included with the source.

**Controller firmware notice:** the build includes Broadcom/Cypress Bluetooth controller patch RAM (`BCM4343A1_001.002.009.0122.0538`). No license or redistribution terms for this file were found in the source branch, and its origin has not been verified. No redistribution clearance is claimed. See [UPSTREAM-PROVENANCE.txt](UPSTREAM-PROVENANCE.txt).

## Attribution

Release credit: **WalkerFans Team**. Base: Rockbox master `baa2b4564b`; Bluetooth changes replayed from BlackIsBlack release `h2-bt-20261023-2f059ce`. Original contributor credits include Skye Green and Cameron. Noto Sans SC retains its Adobe/Google notices and OFL license. Preserve Rockbox GPL, Apache, BSD and font notices; component licenses are not replaced by the publishing signature.

## Disclaimer

WalkerFans Team is a group of HIFIWALKER fans and geeks. This project is shared for development and community exchange only, and is non-commercial: we make no profit from it. It is not an official Rockbox project release. All trademarks and copyrights belong to their respective owners.

If any content here involves a copyright, patent or other right we are not aware of, please contact us at **walkerfans007@gmail.com** and we will remove it.

— **WalkerFans Team** · walkerfans007@gmail.com
