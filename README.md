# Homebrew to KPM

A self-hosted [KPM](https://github.com/KindleModding/KPM) repository porting
jailbroken-Kindle homebrew extensions to the KPM package format.

Index: https://dharmendra-gupta.github.io/kindle-kpm-repo/manifest.json

All packages target `kindlehf` (Kindle Paperwhite 10th gen / firmware 5.18,
`hdnext` stack).

## Packages

| Package | Install | Description |
|---|---|---|
| **Bluetooth Toggle** | `;kpm install bluetooth_toggle` | Enable/Disable Bluetooth (`lipc-set-prop`). For region-locked Kindles that ship with Bluetooth hidden. Author: GreenCat777. |
| **LARK Audiobook Player** | `;kpm install lark` | M4B/MP3 audiobook player with chapters & bookmarks. Audio is Bluetooth-only on this device — enable Bluetooth first. Author: kbarni (GPLv3). |
| **SSH Server (Persistent)** | `;kpm install sshd` | Persistent SSH (port 2222) reusing KOReader's bundled dropbear, launched detached so it survives KOReader closing. Sessions land in `/mnt/us` with a writable `HOME` and `kpm` on PATH. Requires KOReader installed. |
| **Telnet** | `;kpm install telnet` | ⚠️ **Unauthenticated** root shell on port 23, unencrypted. Trusted local networks only. Tap the screen to stop. Author: Foskya. |

## Registering this repo on-device

`;kpm add-repo <url>` does not work from the Kindle search bar (the
`scriptExecutor` bridge rejects any argument containing `:` or `/`). Register
the repo once by inserting a row directly into KPM's local database over USB:

```sh
sqlite3 "/Volumes/<Kindle>/kmc/kpm/kpm.db" \
  "INSERT INTO repositories (id, url, name, description) VALUES ('homebrewtokpm', 'https://dharmendra-gupta.github.io/kindle-kpm-repo/manifest.json', 'Homebrew to KPM', 'Self-hosted KPM repo.');"
```

Then, from the Kindle search bar:

```
;kpm update
;kpm install <package-id>
```
