---
slug: 8e16e353
---

# Official Image: registry

Repository List: `http://127.0.0.1:5000/v2/_catalog`

## Install

### Manually Deploy

#### docker-compose.yml
```yaml
services:
  registry:
    image: registry:2 # https://hub.docker.com/_/registry
    container_name: registry 
    ports:
      - "5000:5000"
    volumes:
      - registry-data:/var/lib/registry

volumes:
  registry-data:
    name: registry-data
```

### With htpasswd authentication

#### install htpasswd
```
sudo apt install apache2-utils
```

#### create htpasswd file
```
htpasswd -Bc ./mounts/htpasswd <username>
```

#### docker-compose.yml
```yaml
services:
  registry:
    image: registry:2
    container_name: registry # https://hub.docker.com/_/registry
    environment:
      - REGISTRY_AUTH=htpasswd
      - REGISTRY_AUTH_HTPASSWD_PATH=/auth/htpasswd
      - REGISTRY_AUTH_HTPASSWD_REALM="Registry Realm"
    ports:
      - "5000:5000"
    volumes:
      - registry-data:/var/lib/registry
      - ./mounts/htpasswd:/auth/htpasswd

volumes:
  registry-data:
    name: registry-data
```