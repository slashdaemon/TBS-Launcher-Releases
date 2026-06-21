# TBS Launcher — First-run setup

This guide takes a fresh device to **in-world on the TBS server with capture working**.
The APK is only the launcher + capture bridge; everything else is installed on first run.

**Target device:** XREAL Beam Pro 5G (Android 14), or any `arm64-v8a` Android 8+ device.
**You need:** a Microsoft account that **owns Minecraft: Java Edition**.

---

## 1. Install the launcher

1. Download `TBSLauncher-<ver>-arm64-v8a.apk` from the release.
2. On the device, allow "install unknown apps" for your file manager / browser, then open
   the APK to install.
   - Or over ADB: `adb install -r TBSLauncher-<ver>-arm64-v8a.apk`
3. Launch **TBS Launcher**. It installs alongside stock ZalithLauncher (distinct package
   `as.papp.tbs.launcher.v2`). You'll see the **"Unofficial Modified Versions"** notice on
   startup — expected.

## 2. Sign in to Microsoft

In the launcher, add/sign in with the Microsoft account that owns MC Java. This is required
to launch online and to connect to the server.

## 3. Install the Java 25 runtime

Install the bundled **JRE 25** runtime when prompted (Settings → Runtimes if not auto-prompted).
MC 26.1.2 requires Java 25.

## 4. Install Minecraft 26.1.2 + Fabric + Fabric API

1. Create/install a **Minecraft 26.1.2** instance.
2. Install the **Fabric** loader for 26.1.2.
3. Install **Fabric API** (matching 26.1.2) into that instance's mods.

> Use the version that matches the live TBS server. At time of this release the server runs
> the **26.1.2** line.

## 5. Sideload the StreamCraft mod

The StreamCraft client mod is **not** on a public mod index (it carries a custom
Android-aarch64 LiveKit native), so you add it by hand:

1. Download `streamcraft-<ver>-android-aarch64.jar` from the release.
2. Copy it into your 26.1.2 instance's **`mods/`** folder, alongside Fabric API.
   - In the launcher: instance → manage mods → import/add, select the jar.
   - Or via files: `…/.minecraft/<instance>/mods/streamcraft-<ver>-android-aarch64.jar`
3. **Use only this `-android-aarch64` jar.** The desktop StreamCraft jars (linux/macos/windows)
   do not contain the Android native and will fail to initialize LiveKit on-device.

> Match the mod version to the server's StreamCraft version. If voice/video won't connect,
> a client/server StreamCraft protocol mismatch is the first thing to check.

## 6. Grant Android permissions

So the capture bridge can publish from the device, grant the TBS Launcher app:
**Camera**, **Microphone**, and (for screen-share) accept the **screen-capture / cast**
consent prompt when you start it. Android 14 shows a foreground-service notification while
screen-sharing.

## 7. Add the server and play

1. Launch the 26.1.2 + Fabric instance.
2. Add a server: **`theblocksurvival.com`** (Minecraft: Java Edition).
3. Join. StreamCraft handshakes during connect; you should see voice signaling come up.

## 8. Use capture in-game

Open the **StreamCraft menu** in-world:
- **Voice** is automatic once connected (mic + playback via the device).
- **Camera** → publishes the device webcam as a video track.
- **Share Screen** → grant the cast prompt → publishes the device screen.

A remote track only renders in-world when another participant is publishing on the room.

---

## Troubleshooting

- **"Unofficial Modified Versions" on every launch** — expected; required by the GPL fork terms.
- **Login fails / can't go online** — confirm the Microsoft account owns MC Java.
- **LiveKit / capture won't initialize** — confirm you installed the **`-android-aarch64`**
  StreamCraft jar (not a desktop one) and that Camera/Mic permissions are granted.
- **No voice audio** — the device audio shim handles mic + playback; make sure Microphone is
  granted and the StreamCraft voice relay authenticated (check the in-game/log status).
- **Connected but no video from others** — nobody is publishing on the room; that's normal.

## Status (this release line)

- ✅ Boots Java 25 + MC 26.1.2 + Fabric + StreamCraft on-device; Microsoft login; server
  connect + voice signaling; LiveKit FFI initializes (receive path).
- ⏳ Two-way voice, webcam broadcast, and screen-share are **built**; verify on your device.

See the launcher source for full phase notes:
https://github.com/slashdaemon/ZalithLauncher2 (branch `tbs-2.4.8`).
