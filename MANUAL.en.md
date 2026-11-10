# WalkerFans H2 Bluetooth — Quick Manual

> **Important — based on HIFIWALKER original firmware V2.3.** This build was developed and tested on an H2 running the original HIFIWALKER firmware **V2.3**. Other firmware versions have not been tested and may not be compatible. If your player runs a different version, back up first and upgrade at your own risk.

Version `843986adb6-261110`. Bluetooth is for **H2 hardware revision 4 (original V1.9–V2.3)**. This ZIP updates an existing erosqnative Rockbox installation; it is not a factory update.upt. Establish the correct Rockbox bootloader first. New-flash V2.3 units require a matching HW4 bootloader dated 2026-02-03 or later.

Back up the entire `.rockbox` directory, including config.cfg and bt_config.conf. Pairing records contain link keys: never publish them. Extract the ZIP and merge its `.rockbox` directory directly into the card root, replacing program files without nesting an extra folder. Verify files, safely eject, unplug and reboot. Confirm `843986adb6-261110` in system information.

Put the headphones into pairing mode. Settings → Bluetooth Settings → Devices, select the device and press Play. Follow any pairing-code prompt. Compatibility depends on the headphones. Disconnect competing phones and try SBC if connection/audio fails. Enable Debug Logging only while reproducing a problem, and redact sensitive records before sharing.

Default UI: 20-NotoSansSC; additional sizes 16/18/22/24 and the Rockbox font pack are included. Menu status icons are 20 px with a 10 px top margin. Use 16-GNU-Unifont if the default font lacks your script. Translation improvements still need native-speaker review.

Audio limitations: DSD64/128/256 DSF/uncompressed DFF have software decoding to PCM; no native DSD/DoP output is claimed. DSD host tests are not H2 real-time performance tests. The current DSP/mixer output is 16-bit PCM. Wired sampling support tops out at 192 kHz subject to settings. Bluetooth uses lossy negotiated codecs, not native high-resolution file passthrough; no codec certification or broad device acceptance is claimed.

Rollback by restoring the backed-up `.rockbox` folder. Factory recovery requires a matching original firmware package; WalkerFans H2 Tools currently bundles V2.3 only. For failure reports, provide versions, headphone model and reproduction steps, but remove pairing keys, addresses and private logs.

Publishing and documentation: **WalkerFans Team**. Preserve upstream authors and component license notices. This is a development pre-release. The origin and redistribution terms of the Bluetooth controller firmware have not been verified.

Non-commercial community project by WalkerFans Team. If any content involves a copyright or patent we are not aware of, contact walkerfans007@gmail.com and we will remove it.
