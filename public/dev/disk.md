## Example
- PVE 
  - /dev/sda `LVM`
    - vm-xxx-disk-0 type=raw `LV` `VM Disk`
    - vm-xxx-disk-1 type=raw `LV` `VM Disk`
    - ...
  - /dev/sdb `GPT partitions`
    - /dev/sdb1 `BIOS boot`
    - /dev/sdb2 `EFI`
    - /dev/sdb3 `LVM`
      - `LVM-thin`
        - vm-xxx-disk-0 type=raw `LV` `VM Disk`
        - vm-xxx-disk-1 type=raw `LV` `VM Disk`
        - ...
      - `Directory`
  - /dev/sdc `LVM`
    - vm-xxx-disk-0 type=raw `LV` `VM Disk`
    - vm-xxx-disk-1 type=raw `LV` `VM Disk`
    - ...
## 名詞解釋
### VM Disks Formats
- raw
- qcow2

### 磁碟分割表格式
- GPT
- MBR

### Disk
物理硬碟
### Disk Partition
物理磁碟劃分為多個邏輯區域，每個區域可以被當作獨立的磁碟來使用。每個分區可以有自己的檔案系統

### FS
- NTFS
- FAT32
- ext4

## PVE Storage
分割成很多VM Disk

種類:
- Directory
存放 VM 映像、容器、ISO、備份等。通常掛載於 /var/lib/pve 或 /mnt/storage 之類的目錄。
- ZFS
支援快照、壓縮、重複資料刪除等功能，適合高可靠性需求。
- LVM
用來管理磁碟分區，每個 VM 磁碟是一個獨立的 LVM Volume，但不支援快照。
  - 架構: 
    - Physical Disk, 能有多個
      - 多個 Physical Disk可以組VG, 能有多個
        - 一個 VG 分割成 {1,n} 個 LV, 能有多個
          - 一個 LV 對一個 FS, 能有多個
- LVM-thin
基於 LVM，但支援 精簡配置（thin provisioning），可以動態分配空間，並支援快照功能，比傳統 LVM 更靈活。

