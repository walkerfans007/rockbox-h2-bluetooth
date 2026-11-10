# WalkerFans H2 Rockbox Bluetooth — Standard edition

> **Important — based on HIFIWALKER original firmware V2.3.** Developed and tested on an H2 running the original HIFIWALKER firmware **V2.3**. Other firmware versions have not been tested and may not be compatible. Back up first and upgrade at your own risk.

**Version:** `843986adb6-261110` · **Branch:** `h2-bluetooth` · **Audio path:** 16-bit (unchanged from upstream)
**Status:** pre-release, installed and running on the development H2
**Package:** `rockbox-h2bt-843986adb6-261110.zip` (518 files)
**SHA-256:** `2c8b837fe7b7215aca4a29f656a889dc63f5d0bff51f8adc43e32a36bf51b342`

This is the recommended edition for everyday use. It adds Chinese-capable fonts, corrected translations, a larger status bar and more robust Bluetooth start-up on top of the upstream Bluetooth branch. **It does not change audio processing:** music is processed and output at 16 bits, exactly as upstream.

## Based on

| Layer | Source | Revision |
|---|---|---|
| Rockbox | https://github.com/Rockbox/rockbox (master) | `baa2b4564b` (2026-10-26) |
| Bluetooth for H2 | https://github.com/BlackIsBlack/rockbox-h2-bluetooth (`h2-bluetooth`) | up to `3dba828a46` (2026-10-19), replayed on the Rockbox revision above |

Everything in the "Inherited" section below is upstream work. Everything in "Changed by WalkerFans" is new in this release.

## Changed by WalkerFans

### Bluetooth robustness (`ab8ef9b67a`, `032e9da63d`)
- The Bluetooth UART now gives up after 1 second instead of waiting forever when the controller is missing or holds the line; start-up fails cleanly instead of freezing the player.
- A corrupted or oversized Bluetooth packet no longer crashes the player (previously a panic). The driver drops bytes until the line is quiet and resynchronises; after 16 bad packets in a row it stops the Bluetooth thread.
- H2 units older than hardware revision 4 now show "Bluetooth not supported on this hardware" and the firmware does not touch the radio.
- If the controller does not answer, the message now says so plainly instead of "failed to start (controller -1)".
- `bt_log.txt` records memory use and UART error counters every time Bluetooth is turned on or off, for leak and long-play testing.

### Fonts (`c62ccdd37a`)
- New default UI font: **Noto Sans SC, 20 px** (version 2.004, SIL Open Font License 1.1). The previous default (15 px Adobe Helvetica) had no Chinese or Japanese glyphs, so those menus showed boxes.
- Also included: Noto Sans SC at 16, 18, 22 and 24 px, and the full Rockbox font pack.
- The built-in cabbiev2 theme (320×240) uses the new font; its playback-screen time row uses the 16 px size so it fits.
- Not covered by Noto Sans SC: Korean (Hangul), Arabic, Hebrew, Thai and Latin Extended-A. Choose another font from the pack for those.

### Translations (`6420304039`, `08aabaf999`)
- **Simplified Chinese:** 61 mistranslations corrected; stray Traditional characters removed.
- **Traditional Chinese:** regenerated from the corrected Simplified Chinese and adapted to Taiwan UI wording (檔案, 設定, 選單, 外掛程式, 播放清單…). About 440 missing strings were added and about 350 strings that were still in English were translated; machine-translation errors were removed.
- **Japanese:** 53 missing strings added (Database menu).
- **French:** 13 missing strings added; one plural form fixed.
- **Bluetooth strings** translated into Simplified Chinese, Traditional Chinese, Japanese, German, French, Spanish and Italian.
- None of these translations has been reviewed by a native speaker yet.

### Status bar (`d45cc7400a`, `843986adb6`)
- Menu screens use a new status bar with **20 px icons, starting 10 px from the top edge**; menu content starts below it. The bar is on by default for this target.
- The playback screen keeps its existing layout.
- Packaging fix so the status-bar images are always included, and a check that the final package contains all 518 expected files.

### Build (`26c0d83538`, `4f43ea84ce`, `eb074ab280`, `5c0c1107cd`)
- `tools/h2bt/build.sh` builds the complete SD-card package from source with pinned tool and font versions.
- Build timestamps are pinned and nested archives repacked, so two builds of the same commit produce byte-identical packages.
- macOS build support (GNU `date` mapping, font converter built locally).

## Inherited from upstream (not changed in this release)
- Bluetooth audio for H2 hardware revision 4 (Bluedroid stack ported from ESP-IDF 6.1).
- Codecs: SBC (with automatic bitpool back-off), aptX, aptX HD, LDAC.
- Bluetooth settings menu, quick toggle, device list with headphone battery, pairing codes, switching between devices, taking over busy headphones, Nest speaker support.
- AVRCP play status and controls, volume sync, pause when headphones disconnect, automatic power-off.
- One fixed sample rate per connection (44.1 kHz preferred) to avoid dropouts.

## Audio specifications (unchanged from upstream)

| Item | This edition |
|---|---|
| Internal processing and wired output | **16-bit PCM** |
| Wired sample-rate limit | 192 kHz |
| FLAC | up to 24-bit / 192 kHz input; reduced to 16-bit for output |
| WAV | integer PCM up to 32-bit, float up to 64-bit input; reduced to 16-bit for output |
| DSD (DSF, uncompressed DFF) | DSD64 / 128 / 256 converted in software to 44.1 / 88.2 / 176.4 kHz PCM; no native DSD or DoP |
| Bluetooth | always re-encoded (lossy) as SBC, aptX, aptX HD or LDAC, depending on the headphones |

Files with more than 16 bits play correctly, but their extra resolution is not kept. For 24-bit wired output, see the separate **24-bit experimental edition**.

## Validation
- Done: package contents and every file written to the card verified on the development H2; the player runs this build. DSD decoding tested on a computer.
- Not done: broad headphone testing, long-play stability, analog measurements, DSD256 performance on the H2.

## Requirements and install
- Bluetooth requires H2 **hardware revision 4** (original V1.9–V2.3); older revisions show a "not supported" message.
- This ZIP updates an existing Rockbox installation; it is not a factory `update.upt`. Install the correct Rockbox bootloader first.
- Back up the whole `.rockbox` folder (including `config.cfg` and `bt_config.conf`). Pairing records contain link keys: never publish them.
- Extract the ZIP to the card root so its `.rockbox` folder replaces the old one. Do not mix files from the 24-bit edition.
- After reboot, System → Rockbox Info should show `843986adb6-261110`.
