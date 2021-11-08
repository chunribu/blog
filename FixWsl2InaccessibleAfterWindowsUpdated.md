[HOME🏠](README.md)

# Fix: WSL2 Become Inaccessible After Windows Updated
---

## Run in PowerShell as admin:
```
DISM /online /disable-feature /featurename:VirtualMachinePlatform /norestart
DISM /online /disable-feature /featurename:Microsoft-Windows-Subsystem-Linux /norestart
```
## Reboot, and again:
```
dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```
## (Optional) Reboot, and again:
```
wsl --set-default-version 2
```
