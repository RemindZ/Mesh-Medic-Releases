# Mesh Medic - Batch 3D Mesh Repair

## About

A Windows tool that batch-repairs 3D printing STL files. It reads STL files, checks for mesh errors, and repairs them using the Windows 3D Printing API - the same repair engine used by **Windows 3D Builder**. Files are repaired in-place with automatic backup safety.

> **Prerequisite:** [Microsoft 3D Builder](https://apps.microsoft.com/detail/9wzdncrfj3t6) must be installed from the Microsoft Store. If 3D Builder is not available in your region, the app provides an [alternative download via Uptodown](https://3d-builder.en.uptodown.com/windows). Mesh Medic uses the 3D repair engine that ships with 3D Builder - without it, repairs will fail.

## Usage

Download the latest `MeshMedic.exe` from the [Releases](../../releases) page.

### Three ways to use it

**1. Command line** - pass a folder path directly:

```
MeshMedic "C:\My Models\Minis"
```

**2. Terminal** - open a terminal in your STL folder and type:

```
MeshMedic
```

**3. Direct launch** - double-click `MeshMedic.exe`, browse or paste a folder path, and click **Start Repair**.

### Setup (optional)

For easy access from any terminal, copy `MeshMedic.exe` to a dedicated folder and add it to your PATH:

```
mkdir "C:\Program Files\MeshMedic"
copy MeshMedic.exe "C:\Program Files\MeshMedic\"
```

Then add to PATH (run Command Prompt as Administrator):

```
setx PATH "%PATH%;C:\Program Files\MeshMedic" /M
```

Restart your terminal. You can now run `MeshMedic` from anywhere - no `.exe` extension needed.

**Or via Windows Settings:**

1. Press `Win + R`, type `sysdm.cpl`, press Enter
2. Go to **Advanced** tab → **Environment Variables**
3. Under **System variables**, select `Path` → **Edit**
4. Click **New** and add `C:\Program Files\MeshMedic`
5. Click **OK** and restart your terminal

### Arguments

- **Directory or file path** (optional) - folder of STL files, or a single `.stl` file (its parent folder will be used). Defaults to the current working directory.
- `--timeout <seconds>` (optional) - max repair time per file. Default: `600` (10 minutes).

### Examples

```
MeshMedic                                  # Repair current folder
MeshMedic "C:\Models\MyPrints"             # Specific folder
MeshMedic "C:\Models\dragon.stl"           # Parent folder of a file
MeshMedic "C:\Models" --timeout 120        # Custom timeout (2 min)
```

### How It Works

Files are repaired **in-place** with a safe backup workflow:

1. `model.stl` → creates `model_backup.stl`
2. Repairs and overwrites `model.stl`
3. On success → deletes `model_backup.stl`
4. On failure → restores `model.stl` from backup

Your original files are never corrupted, even if the repair crashes or is interrupted.

**Smart skip:** Files that are already valid are detected and left untouched. No wasted time, no unnecessary writes.

**Repair strategies:** Mesh Medic tries multiple approaches - `RepairAsync`, `RepairWithProgressAsync`, and `TryPartialRepairAsync` - falling back automatically if one method fails.

### Repair Log

Successfully repaired files are logged to `AAA repaired.txt` in the target directory. On subsequent runs, files already in the log are **skipped**, so you can safely re-run the tool without re-processing everything. Delete the log file to force a full re-run.

### GUI

The app opens a graphical window showing:
- Progress bar with file count
- Live log with color-coded results per file
- Completion statistics (repaired, already valid, skipped, failed, time elapsed)
- Button to open the target folder

In **interactive mode** (double-click launch), you also get:
- Folder picker with Browse button
- Help overlay (click **?**) with setup instructions and tabbed usage guide
- Theme toggle - Light, Dark, or Automatic

### Requirements

- **Windows 3D Builder** - [install from Microsoft Store](https://apps.microsoft.com/detail/9wzdncrfj3t6). If unavailable in your region, use the [alternative download via Uptodown](https://3d-builder.en.uptodown.com/windows). This provides the 3D repair engine that Mesh Medic depends on.
- Windows 10 (build 19041 or later)
- .NET 8.0 runtime (included in the self-contained release)

## Building from Source

```
dotnet publish MeshRepair/MeshRepair.csproj -c Release -r win-x64 --self-contained
```

The output exe will be in `MeshRepair/bin/Release/net8.0-windows10.0.19041.0/win-x64/publish/`.

## Changelog

See [CHANGELOG.md](CHANGELOG.md) for release notes.

---

*With love by [remerlinds.com](https://remerlinds.com)*
