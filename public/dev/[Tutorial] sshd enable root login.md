---
date: 2025-05-12 14:27
---

# Overview
本文件說明如何修改 SSH 設定以允許 root 登入，並重新啟動 SSH 服務。


## Steps


### modify ssh configuration

File: `/etc/ssh/sshd_config`

```cfg
+ PermitRootLogin yes
```

### restart sshd service

```shell
sudo systemctl restart sshd
```