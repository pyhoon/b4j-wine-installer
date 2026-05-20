## 🔑 Key Technical Notes

1. **32-bit Wine prefix** (`WINEARCH=win32`) is used because B4J and its .NET dependencies have better compatibility in 32-bit Wine environments <sup>[forum.winehq.org](https://forum.winehq.org/viewtopic.php?t=35509)</sup>.

2. **Dedicated prefix** (`~/.wine_b4j`) isolates B4J from other Wine applications, preventing dependency conflicts <sup>[linuxconfig.org](https://linuxconfig.org/using-wine-prefixes)</sup> <sup>[askubuntu.com](https://askubuntu.com/questions/956244/what-is-a-wineprefix)</sup>.

3. **Silent installation** uses Inno Setup parameters (`/VERYSILENT /SUPPRESSMSGBOXES`) for B4J, and `winetricks -q` for quiet component installs.

4. **JDK extraction** uses native Linux `unzip` then copies to Wine's C: drive, avoiding potential Wine zip handling issues.

5. **Desktop integration** follows Linux Mint/Cinnamon standards with proper `.desktop` file fields and icon handling <sup>[forum.manjaro.org](https://forum.manjaro.org/t/how-to-create-desktop-shortcut-link-to-application-installed-in-wine/25660)</sup> <sup>[forum.winehq.org](https://forum.winehq.org/viewtopic.php?t=33554)</sup>.