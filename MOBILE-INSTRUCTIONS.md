# Mobile controller installation and migration

## Install the new controller

1. Keep the old controller installed and preserve its data. Obtain a complete guest-save JSON backup before changing which server you play on. The new controller cannot read another app's private files.
2. Close JPB and stop the old controller's server. Both apps use the same local ports and must not run their servers together.
3. Download `JPB-Controller-v0.8.23.apk` from [release Assets](https://github.com/discordsussy12345-cpu/JPB-DinoServer-Controller/releases/tag/v0.8.23). Install it through Android; allow installation from your download app if Android asks.
4. Open **JPB DinoServer Controller (New)**. This has a separate app ID and separate storage. It does not replace the old app.
5. Import the Android cache ZIP or extracted cache folder using the controller's cache controls. You need a copy accessible through Android's file picker; the old app's private cache is not shared automatically.
6. Use the matching JPB localhost game APK. Start this controller's server and wait for SERVER RUNNING, then open the game. No Termux, Python installation or Windows EXE is needed.

Do not uninstall or clear the old controller to resolve an installation problem. If there is no accessible backup of your park, keep using the old app until a safe export is available.

## Import your park

**MUST PLAY GAME ONCE FIRST TO GET DEVICE/SAVE ID.**

1. With only the new server running, enter JPB as a guest once so the new controller records the destination save identity.
2. Let it save, close JPB completely and stop the server.
3. Open **Import Guest Save > Check current guest save**.
4. Select an accessible old server folder or complete guest-save JSON. If several candidates are shown, choose the correct park. The Android picker cannot directly browse a Windows C: drive; transfer the backup to Android storage first.
5. Review the source and current destination, then use **Back Up & Import**. The importer retains the current device binding and backs up the replaced save. Do not manually rename saves or delete recovery databases.
6. Start the new server, open JPB and check level, Bucks, food, dinosaurs and all previously unlocked areas. Make a small normal change, let it save and reconnect to verify persistence.
7. Keep the original app and backup until recovery is verified. Only one server should be running at a time.

Import requires an actual complete save. It cannot reconstruct missing profile/resources, repair every corrupted save or recover private data from the old controller automatically.

## Indominus offers

Indominus is in the surface add-on pool. Offers follow the existing schedule, so it may not be selected immediately. A one-time migration adds it to an existing nonempty pool inside this new app, preserving other settings and backing up the original configuration. Empty/disabled pools and later custom removal are respected. This does not migrate the old app's private configuration.

## Connecting to the server

**Server running inside the same Android device or emulator:** start it in this controller, then open `http://127.0.0.1:9943/status/2.0/` in that Android browser. Use HTTP, not HTTPS. The matching localhost APK connects to this server. Windows firewall changes are not needed for this setup. If no response arrives, check controller Diagnostics, startup errors, cache setup and whether another server app is running. Local ports are 8080, 9943 and 9933.

**Server running on a Windows PC instead:** stop this controller's embedded server. Route the game to the PC's LAN IP, not localhost. Compare `http://PC-LAN-IP:9943/status/2.0/` in both Windows and the emulator browser. A response containing `"status":true` confirms basic HTTP connectivity, not complete game login.

If Windows responds but Android/LDPlayer does not:

1. On Windows, press **Win + R**, enter `wf.msc`, then press Enter.
2. Select **Inbound Rules > New Rule > Port > TCP**.
3. Enter **80,9943,9933** under Specific local ports.
4. Choose **Allow the connection** and the active network profile. Use Private for a trusted home network; a Private-only rule does not apply when that connection is classified Public.
5. Name it **DinoServer TCP**, finish, and retry. Keep Windows Firewall enabled.
6. If LDPlayer alone still hangs, try **Settings > Network > Network Bridging**, install its bridge driver if requested, choose the active PC network adapter and **DHCP**, save and restart LDPlayer. Keep game hosts pointed at the PC's IP. Do not assign that IP to the emulator. Bridging is an option to investigate, not a guaranteed fix.

No router port forwarding is needed for a same-PC emulator or same-home-network connection. If status works but the game fails, check routing and TCP 9933 access and capture a fresh login log. Do not delete saves to fix a network timeout.

References: [Microsoft firewall guidance](https://support.microsoft.com/en-us/windows/security/firewall/risks-of-allowing-apps-through-windows-firewall), [LDPlayer bridging guide](https://www.ldplayer.net/support/how-to-set-up-network-bridging-on-the-android-emulator-ldplayer.html), [complete Windows server guide](https://github.com/discordsussy12345-cpu/JPB-DinoServer-Downloads/blob/main/WINDOWS-INSTRUCTIONS.md).

## Future controller updates

The new controller checks this repository automatically (at most once every six hours when opened), or through **Controller updates**. Download when offered, then close JPB and stop the server before verifying and installing. Android asks you to confirm installation and may ask you to allow installs from this controller. Updates require a matching app ID, newer version, valid checksum and the same signing key. They preserve this new app's storage during an in-place installation. Do not uninstall or clear storage between updates.

Automatic checks can be disabled in the Updates screen. The older controller does not receive this new app through its updater.

## Moving a guest save from Termux

Follow the [detailed Termux export and controller import guide](TERMUX-SAVE-IMPORT.md). It covers storage permissions, locating saves, exporting to Downloads, LDPlayer transfers, the play-once checker, and verification. Keep the original installation and backups.
