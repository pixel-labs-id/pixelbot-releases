# 🚀 PixelBot Releases Repository

Official binary and update release distribution repository for **PixelBot** (`pixel-labs-id/pixel-bot`).

This repository hosts official production builds, release notes, and assets consumed directly by PixelBot's built-in **In-App Auto-Updater** across macOS and Windows.

---

## 📦 Release Asset Specifications

For the In-App Updater to automatically detect, download, and verify binary releases, every GitHub Release in this repository adheres to the following naming format:

| Operating System | Architecture | Asset File Name | Type | Notes |
|---|---|---|---|---|
| **macOS** | Apple Silicon (M1/M2/M3/M4) | `PixelBot-<version>-macOS-AppleSilicon.zip` | ZIP Archive | Contains `PixelBot.app` with embedded dylibs |
| **macOS** | Intel (x86_64) | `PixelBot-<version>-macOS-Intel.zip` | ZIP Archive | Contains `PixelBot.app` with embedded dylibs |
| **macOS** | Manual Installer | `PixelBot-<version>-macOS-AppleSilicon.dmg` | Disk Image | For fresh clean manual installations |
| **macOS** | Manual Installer | `PixelBot-<version>-macOS-Intel.dmg` | Disk Image | For fresh clean manual installations |
| **Windows** | Setup Wizard Installer | `PixelBot-<version>-Windows-Setup-x64.exe` | NSIS Installer | Full desktop setup with Start Menu & Desktop shortcuts |
| **Windows** | In-App / Portable Update | `PixelBot-<version>-Windows-x64.zip` | ZIP Archive | Contains `PixelBot.exe` + `lib/` directory |
| **Windows** | Standalone Executable | `PixelBot-<version>-Windows-x64.exe` | Executable | Standalone single binary |
| **All Platforms** | Integrity Manifest | `checksums.txt` | Text / SHA-256 | SHA-256 hash digests for all assets above |

---

## 🔒 Security & Integrity Verification

Every release includes a `checksums.txt` file containing SHA-256 checksums generated during packaging:

```bash
# Example verification:
shasum -a 256 -c checksums.txt
```

PixelBot's in-app updater automatically downloads `checksums.txt`, parses the SHA-256 digest matching the target platform asset, and validates the downloaded stream before extracting or launching.

---

## 🛠️ Publishing a Release from `pixel-bot`

From the main `pixel-bot` source directory:

```bash
# 1. Package release archives, NSIS installer, and calculate checksums
make package-releases

# 2. Publish to GitHub Releases using GitHub CLI
gh release create v1.19.2 dist/PixelBot-* dist/checksums.txt \
  --repo pixel-labs-id/pixelbot-releases \
  --title "PixelBot v1.19.2" \
  --notes "### What's New in v1.19.2..."
```

---

© Pixel Labs ID. All rights reserved.
