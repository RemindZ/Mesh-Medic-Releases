# Mesh Medic - Batch 3D Mesh Repair

[![Download Mesh Medic](https://img.shields.io/github/downloads/RemindZ/Mesh-Medic-Releases/total?style=for-the-badge&logo=github&label=Downloads&color=blue)](https://github.com/RemindZ/Mesh-Medic-Releases/releases/latest)
[![Latest Release](https://img.shields.io/github/v/release/RemindZ/Mesh-Medic-Releases?style=for-the-badge&logo=github&label=Latest%20Release&color=green)](https://github.com/RemindZ/Mesh-Medic-Releases/releases/latest)
[![VirusTotal Scan](https://img.shields.io/badge/VirusTotal-Clean-brightgreen?style=for-the-badge&logo=virustotal)](https://www.virustotal.com/gui/file/f2b1ccb852ec2b3e50e6ad19819991c60d7df50a5cef05fd7b8adf8d22ce8815/detection)

A Windows tool that batch-repairs 3D printing STL files using two repair engines: **geometry3Sharp** and **Windows 3D Builder**. Multithreaded, with a multi-step repair pipeline that builds on each step's progress. Files are repaired in-place with automatic backup safety.

> **[Download the latest release here](https://github.com/RemindZ/Mesh-Medic-Releases/releases/latest)**

---

## Quick Start

1. Install [Microsoft 3D Builder](https://apps.microsoft.com/detail/9wzdncrfj3t6) from the Microsoft Store ([alternative download](https://3d-builder.en.uptodown.com/windows))
2. Download `MeshMedic.exe` from [Releases](../../releases)
3. Double-click it, pick a folder, and click **Scan Folders**

You can also use it from the command line:

```
MeshMedic "C:\My Models\Minis"
MeshMedic "C:\Models" --timeout 120
```

Use the built-in **Install** button to add Mesh Medic to your PATH for terminal access anywhere.

---

<p align="center">
  <img src="https://github.com/user-attachments/assets/140a8726-99bb-4b8b-9886-98262ddfae86" width="32%" />
  <img src="https://github.com/user-attachments/assets/7f9c2815-6508-4566-b1a5-6358f3302575" width="32%" />
  <img src="https://github.com/user-attachments/assets/c27fe684-6132-4b07-a8d9-241a3bf8fa21" width="32%" />
</p>

---

## Features

- **Multithreaded** — repairs files in parallel across all CPU cores (configurable)
- **Multi-step pipeline** — geometry3Sharp pre-repair, then 3D Builder. Each step builds on the last
- **Tuned for figurines** — tolerances calibrated for high-res resin printers, preserves thin supports and fine detail
- **Batch repair** — processes entire folders and subfolders of STL files
- **Safe backups** — originals are never lost, even on crash
- **Crash recovery** — resumes interrupted batches on next launch
- **Smart skip** — already-valid files are left untouched
- **3 brand themes** — Remerlinds, Bird, and Henchman with light/dark mode
- **8 languages** — DE, FR, ES, IT, PT-BR, JA, KO, ZH with auto-detection
- **Live thread view** — see what each core is working on in real time

---

## Requirements

- [Microsoft 3D Builder](https://apps.microsoft.com/detail/9wzdncrfj3t6) (app checks on startup)
- Windows 10 (build 19041+)
- .NET 8.0 runtime (included in release)

---

## Privacy

Mesh Medic sends a single anonymous analytics ping on launch (random ID + app version). No file names, no personal data. If the app crashes, you're asked before any report is sent.

---

## Security

This application is unsigned, so some antivirus engines may flag it. A full [VirusTotal scan report](https://www.virustotal.com/gui/file/f2b1ccb852ec2b3e50e6ad19819991c60d7df50a5cef05fd7b8adf8d22ce8815/detection) is available for transparency.

---

*With love by [remerlinds.com](https://remerlinds.com)*
