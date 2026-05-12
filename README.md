# My Orphies

A personal AI desktop assistant for macOS. This repo only hosts the release binaries — it does not contain source code.

## Download

Grab the latest `.dmg` from the [Releases page](https://github.com/joyzhang14-14/My-App-Release/releases/latest).

Pick the file named `My-Orphies_<version>_aarch64.dmg` (Apple Silicon — M1 / M2 / M3 / M4).

> The other files in the release (`*.app.tar.gz`, `latest.json`) are used by the in-app auto-updater. You only need the `.dmg` for the first install.

## Install (first time only)

My Orphies is signed but **not notarized by Apple**. macOS Gatekeeper will block the first launch with a "cannot be verified" warning. This is expected — follow the steps below to bypass it once. Future updates download silently in the background.

### Step 1 — Mount the DMG and copy the app

1. Double-click the downloaded `.dmg` to mount it.
2. Drag **My Orphies** into the **Applications** folder.
3. Eject the disk image (right-click on the mounted volume → Eject).

### Step 2 — Tell macOS to trust the app

Open **Terminal** (press `⌘+Space`, type `Terminal`, Enter), then paste this command and press Enter:

```bash
xattr -cr "/Applications/My Orphies.app"
```

This clears the `com.apple.quarantine` flag that macOS stamps on anything downloaded from the internet. You only have to do this once — auto-updates afterwards are signed with the app's own minisign key and don't need this step.

### Step 3 — Launch and grant permissions

Open My Orphies from Launchpad or `/Applications`. On first launch the app will ask for several macOS permissions:

- **Screen Recording** — for the screen capture / OCR pipeline
- **Microphone** — for meeting audio transcription
- **Calendar** — for upcoming-meeting awareness (via Automation)
- **Spotify Automation** (only if you connect Spotify) — for local lyric display
- **Full Disk Access** (optional) — only if you connect Voice Memos

Each permission triggers a native macOS dialog. Approve the ones you want and you're set.

## Updating

Once installed, My Orphies handles updates itself: it checks this repo's `latest.json`, downloads the new `.app.tar.gz`, verifies the minisign signature, and restarts. You don't need to repeat any of the steps above.

## Troubleshooting

**"App is damaged and can't be opened"**
Re-run Step 2. If the warning persists, also try opening **System Settings → Privacy & Security**, scroll to the bottom, and click **Open Anyway** next to the My Orphies message.

**Auto-update isn't picking up a new release**
Quit and relaunch the app. It checks on startup, then every few hours.

**Want to fully uninstall**
Drag `/Applications/My Orphies.app` to the Trash, then delete `~/.screenpipe/` (the local data directory).
