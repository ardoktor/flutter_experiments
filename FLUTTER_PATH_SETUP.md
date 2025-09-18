# Flutter PATH Setup Guide for Windows PowerShell

This guide helps resolve common PATH issues when setting up Flutter on Windows using PowerShell.

## Common Issues and Solutions

### Issue 1: Flutter command not found
**Error:** `flutter: The term 'flutter' is not recognized...`

**Solution:**
```powershell
$env:PATH = "D:\flutter\bin;" + $env:PATH
```
Replace `D:\flutter\bin` with your actual Flutter installation path.

### Issue 2: Git not found by Flutter
**Error:** `Error: Unable to find git in your PATH.`

**Prerequisites:** Verify Git is installed:
```powershell
git --version
```

**Solution:**
```powershell
$env:PATH = "D:\flutter\bin;C:\Program Files\Git\bin;" + $env:PATH
```

### Issue 3: WHERE command not recognized
**Error:** `'WHERE' is not recognized as an internal or external command`

**Solution:** Add Windows System32 to PATH:
```powershell
$env:PATH = "D:\flutter\bin;C:\Program Files\Git\bin;C:\Windows\System32;" + $env:PATH
```

### Issue 4: PowerShell executable not found
**Error:** `PowerShell executable not found. Either pwsh.exe or PowerShell.exe must be in your PATH.`

**Solution:** Add PowerShell directory to PATH:
```powershell
$env:PATH = "D:\flutter\bin;C:\Program Files\Git\bin;C:\Windows\System32;C:\Windows\System32\WindowsPowerShell\v1.0;" + $env:PATH
```

## Complete Setup Command

Run this single command to add all necessary paths:
```powershell
$env:PATH = "D:\flutter\bin;C:\Program Files\Git\bin;C:\Windows\System32;C:\Windows\System32\WindowsPowerShell\v1.0;" + $env:PATH
```

## Verify Setup

After setting up the PATH, verify everything works:
```powershell
flutter --version
flutter doctor
```

## Make PATH Changes Permanent

The above commands only work for the current PowerShell session. To make changes permanent:

1. Open System Properties → Advanced → Environment Variables
2. Add `D:\flutter\bin` to your user or system PATH variable
3. Restart PowerShell

Or use PowerShell to modify permanently:
```powershell
[Environment]::SetEnvironmentVariable("Path", $env:Path + ";D:\flutter\bin", [EnvironmentVariableTarget]::User)
```

## Notes

- Replace `D:\flutter\bin` with your actual Flutter installation path
- Git installation path may vary (check with `where.exe git`)
- These commands are specific to Windows PowerShell
- Restart PowerShell after making permanent changes