---
date: 2026-06-16 12:07:00
title: Enable no-subscription repository on PVE
slug: 9ea451fe
---

```
cat > /etc/apt/sources.list.d/proxmox-no-subscription.sources <<'EOF'
Types: deb
URIs: http://download.proxmox.com/debian/pve
Suites: trixie
Components: pve-no-subscription
Signed-By: /usr/share/keyrings/proxmox-archive-keyring.gpg
EOF

rm  /etc/apt/sources.list.d/pve-enterprise.sources
```
