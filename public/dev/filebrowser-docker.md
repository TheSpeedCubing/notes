---
date: 2025-04-19 13:43:00
slug: a783bf21
title: "Filebrowser Docker setup"
---

# Overview

本文件提供了簡單的 https://github.com/filebrowser/filebrowser 配置，使用Docker。

## Installation

### file structure

```yml
- filebrowser
  - config
    - settings.yml
  - database
    - filebrowser.db
  - start.sh
```

### scripts

其中 -v /path/to/your/files 換成你要serve的folder
```shell
docker stop filebrowser
docker rm filebrowser
docker run -d --name filebrowser -v /path/to/your/files:/srv -v ./database/filebrowser.db:/database/filebrowser.db -v ./config/settings.json:/config/settings.json -e PUID=$(id -u) -e PGID=$(id -g) -p 1235:80 filebrowser/filebrowser:s6
```

## Configuration

### settings.yml
Default: https://github.com/filebrowser/filebrowser/blob/master/docker/root/defaults/settings.json

```json
{
  "port": 80,
  "baseURL": "",
  "address": "0.0.0.0",
  "log": "stdout",
  "database": "/database/filebrowser.db",
  "root": "/srv"
}
```

### 關閉驗證
```
cd database
filebrowser config set --auth.method=noauth
```
