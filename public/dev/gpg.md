---
date:2025-05-04
---

# GPG Usage Guide

## Generate Key using gpg

```
gpg --full-generate-key
```
或是
```
gpg --expert --full-generate-key
```

選項:
```
Please select what kind of key you want:
   (1) RSA and RSA (default)
   (2) DSA and Elgamal
   (3) DSA (sign only)
   (4) RSA (sign only)
   (7) DSA (set your own capabilities)
   (8) RSA (set your own capabilities)
   (9) ECC and ECC
  (10) ECC (sign only)
  (11) ECC (set your own capabilities)
  (13) Existing key
  (14) Existing key from card

Please select which elliptic curve you want:
   (1) Curve 25519
   (3) NIST P-256
   (4) NIST P-384
   (5) NIST P-521
   (6) Brainpool P-256
   (7) Brainpool P-384
   (8) Brainpool P-512
   (9) secp256k1

Please specify how long the key should be valid.
         0 = key does not expire
      <n>  = key expires in n days
      <n>w = key expires in n weeks
      <n>m = key expires in n months
      <n>y = key expires in n years

```
需要輸入Real name, Email address, Comment
```
GnuPG needs to construct a user ID to identify your key.

Real name: speedcubing
Email address: speedcubing@speedcubing.top
Comment: speedcubing
```
接下來會需要輸入一組密碼, 使用私鑰時會需要。

之後revocation certificate(撤銷證書)會建立於`~/.gnupg/openpgp-revocs.d/<fingerprint>.rev`
並且會看到有一組Key以及它的資訊出現
```
pub   <algorithm> <date> [SC]
      <fingerprint>
uid           [<level>] <Real name> (<Comment>) <<Email address>>
sub   <algorithm> <date> [E]
```
## List all Keys

```
gpg --list-keys
```

## Import Public Key

1. 匯入Public Key

  - 直接匯入Public Key檔案
  ```
  gpg --import pub.asc
  ```
  - 從keyserver以fingerprint匯入
  ```
  gpg --keyserver <keyserver> --recv-keys <fingerprint>
  ```
  
2. 使用fingerprint校驗Public Key
可以看一下儲存的Key的fingerprint是不是相同。
```
gpg --list-keys
```

## Encrypt file with Public Key

(file.txt)
```
gpg --encrypt --recipient <fingerprint> --output file.txt.gpg file.txt
```

## Decrypt file

(要先有私鑰)

```
gpg --decrypt file.txt.gpg
```
```
gpg --decrypt --output file.txt file.txt.gpg
```

## Export Key

- Public Key
```
gpg -a --export <fingerprint> > publickey.asc
```

- Private Key
```
gpg -a --export-secret-keys <fingerprint> > privatekey.asc
```

註: -a 為 --armor, 文字檔格式