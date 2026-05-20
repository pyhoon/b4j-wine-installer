# B4J Silent Installer for Linux Mint (Wine-based)

> 🎯 Install B4J on Linux Mint using Wine with a single script.

[![Linux Mint](https://img.shields.io/badge/Linux_Mint-21.x%20%7C%2022.x-green?logo=linux-mint)](https://linuxmint.com/)
[![Wine](https://img.shields.io/badge/Wine-Stable-blue?logo=wine)](https://winehq.org/)
[![B4J](https://img.shields.io/badge/B4J-Basic4Java-orange?logo=java)](https://www.b4x.com/b4j.html)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## ✨ Features

This script automatically:

1. ✅ Installs **Wine Stable** (latest) from official WineHQ repository
2. ✅ Installs **Winetricks** for dependency management
3. ✅ Creates a dedicated **32-bit Wine prefix** for optimal B4J compatibility
4. ✅ Installs required components:
   - `.NET Framework 4.5.2` (dotnet452)
   - `Visual C++ 2010 Runtime` (vcrun2010)
   - `GDI+`, `corefonts`, font smoothing
5. ✅ Downloads & installs **B4J** from https://www.b4x.com/b4j/files/B4J.exe
6. ✅ Downloads & extracts **JDK 19** to `C:\Java` in Wine prefix
7. ✅ Creates **desktop launcher** with icon (menu + desktop)
8. ✅ Creates optional folders:
   - `C:\Additional Libraries\{B4A,B4J,B4X}`
   - `~/B4J_Projects` in your home directory
9. ✅ Sets appropriate permissions
10. ✅ Provides helpful terminal messages throughout

## 🖥️ System Requirements

- **Linux Mint 21.x** (Vanessa/Vera/Victoria/Virginia) or **22.x** (Wilma/Xia/Zara/Zena)
- **64-bit architecture** (with 32-bit support enabled)
- **Internet connection** for downloads
- **~2 GB free disk space** (Wine prefix + JDK + B4J)
- **sudo privileges** for system package installation

## 🚀 Quick Start

### 1. Download the script
```bash
wget https://raw.githubusercontent.com/pyhoon/b4j-wine-installer/main/install_b4j_wine.sh
chmod +x install_b4j_wine.sh
```

### 2. Run the installer
```bash
./install_b4j_wine.sh
```
> 🔐 You'll be prompted for your password when `sudo` is needed.

### 3. Launch B4J
- From Application Menu → Search "B4J"
- Or double-click the desktop icon
- Or run manually:
```bash
WINEPREFIX="$HOME/.wine_b4j" wine "C:\\Program Files\\Anywhere Software\\B4J\\B4J.exe"
```

## ⚙️ Configuration Details

### Wine Prefix Location
```
~/.wine_b4j/  (dedicated prefix, won't interfere with default ~/.wine)
```

### Java Configuration in B4J
After first launch, verify JDK path in B4J:
1. Go to **Tools → Configure Paths**
2. Ensure **Java Home** points to: `C:\Java`
3. JDK should be auto-detected as version 19.0.2

### Desktop Launcher
- Location: `~/.local/share/applications/b4j-wine.desktop`
- Also copied to: `~/Desktop/b4j-wine.desktop`
- Icon: Downloaded from B4X website (fallback to generic if unavailable)

## 🔧 Troubleshooting

### B4J won't start / crashes
```bash
# Reinstall critical components in the B4J prefix
export WINEPREFIX="$HOME/.wine_b4j"
winetricks -q dotnet452 vcrun2010 gdiplus
```

### Font rendering issues
```bash
export WINEPREFIX="$HOME/.wine_b4j"
winetricks fontsmooth=rgb corefonts
wine reg add "HKCU\Control Panel\Desktop" /v FontSmoothing /t REG_SZ /d 2 /f
```

### .NET Framework errors
```bash
# Verify .NET installation
export WINEPREFIX="$HOME/.wine_b4j"
winetricks list-installed | grep dotnet
# If missing:
winetricks -q dotnet452
```

### Reset everything
```bash
# Backup first!
mv ~/.wine_b4j ~/.wine_b4j.backup
# Then re-run the installer script
./install_b4j_wine.sh
```

### Wine Mono/Gecko download failures
The script handles this automatically by downloading MSI files directly 
<sup>[linuxcapable.com](https://linuxcapable.com/how-to-install-wine-on-linux-mint/)</sup>. If issues persist:
```bash
export WINEPREFIX="$HOME/.wine_b4j"
# Manual install commands are in the script (search for "wine-mono")
```

## 📁 Folder Structure Created

```
~/.wine_b4j/                    # Dedicated Wine prefix
├── drive_c/
│   ├── Java/                  # JDK 19 extracted here
│   ├── Program Files/
│   │   └── Anywhere Software/
│   │       └── B4J/          # B4J installation
│   └── Additional Libraries/ # Optional libraries folder
│       ├── B4A/
│       ├── B4J/
│       └── B4X/
│
~/B4J_Projects/                # Default project location
~/.local/share/applications/b4j-wine.desktop  # Menu launcher
~/Desktop/b4j-wine.desktop     # Desktop shortcut
```

## 🛡️ Security & Permissions

- Script **does not run as root** (checks and exits if attempted)
- Uses `sudo` only for system package installation
- Wine prefix owned by your user account
- All downloads use HTTPS from official sources
- No telemetry or external analytics

## 🔄 Updates

### Update Wine
```bash
sudo apt update
sudo apt install --only-upgrade winehq-stable
```

### Update B4J
1. Download latest B4J.exe from https://www.b4x.com/b4j.html
2. Run installer in the prefix:
```bash
WINEPREFIX="$HOME/.wine_b4j" wine ~/Downloads/B4J.exe
```

### Update Winetricks components
```bash
export WINEPREFIX="$HOME/.wine_b4j"
winetricks --update
winetricks -q dotnet452 vcrun2010 gdiplus
```

## 📚 References & Resources

- WineHQ Installation Guide for Linux Mint <sup>[linuxcapable.com](https://linuxcapable.com/how-to-install-wine-on-linux-mint/)</sup>
- B4J on Wine AppDB <sup>[appdb.winehq.org](https://appdb.winehq.org/objectManager.php?sClass=application&iId=21338)</sup>
- B4X Forum: Running B4J on Linux with Wine <sup>[www.b4x.com](https://www.b4x.com/android/forum/threads/running-b4a-and-b4j-under-linux-with-wine-fully-functional.98431/)</sup>
- Winetricks Documentation <sup>[GitHub](https://github.com/Winetricks/winetricks?spm=a2ty_o01.29997173.0.0.222555fb6auMYp)</sup>
- Wine Prefix Management <sup>[linuxconfig.org](https://linuxconfig.org/using-wine-prefixes)</sup>

## ⚠️ Disclaimer

> This script is **not officially supported or endorsed** by Anywhere Software (B4J developers) or WineHQ. Use at your own risk. Always backup important data before running installation scripts. The author is not responsible for any damage to your system.

## 🤝 Contributing

Found an issue or have an improvement?
1. Fork the repository
2. Create a feature branch
3. Submit a Pull Request

## 📄 License

MIT License - See [LICENSE](https://github.com/pyhoon/b4j-wine-installer/tree/main?tab=MIT-1-ov-file#) file for details.

---
*Last updated: 21 May 2026 | Compatible with Linux Mint 21.x / 22.x*
