# JPB DinoServer Mobile Controller

Android controller downloads and future updates are hosted in this repository, separate from the Windows server releases.

[Download Controller 0.8.23](https://github.com/discordsussy12345-cpu/JPB-DinoServer-Controller/releases/tag/v0.8.23) · [Installation and migration](MOBILE-INSTRUCTIONS.md)

## Read before installing

**This is a separate app, not an in-place update of the old controller.** It uses a new signing key and application ID `org.jpb.dinoserver.controller`, with launcher name **JPB DinoServer Controller (New)**. It can coexist with the older `org.jpb.dinoserver` controller. Keep the old app installed: uninstalling or clearing its storage erases its private saves and cache. The new app cannot automatically read them.

Stop the old server before starting the new one. Import the cache and an accessible guest-save backup into the new app, then verify the park before switching over. If your only save is trapped in the old app's private storage, keep using it until you can obtain a safe export; do not uninstall it.

## Included in 0.8.23

- Indominus in the surface offer pool, following the existing schedule.
- Guided guest-save import from an old folder or JSON, current-save checking and automatic backups. **MUST PLAY GAME ONCE FIRST TO GET DEVICE/SAVE ID.**
- GitHub update checks, download progress, SHA-256 and signing-certificate verification, and Android-confirmed installation. Updates are never silently installed.
- Server setup help for same-Android localhost connections and Windows-hosted LDPlayer/phone connections, including firewall troubleshooting.

The first installation is manual. Future versions of this new app can update in place using the same application ID and signing key. Its feed is [android-controller-update.json](android-controller-update.json).

Android 7.0+ (API 24); ARMv7, ARM64, x86 and x86_64. The game APK and Android cache are separate downloads. Optional soundtrack audio was absent from the handoff and is not included. New help text is English. Build, automated tests and lint checks passed; physical-device installation/upgrade testing remains pending.

Save resets, XP stalls and battle timers remain under investigation. This release does not claim to fix those issues.

Download the APK under release **Assets**, not GitHub's generated Source code archive. Signing keys and player data are never included in this repository.

## Moving a guest save from Termux

Follow the [detailed Termux export and controller import guide](TERMUX-SAVE-IMPORT.md). It covers storage permissions, locating saves, exporting to Downloads, LDPlayer transfers, the play-once checker, and verification. Keep the original installation and backups.
