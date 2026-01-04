DLL SIDELOAD + PROCESS INJECTION + PERSISTENCE
=================================================

Method: DLL Hijacking + Remote Process Injection + Registry Persistence
DLL Template: mscorsvc.dll
Target Process: explorer.exe

Files:
- SystemService.exe (Loader executable with auto-install)
- mscorsvc.dll (Malicious DLL)

Instructions:
1. Extract BOTH files to SAME directory
2. Run SystemService.exe
3. First run: Auto-installs to %APPDATA%\Microsoft\[RandomName]
4. Adds registry Run key for persistence
5. Payload injects into explorer.exe for stealth
6. Survives reboots automatically

Technical Flow (First Run):
SystemService.exe → Copies itself + DLL to APPDATA → Adds registry key → Launches installed copy → Original exits

Technical Flow (Subsequent Runs):
Registry → SystemService.exe → Loads mscorsvc.dll → Injects into explorer.exe → Loader exits

Persistence Features:
- Installation to %APPDATA%\Microsoft\[Random folder name]
- Registry Run key (HKCU) with random name
- Both EXE and DLL copied to install location
- Automatic execution on login
- Stealth operation (no windows)

Features:
- ✅ Registry persistence (survives reboot)
- ✅ Random folder & registry names
- ✅ Payload runs in explorer.exe context
- ✅ Loader process exits after injection
- ✅ No orphaned processes
- ✅ Maximum stealth
