# neo-vim-config

```powershell
# 1) Find gcc.exe inside the WinLibs package
$gcc = Get-ChildItem "$env:LOCALAPPDATA\Microsoft\WinGet\Packages\BrechtSanders.WinLibs.POSIX.UC*" -Recurse -Filter gcc.exe -ErrorAction SilentlyContinue |
  Select-Object -First 1 -ExpandProperty FullName

if (-not $gcc) {
  Write-Host "Couldn't find gcc.exe under the WinLibs package path." -ForegroundColor Red
} else {
  $bin = Split-Path $gcc
  Write-Host "Found gcc at: $gcc"
  Write-Host "Bin folder:    $bin"

  # 2) Add it to your *user* PATH permanently
  [Environment]::SetEnvironmentVariable("Path", $env:Path + ";" + $bin, "User")

  # 3) Add it to this PowerShell session too
  $env:Path += ";" + $bin

  # 4) Verify
  gcc --version
}

```
