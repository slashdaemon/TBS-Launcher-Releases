# TBS Launcher — Releases

Sideloaded Android builds of the **TBS Launcher**: a fork of
[ZalithLauncher2](https://github.com/ZalithLauncher/ZalithLauncher2) that boots a desktop
JVM on-device and launches **Minecraft 26.1.2 + Fabric + the StreamCraft client mod**,
connecting to the TBS server as a *client* — with **webcam / screen-share / voice capture
from the Android device** bridged into the game.

**Target hardware:** XREAL Beam Pro 5G (Android 14, Snapdragon 6 Gen 1 / Adreno 710, 8 GB),
`arm64-v8a`.

> ⚠️ **Unofficial Modified Version.** Not affiliated with Mojang, Microsoft, or the
> ZalithLauncher project. Does **not** bundle Minecraft — the game client is downloaded from
> Mojang at runtime and requires you to own Minecraft: Java Edition.

## Downloads

Grab the latest from **[Releases](../../releases/latest)**. Each release attaches:

| Asset | What it is |
|---|---|
| `TBSLauncher-<ver>-arm64-v8a.apk` | The launcher APK (arm64-v8a only, release-signed). Sideload this. |
| `streamcraft-<ver>-android-aarch64.jar` | The StreamCraft client mod with the custom Android-aarch64 software-codec LiveKit native. **Not bundled in the APK** — you sideload it into the game instance (see SETUP). |
| `SETUP.md` | Step-by-step first-run setup. |

## What's in the APK (and what isn't)

The APK is a rebranded ZalithLauncher2 plus the **TBS capture bridge** (host-side
camera / screen / mic → local IPC → the StreamCraft mod inside the embedded JVM). It does
**not** bundle the Minecraft client, the Java runtime, Fabric, the StreamCraft mod, or any
server configuration — those are installed/sideloaded on first run. See **[SETUP.md](SETUP.md)**.

## Source & license

The launcher is **GPL-3.0** (inherited from ZalithLauncher2). Per those terms this is a
renamed, source-published fork that displays *"Unofficial Modified Versions"* on startup.

- Launcher source: **https://github.com/slashdaemon/ZalithLauncher2** (branch `main`)
- Upstream: https://github.com/ZalithLauncher/ZalithLauncher2

The StreamCraft Android native (`liblivekit_ffi.so` inside the mod jar) is a custom
software-codec build of [livekit/rust-sdks](https://github.com/livekit/rust-sdks)
`livekit-ffi/v0.12.48`; build provenance + patch are documented inside the jar at
`natives/android-aarch64/README.md`.
