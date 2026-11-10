# WalkerFans H2 Rockbox Bluetooth — 24-bit experimental edition

> **Important — based on HIFIWALKER original firmware V2.3.** Developed and tested on an H2 running the original HIFIWALKER firmware **V2.3**. Other firmware versions have not been tested and may not be compatible. Back up first and upgrade at your own risk.

**Version:** `a49363b515-24bit-261110` · **Branch:** `h2-bluetooth-24bit` · **Audio path:** 24-bit wired
**Status:** ⚠️ **experimental pre-release — not yet audio-validated on hardware**
**Package:** `rockbox-h2bt-a49363b515-24bit-261110.zip` (519 files)
**SHA-256:** `025b7dffdab221b0f17e46a9d733455b071626aad3e53cff4d05cb0e09012629`

This edition is the Standard edition `843986adb6-261110` **plus one change: the wired audio path keeps 24-bit precision** from the decoder to the DAC. Fonts, translations, status bar and Bluetooth features are identical to the Standard edition. Bluetooth audio is still 16-bit and lossy.

Use it only if you want to test 24-bit wired playback and can go back to the Standard edition if something sounds wrong.

## Based on
- Standard edition `843986adb6-261110` (all of its changes are included; see its changelog).
- Two additional commits:
  - `0855be3ef4` — separate experimental 24-bit wired PCM pipeline
  - `a49363b515` — keep the older DAC's anti-auto-mute offset in 24-bit software volume

## What changes compared with the Standard edition

### Audio path
- Music DSP output switched to **24-bit samples stored in 32-bit containers** (8 bytes per stereo frame). The Standard edition outputs 16-bit.
- The music buffer, crossfade, mixer and software volume keep 24-bit precision.
- Wired DMA / I2S sends 24-bit data to the DAC, including on hardware that uses DAC-side volume.
- When dither is enabled on the 24-bit path, it is TPDF dither targeted at the 24-bit least significant bit.
- On older hardware generations that use software volume, the small DC offset the original driver adds to stop the DAC from auto-muting is kept.

### Compatibility kept at 16-bit
- Voice prompts, beeps, USB audio and plugins still use their original 16-bit interfaces; they are converted up to 24-bit where they enter the mixer.
- **Bluetooth:** audio is converted from 24-bit to 16-bit just before the encoder, with the doubled buffer size handled, then sent through the same SBC / aptX / aptX HD / LDAC encoders as before. Bluetooth is **not** 24-bit and **not** lossless.
- The digital peak meter is scaled to the original 16-bit range.

### Files
- Added `.rockbox/docs/H2-24BIT.txt` (what this edition changes, its limits and how to test it). This is the one extra file compared with the Standard package.
- Build script builds into separate folders and package names, so the two editions never overwrite each other.

## What does not change
- Wired sample-rate limit remains 192 kHz.
- DSD is still converted to PCM in software; there is no native DSD or DoP output.
- 16-bit source files do not gain any resolution.
- EQ, volume below 0 dB, resampling, ReplayGain and crossfade change sample values, so this is not "bit-perfect" output.
- Bluetooth codec negotiation and the 44.1 kHz per-connection preference are the same as the Standard edition.

## Audio specifications

| Item | Standard `843986adb6` | **24-bit experimental `a49363b515-24bit`** |
|---|---|---|
| Internal processing and wired output | 16-bit | **24-bit (in 32-bit containers)** |
| 24-bit FLAC / WAV on the wired output | reduced to 16-bit | **24-bit kept to the DAC driver** |
| Wired sample-rate limit | 192 kHz | 192 kHz |
| Bluetooth | 16-bit, lossy | 16-bit, lossy (converted before the encoder) |
| DSD | converted to PCM | converted to PCM |

## Validation
- Done on a computer: five test groups run against this branch's production C code with AddressSanitizer and UndefinedBehaviorSanitizer — 24-bit data kept for 8,192 stereo frames down to the lowest bit; mono, 16-bit input, full-scale clipping and buffer edges; mixing 24-bit with 16-bit channels; Bluetooth 24→16-bit conversion, volume and mute; DSP routing and plugin compatibility; software volume and the older DAC offset.
- Done: clean cross-build; all 519 package files verified; package installed on the development H2 (2026-11-09) with every written file verified.
- **Not done:** listening and measurement on hardware. I2S data alignment on different H2 hardware generations, noise, left/right channels, volume steps, battery use and real-time performance at high sample rates have not been verified. Proving that the DAC really receives valid 24-bit data needs a digital capture or electrical measurement; file tags or listening alone are not proof.

## Before you install
- Back up the whole `.rockbox` folder, including `config.cfg` and `bt_config.conf`. Pairing records contain link keys: never publish them.
- Same hardware and bootloader requirements as the Standard edition. Bluetooth requires H2 hardware revision 4.
- Extract the full ZIP to the card root so its `.rockbox` folder replaces the old one. **Do not mix files from the two editions.** Ideally test on a separate SD card first.
- Start with low volume. Check for noise, pops, distortion, wrong playback speed or pitch, and test Bluetooth playback as well.
- After reboot, System → Rockbox Info should show `a49363b515-24bit-261110`.

## Going back
Restore your `.rockbox` backup, or install the full Standard edition package `843986adb6-261110`. This edition does not change the bootloader.

Please report problems with your H2 hardware version, the file format and sample rate, and whether you used wired or Bluetooth output.
