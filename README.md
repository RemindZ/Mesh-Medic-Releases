# Mesh Medic

**Batch-repair STL and OBJ files for 3D printing, instead of fixing them one at a time.**

[![Download Mesh Medic](https://img.shields.io/github/downloads/RemindZ/Mesh-Medic-Releases/total?style=for-the-badge&logo=github&label=Downloads&color=blue)](https://github.com/RemindZ/Mesh-Medic-Releases/releases/latest)
[![Latest Release](https://img.shields.io/github/v/release/RemindZ/Mesh-Medic-Releases?style=for-the-badge&logo=github&label=Latest%20Release&color=green)](https://github.com/RemindZ/Mesh-Medic-Releases/releases/latest)
[![VirusTotal Scan](https://img.shields.io/badge/VirusTotal-Clean-brightgreen?style=for-the-badge&logo=virustotal)](https://www.virustotal.com/gui/file/f2b1ccb852ec2b3e50e6ad19819991c60d7df50a5cef05fd7b8adf8d22ce8815/detection)

<!-- The VirusTotal badge above and the link in the Security section are pinned to the
     v2.3.0 file hash. Update both when publishing a new release. -->


Point it at a folder. It finds every STL and OBJ inside, leaves the healthy ones alone,
and repairs the rest across all your CPU cores. Two engines do the work: geometry3Sharp
for speed, and the Windows 3D Builder engine for the stubborn ones.

> ### **[Download the latest release](https://github.com/RemindZ/Mesh-Medic-Releases/releases/latest)**

<!-- SCREENSHOT SLOT: hero shot, full width -->

---

## Why you'd want it

You download a model and your slicer refuses to touch it. Or it slices fine and the print
comes out with a hole in the side, or a wall that just isn't there.

That's usually broken geometry: holes, flipped normals, self-intersections, duplicate
vertices. 3D Builder does fix it, but one file at a time, by hand, and a kit can be forty
files. If you have ever sat there opening and re-saving STLs one by one, this is that job,
automated.

---

## Quick start

1. Install [Microsoft 3D Builder](https://apps.microsoft.com/detail/9wzdncrfj3t6) from the
   Microsoft Store ([alternative download](https://3d-builder.en.uptodown.com/windows))
2. Download the latest `.zip` from
   [Releases](https://github.com/RemindZ/Mesh-Medic-Releases/releases/latest)
3. Extract `MeshMedic.exe`, double-click it, pick a folder, and hit **Scan Folders**

No installer, no account, no config file.

<p align="center">
  <img src="https://github.com/user-attachments/assets/c2354b80-2c20-4320-9611-fe5fb590799a" width="32%" />
  <img src="https://github.com/user-attachments/assets/35c72aed-652d-4ba4-8fa5-cf9fba10d28a" width="32%" />
  <img src="https://github.com/user-attachments/assets/04d800ce-9f9a-46cf-937a-76c93333dd19" width="32%" />
</p>

---

## What it does

### Fixes things

- **Two engines, in order.** geometry3Sharp goes first because it is fast. Anything it
  cannot fix cleanly gets handed to the Windows 3D Builder engine, Quick Fix and then
  Full Fix.
- **Scale-aware.** Tolerances come from each mesh's own coordinate scale, so thin supports
  and fine detail survive instead of being smoothed away.
- **Skips what is already fine.** Healthy files are left untouched, not re-saved.
- **Whole folders**, subfolders included.

### Does not lose your files

- **Repairs are transactional.** Every engine writes to a staging file that gets validated
  before it replaces your original. If the check fails, your file stays exactly as it was.
- **Never silently overwrites.** A converted output will not clobber a file already
  sitting at the destination.
- **Survives a crash.** Interrupted batches pick up where they left off on next launch,
  and a leftover backup gets restored.

### Handles your formats

- **Output modes.** Automatic keeps the source extension, or force `.stl` or `.obj` and
  get sibling converted files.
- **OBJ preservation.** `mtllib`, material scopes, `.mtl` files, and relative texture
  sidecars are kept where possible. Worth knowing: repaired or rebuilt topology can lose
  exact UV mapping.

### Shows its work

- **Multithreaded** across as many cores as you want to give it.
- **Live thread view**, so you can watch which file each core is chewing on in real time.

### Looks how you like

- **Three themes** (Remerlinds, Bird, Henchman), each with light and dark mode, all
  meeting WCAG AA contrast.
- **Nine languages.** English plus DE, FR, ES, IT, PT-BR, JA, KO and ZH, auto-detected
  from your system.

---

## From the command line

```
MeshMedic "C:\My Models\Minis"
MeshMedic "C:\Models" --timeout 120
MeshMedic "C:\Models" --output-format obj
```

`--output-format` takes `auto`, `stl`, or `obj`. `--timeout` is per file, in seconds. The
in-app **Install** button adds Mesh Medic to your PATH so you can call it from any
terminal.

---

## Requirements

- Windows 10 build 19041 or newer
- [Microsoft 3D Builder](https://apps.microsoft.com/detail/9wzdncrfj3t6), which the app
  checks for on startup
- .NET 8.0 runtime, already bundled in the release

---

## Something broken? Missing a feature?

Hit the **shield button in the top right** of the app to open the feedback panel. Bug
reports, feature requests, "this bit is confusing", it all comes straight to us and it is
the fastest way to get something onto the list. We read every one.

---

## Privacy

On launch, Mesh Medic sends a persistent randomly generated client ID and the app version
for basic usage counts. Cloudflare receives the source IP and uses it for per-IP rate
limiting.

Diagnostic and crash payloads contain no model names, no file paths, and no arbitrary
exception text. Crash metadata is sent only after you opt in. Feedback includes the text
you chose to submit, and nothing you did not.

---

## Security

Releases are unsigned, so Windows SmartScreen may warn you before running the app, and
some antivirus engines may flag it for the same reason. The full
[VirusTotal scan report](https://www.virustotal.com/gui/file/f2b1ccb852ec2b3e50e6ad19819991c60d7df50a5cef05fd7b8adf8d22ce8815/detection)
is public, so you can check the binary yourself rather than take our word for it.

---

*With love by [remerlinds.com](https://remerlinds.com)*
