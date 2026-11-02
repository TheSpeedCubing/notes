---
date: 2026-08-08 21:38:00
title: Running Ubuntu Cloud image on PVE
slug: 96366db6
---

- Image: [noble-server-cloudimg-amd64.img](https://cloud-images.ubuntu.com/noble/20260801/noble-server-cloudimg-amd64.img)

```
qm create 101 --memory 16384 --net0 virtio,bridge=vmbr1

qm importdisk 101 /var/lib/vz/import/noble-server-cloudimg-amd64.img local-hdd-600-dell

qm set 101 --scsihw virtio-scsi-pci --scsi0 local-hdd-600-dell:vm-101-disk-0
 
qm set 101 --boot c --bootdisk scsi0

qm set 101 --serial0 socket --vga serial0

qm disk resize 101 scsi0 64G # resize disk
```

---

參考: https://git.proxmox.com/?p=pve-docs.git;a=blob;f=qm-cloud-init.adoc;h=cfac011c659440e4b4b91d985dea79f98e5f083c;hb=HEAD
