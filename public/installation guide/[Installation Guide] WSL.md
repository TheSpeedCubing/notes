---
date: 2026-02-08 14:53:00
slug: 53265b6a
---


**Powershell**

Enable WSL related Windows Features

```
dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
```

Enable VM Platform

```
Enable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform -NoRestar
```

Install WSL

```
wsl --install --no-distribution
```

Set WSL version to WSL2

```
wsl --set-default-version 2
```

```
wsl --version
```
```
PS C:\WINDOWS\system32> wsl --version
WSL version: 2.6.3.0
Kernel version: 6.6.87.2-1
WSLg version: 1.0.71
MSRDC version: 1.2.6353
Direct3D version: 1.611.1-81528511
DXCore version: 10.0.26100.1-240331-1435.ge-release
Windows version: 10.0.26200.7705
```

Install Distro

```
wsl.exe --install Debian
```

```
debian@ANDY-PC:/mnt/c/WINDOWS/system32$ wsl.exe -l -v
  NAME      STATE           VERSION
* Debian    Running         2
```