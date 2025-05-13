# Hacking-tools-for-Windows
a few hacking tools for windows
paste this in your terminal(cmd) as admin:
@echo off
echo ============================================
echo   Windows Hacking Toolset Installer (CMD)
echo ============================================

:: Step 1: Create tools directory
set "TOOL_DIR=C:\HackingTools"
mkdir "%TOOL_DIR%"
echo [+] Created folder: %TOOL_DIR%

:: Step 2: Install tools via winget
echo [+] Installing tools via winget...
winget install -e --id Nmap.Nmap
winget install -e --id WiresharkFoundation.Wireshark
winget install -e --id WiresharkFoundation.TShark
winget install -e --id Insecure.Sqlmap
winget install -e --id OWASP.ZAP
winget install -e --id Python.Python.3.12
winget install -e --id Git.Git
winget install -e --id OpenJS.NodeJS.LTS

:: Step 3: Download portable tools
echo [+] Downloading portable tools...

:: Download Hydra (Windows fork)
curl -L -o "%TOOL_DIR%\hydra.zip" https://github.com/0xsp-SRD/multibruteforce/releases/download/v1.0/hydra-win.zip

:: Download Hashcat
curl -L -o "%TOOL_DIR%\hashcat.7z" https://hashcat.net/files/hashcat-6.2.6.7z

:: Download Nikto (Perl)
curl -L -o "%TOOL_DIR%\nikto-master.zip" https://github.com/sullo/nikto/archive/refs/heads/master.zip

:: Step 4: Extract tools (you must have 7-Zip installed!)
echo [+] Extracting archives...
if exist "C:\Program Files\7-Zip\7z.exe" (
    "C:\Program Files\7-Zip\7z.exe" x "%TOOL_DIR%\hydra.zip" -o"%TOOL_DIR%\hydra"
    "C:\Program Files\7-Zip\7z.exe" x "%TOOL_DIR%\hashcat.7z" -o"%TOOL_DIR%\hashcat"
    "C:\Program Files\7-Zip\7z.exe" x "%TOOL_DIR%\nikto-master.zip" -o"%TOOL_DIR%\nikto"
) else (
    echo [!] Please install 7-Zip to extract files automatically.
)

:: Step 5: Add tool directory to system PATH
echo [+] Adding tools to system PATH...
setx PATH "%PATH%;%TOOL_DIR%\hydra;%TOOL_DIR%\hashcat;%TOOL_DIR%\nikto"

:: Step 6: Cleanup
del "%TOOL_DIR%\hydra.zip"
del "%TOOL_DIR%\hashcat.7z"
del "%TOOL_DIR%\nikto-master.zip"

echo.
echo [✓] Setup complete!
echo Reboot your system or restart CMD to apply PATH changes.
pause
