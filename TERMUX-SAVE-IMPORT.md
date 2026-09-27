# Move a Termux guest save into the mobile controller

Android's picker cannot browse Termux's private app storage. Export a COPY into Downloads first. Keep Termux, its old server and original saves until the imported park has been verified across multiple sessions. Do not uninstall Termux or clear its data.

## 1. Stop the old server

Close Jurassic Park Builder. Stop DinoServer in Termux using its normal stop option, or Ctrl+C if it is running in the terminal. Do not export while the server is writing to the save.

## 2. Allow shared-storage access

Run in Termux:

```sh
termux-setup-storage
```

Allow Android's file/storage permission if requested. Then check:

```sh
ls "$HOME/storage/downloads"
```

An empty listing is fine. Permission denied means access is not available yet: check Termux's permissions in Android Settings, reopen Termux and retry. Permission names vary by Android version. Downloads here belongs to the Android device running Termux.

## 3. Locate the correct installation

```sh
find "$HOME" -type d -name "guest_saves" 2>/dev/null
```

If nothing appears, search for guest-save files:

```sh
find "$HOME" -type f -name "D-*.json" 2>/dev/null
```

These commands only search Termux's home directory. If neither finds anything, ask for help locating your server's configured save directory. Do not create an empty save to replace it.

Several results can mean several server installations. Use the installation you actually played on. For the following examples, REPLACE `/actual/path/to/guest_saves` with the full path found above. Keep the quotation marks.

```sh
ls -lht "/actual/path/to/guest_saves"
```

Saves commonly look like `D-0123456789abcdef.json`. Modification time is a clue, not proof of ownership or progress. If several players used the server, export all saves and identify your park before importing.

## 4. Export a backup to Downloads

Run these commands in the same Termux session:

```sh
export_dir="$HOME/storage/downloads/JPB-Termux-Backup-$(date +%Y%m%d-%H%M%S)"
mkdir -p "$export_dir"
cp -R "/actual/path/to/guest_saves" "$export_dir/"
ls -lh "$export_dir/guest_saves"
```

Remember to replace the example source path. The copy command preserves the original folder; it does not move or delete it. If a command reports an error, stop and resolve it before importing. Open Android's file manager and confirm the JSON files exist under Downloads > JPB-Termux-Backup-date-time > guest_saves.

Do not edit the JSON, change device IDs or rename files to match the new device. Keep a second backup on your PC if available. Guest saves may contain device identifiers; do not post them publicly for troubleshooting.

## 5. Move the export to the destination device

**Same Android device:** the new controller can select the exported copy in Downloads.

**Phone to LDPlayer:** copy the backup from your phone to your PC, transfer it into LDPlayer using its shared-folder/file-transfer feature, then use LDPlayer's file manager to put it in the emulator's Downloads folder. Confirm that the JSON is visible there.

Your phone's Downloads, Windows Downloads and LDPlayer's Downloads are separate folders. The controller inside LDPlayer cannot automatically browse a physical phone or Termux's private files.

## 6. Create the current device/save identity

**MUST PLAY GAME ONCE FIRST TO GET DEVICE/SAVE ID.**

1. Keep the old Termux server stopped.
2. Finish the new controller's cache and game connection setup.
3. Start the new controller's server.
4. Launch JPB on the device/emulator you will play on and connect it to this new server.
5. Enter the park once and let it save. A new level-1 park at this step is the destination for your import.
6. Close JPB completely and stop the new server.

If you cannot reach the park, fix the connection first. Do not invent a destination ID. If the existing park already loads correctly and you are not migrating, a fresh import may be unnecessary.

## 7. Import the old JSON

1. Open **Import Guest Save > Check current guest save** in the controller.
2. Use the file selection option, open **Downloads**, then your exported backup folder and **guest_saves**.
3. Select the complete old guest-save **JSON file**. If the picker cannot select a folder, navigate inside it and select the individual JSON.
4. Review the source park and current destination. Do not guess if multiple saves exist.
5. Choose **Back Up & Import** and wait for success. The importer keeps the destination identity and backs up the replaced save.
6. Do not manually overwrite the controller's private save files or copy old ownership/recovery databases over the new installation.

## 8. Verify the result

Start the new server and reopen JPB. Check level, park layout, food, coins, Bucks, dinosaurs and previously unlocked areas. Make a small normal change, let it save, close the game normally and reconnect. Confirm progress persists. Keep the original Termux installation and export until several sessions have worked correctly. Only one server should run at a time.

## Troubleshooting

- **Only Downloads, Images and Recent appear:** expected; choose the exported copy under Downloads. Termux's private directory is not directly accessible.
- **No destination save / play-once warning:** enter the park while connected to the new server, let it save, close the game and stop the server before retrying.
- **Level 1 or missing resources after import:** you may have selected the wrong file or a save that already contained a reset. Stop playing and compare backups. Import cannot reconstruct progress absent from the source.
- **save_file_lock or GUEST-RECOVERY:** close the game and stop both servers. Preserve backups and provide the exact error and import result for support. Do not delete ownership/recovery records to bypass the error.
- **Cannot identify the correct JSON:** export all candidates, retain originals, and ask for help. A recent timestamp alone does not identify your park.
- **Cache import shows Errno 13 under `.cache-stage-...`:** this is a separate cache staging failure inside the controller's private storage, not the Termux save export permission. Do not clear controller data or uninstall it to fix the error. Keep the source cache and save backups and provide the controller version and diagnostic log. A screenshot alone cannot establish the precise permission operation that failed.
