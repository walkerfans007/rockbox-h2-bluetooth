# Changes — WalkerFans H2 Bluetooth

## a49363b515-24bit-261110 — 24-bit experimental edition
- Separate edition built from the Standard edition plus two commits (`0855be3ef4`, `a49363b515`).
- Wired audio path keeps 24-bit precision (DSP, buffer, crossfade, mixer, software volume, I2S output).
- Voice, beeps, USB audio and plugins stay 16-bit; Bluetooth is converted to 16-bit before the encoder.
- Not yet audio-validated on hardware. Full details: [CHANGES-a49363b515-24bit-experimental.md](CHANGES-a49363b515-24bit-experimental.md).

## 843986adb6-261110 — Standard edition (recommended)
Full details: [CHANGES-843986adb6-standard.md](CHANGES-843986adb6-standard.md).
- Added 20-pixel menu status icons with a 10-pixel top margin; moved menu content below the bar.
- Fixed status asset inclusion for quoted build model names; validated the final 518-file package.
- Regenerated Traditional Chinese from the corrected Simplified Chinese with Taiwan UI wording.
- Corrected Chinese strings, added missing Japanese/French phrases, translated Bluetooth strings in seven languages.
- Added default 20-pixel Noto Sans SC UI fonts and alternative sizes; included the Rockbox font pack.
- Made build/package output reproducible, pinned build timestamps/dependencies and included convttf setup.
- Added bounded UART waits, malformed-packet recovery and clearer messages for unsupported/silent Bluetooth hardware.

The Bluetooth stack, codecs, pairing/reconnection and controls come from the credited upstream Bluetooth branch (BlackIsBlack); this release builds on that work.

Validation: package contents and delivered files verified on the development H2; host DSD decoder checks completed. Broad headphone testing, long-play stability, analog measurements, 24-bit output and H2 DSD256 performance are not completed.
