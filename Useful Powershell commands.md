# ⚡ Useful PowerShell Commands for Windows 11 Edition Configuration

### 💻 Bypass OOBE Microsoft Account Requirement
```powershell
oobe\bypassnro
# OR (for 24H2 and later)
start ms-cxh:localonly
```

### 🔒 Disable BitLocker (for Pro/Enterprise)
```powershell
Disable-BitLocker -MountPoint "C:"
```

### 🔐 Check BitLocker Status
```powershell
Get-BitLockerVolume
```

### 🧠 Retrieve BitLocker Recovery Key (if backed up to AD)
```powershell
(Get-BitLockerVolume -MountPoint "C:").KeyProtector
```

### 📦 Remove Bloatware (Example: Xbox, Candy Crush, etc.)
```powershell
Get-AppxPackage *xbox* | Remove-AppxPackage
Get-AppxPackage *candy* | Remove-AppxPackage
```

### 🧹 Full Bloatware Removal Script (Minimal)
```powershell
Get-AppxPackage | Where-Object {$_.Name -like "*bing*" -or $_.Name -like "*xbox*" -or $_.Name -like "*zune*" -or $_.Name -like "*candy*"} | Remove-AppxPackage
```

### 🛑 Disable Windows Update Service (temporary freeze)
```powershell
Stop-Service wuauserv
Set-Service wuauserv -StartupType Disabled
```

### 🔄 Re-enable Windows Update
```powershell
Set-Service wuauserv -StartupType Manual
Start-Service wuauserv
```

### 🧰 Enable Group Policy Editor (for Home Edition)
```powershell
dism /online /add-package /packagepath:"%SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientExtensions-Package~*.cab"
dism /online /add-package /packagepath:"%SystemRoot%\servicing\Packages\Microsoft-Windows-GroupPolicy-ClientTools-Package~*.cab"
```

### 📎 Export Installed Programs List
```powershell
Get-ItemProperty HKLM:\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Uninstall\* | Select-Object DisplayName, DisplayVersion, Publisher | Format-Table –AutoSize
```

### ⚙️ Check TPM Status
```powershell
Get-WmiObject -Namespace "Root\CIMv2\Security\MicrosoftTpm" -Class Win32_Tpm | Select *
```

### 🧱 Disable Telemetry (Basic Level)
```powershell
Set-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows\DataCollection" -Name AllowTelemetry -Value 0
```

### 🔄 Restart Explorer (for UI changes)
```powershell
Stop-Process -Name explorer -Force
Start-Process explorer
```

### ✅ Confirm Windows Edition
```powershell
(Get-WmiObject -class Win32_OperatingSystem).Caption
```

### 🆔 Display Current Activation Status
```powershell
slmgr.vbs /xpr
```

### 🪪 View Installed Product Key (Last 5 chars)
```powershell
(Get-WmiObject -query 'select * from SoftwareLicensingService').OA3xOriginalProductKey
```

### 🪓 Disable Copilot (Enterprise/Pro)
```powershell
reg add "HKLM\Software\Policies\Microsoft\Windows\WindowsCopilot" /v TurnOffWindowsCopilot /t REG_DWORD /d 1 /f
```

### 🚫 Disable Cortana (for older versions)
```powershell
reg add "HKLM\Software\Policies\Microsoft\Windows\Windows Search" /v AllowCortana /t REG_DWORD /d 0 /f
```

# 📌 Note:
Some commands require administrator rights. Right-click PowerShell and choose "Run as Administrator" to ensure full access.
