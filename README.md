# B4J Silent Installer for Linux Mint (Wine-based)

> 🎯 Install B4J on Linux Mint using Wine with a single script.

## ✨ Features

This script automatically:

1. ✅ Installs **Wine Stable** (latest) from official WineHQ repository [[1]]
2. ✅ Installs **Winetricks** for dependency management [[8]][[9]]
3. ✅ Creates a dedicated **32-bit Wine prefix** for optimal B4J compatibility [[15]][[46]]
4. ✅ Installs required components:
   - `.NET Framework 4.5.2` (dotnet452) [[42]][[46]]
   - `Visual C++ 2010 Runtime` (vcrun2010) [[40]]
   - `GDI+`, `corefonts`, font smoothing [[65]][[67]]
5. ✅ Downloads & installs **B4J** from https://www.b4x.com/b4j/files/B4J.exe
6. ✅ Downloads & extracts **JDK 19** to `C:\Java` in Wine prefix
7. ✅ Creates **desktop launcher** with icon (menu + desktop) [[59]][[61]]
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
wget https://raw.githubusercontent.com/your-repo/b4j-wine-installer/main/install_b4j_wine.sh
chmod +x install_b4j_wine.sh