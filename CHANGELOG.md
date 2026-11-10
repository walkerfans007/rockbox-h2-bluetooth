# Changes — WalkerFans H2 Bluetooth

## 843986adb6-261110
- Added 20-pixel menu status icons with a 10-pixel top margin; moved menu content below the bar.
- Fixed status asset inclusion for quoted build model names; validated the final 518-file package.
- Regenerated Traditional Chinese from the corrected Simplified Chinese with Taiwan UI wording.
- Corrected Chinese strings, added missing Japanese/French phrases, translated Bluetooth strings in seven languages.
- Added default 20-pixel Noto Sans SC UI fonts and alternative sizes; included the Rockbox font pack.
- Made build/package output reproducible, pinned build timestamps/dependencies and included convttf setup.
- Added bounded UART waits, malformed-packet recovery and clearer messages for unsupported/silent Bluetooth hardware.

The Bluetooth stack, codecs, pairing/reconnection and controls come from the credited upstream Bluetooth branch (BlackIsBlack); this release builds on that work.

Validation: package contents and delivered files verified on the development H2; host DSD decoder checks completed. Broad headphone testing, long-play stability, analog measurements, 24-bit output and H2 DSD256 performance are not completed.
