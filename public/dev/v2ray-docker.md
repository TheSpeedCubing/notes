---
date: 2025-06-09 01:02:00
title: "[Tutorial] (v2ray) v2fly setup"
slug: 991ee4ba
---

# Overview

本文件提供了簡單的 https://github.com/v2fly 配置，使用Docker。


## Docker Compose setup

Repo: https://github.com/v2fly/docker/
DockerHub: https://hub.docker.com/r/v2fly/v2fly-core

### Example docker-compose.yml

File: `docker-compose.yml`
```yaml
services:
  v2ray:
    image: v2fly/v2fly-core
    container_name: v2ray
    restart: unless-stopped
    command: run -c /etc/v2ray/config.json
    volumes:
      - /path/to/your/config.json:/etc/v2ray/config.json:ro
    ports:
      - "1080:1080"
```

## Configuration



### config.json (v4)

default: https://github.com/v2fly/v2ray-core/blob/master/release/config/config.json

### Example: vmess

```json
"inbounds": [{
    // Port to listen on. You may need root access if the value is less than 1024.
    "port": 1080,

    // IP address to listen on. Change to "0.0.0.0" to listen on all network interfaces.
    "listen": "0.0.0.0",

    // Tag of the inbound proxy. May be used for routing.
    "tag": "socks-inbound",

    // Protocol name of inbound proxy.
    "protocol": "vmess",

    // Settings of the protocol. Varies based on protocol.
	"settings": {
        "clients": [
          {
            "id": "(id)",
            "alterId": 0,
            "security": "auto"
          }
        ]
      }
  }]
```
