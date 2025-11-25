# LOVE2D Build EXE

A PowerShell script that automatically creates a standalone Windows executable (`.exe`) from any LOVE2D game project.

## Features

- **Auto-detects LOVE installation** - No manual path configuration needed
- **Works with any LOVE2D game** - Just place the script in your game folder
- **Creates standalone executable** - Combines `love.exe` with your game into `game.exe`
- **Copies required DLLs** - Automatically includes all necessary dependencies
- **Simple to use** - One command to build your game

## Requirements

- **Windows** (PowerShell 5.1 or later)
- **LOVE2D** installed on your system
- A LOVE2D game project with `main.lua` file

## Quick Start

1. **Copy `build-exe.ps1`** into your LOVE2D game folder (the folder containing `main.lua`)

2. **Run the script:**
   ```powershell
   .\build-exe.ps1
   ```

3. **Find your executable** in the `build` folder that gets created

## Output Structure

After running the script, you'll have:

```
your-game-folder/
├── build/
│   ├── game.exe      ← Your standalone executable
│   ├── *.dll         ← Required DLL files
│   └── bin/          ← Additional DLLs (if your game has them)
└── build-exe.ps1
```

## How Auto-Detection Works

The script automatically finds your LOVE installation by checking these locations in order:

1. `C:\Program Files\LOVE`
2. `%LOCALAPPDATA%\Programs\LOVE`
3. `C:\Program Files (x86)\LOVE`
4. System PATH (if `love.exe` is available globally)

If LOVE is found, the script proceeds. If not, you'll get a helpful error message.

## Configuration

You can customize the output folder by editing this line in the script:

```powershell
$path1 = Join-Path $PSScriptRoot "build"
```

Change `"build"` to any folder name you prefer, or use an absolute path like:
```powershell
$path1 = "C:\MyGameBuilds\MyGame"
```

## How It Works

1. **Searches for LOVE2D** - Automatically detects your LOVE installation
2. **Validates project** - Checks that `main.lua` exists
3. **Creates build folder** - Sets up output directory
4. **Compresses game** - Zips all your game files
5. **Creates executable** - Combines `love.exe` + `game.zip` = `game.exe`
6. **Copies DLLs** - Includes all required runtime libraries

## Distribution

To distribute your game:

1. Copy the entire contents of the `build` folder
2. Share that folder with others
3. They can run `game.exe` directly - no LOVE installation needed!

## Troubleshooting

### "LOVE installation not found"

**Solution:** Make sure LOVE is installed. The script searches common installation paths. If LOVE is installed elsewhere, you can manually set the path in the script.

### "Execution Policy" Error

If PowerShell blocks the script, run:
```powershell
powershell -ExecutionPolicy Bypass -File .\build-exe.ps1
```

Or set execution policy (as Administrator):
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### "main.lua is missing"

**Solution:** Make sure you're running the script from your game folder (the folder containing `main.lua`).

## Notes

- The script excludes build artifacts, documentation, and script files from the zip
- The executable name is always `game.exe` (you can rename it after building)
- Each build overwrites previous builds in the output folder
- The script works with any LOVE game version (11.0+)

## Related

- [LOVE2D Official Website](https://love2d.org/)
- [LOVE2D Documentation](https://love2d.org/wiki/Main_Page)

## License

This script is provided as-is. Feel free to use, modify, and distribute it with your games.

---

**Made for LOVE2D game developers**

