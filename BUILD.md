# Build the WalkerFans H2 Bluetooth revision

`Walkerfans-H2BT-source-843986adb6-261110.tar.gz` is the complete source of revision `843986adb6`, including `tools/h2bt/build.sh`.

The build script reads its version string from Git, so put the snapshot in a Git repository first:

```sh
tar xzf Walkerfans-H2BT-source-843986adb6-261110.tar.gz
cd Walkerfans-H2BT-source
git init -q && git add -A && git commit -qm "WalkerFans H2BT 843986adb6 source"
tools/h2bt/build.sh ./release-out
```

The code is the same as the published build. The version label in your build will show your local commit ID instead of `843986adb6`, so the ZIP checksum will differ from the published one.

Build host: macOS on Apple Silicon, or Linux. The script downloads a pinned toolchain and fonts and verifies their SHA-256; the first toolchain build takes much longer than later builds. See `docs/H2BT-WALKERFANS` in the source for branch notes.
