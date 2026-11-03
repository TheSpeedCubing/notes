---
date: 2026-03-05 14:14
title: Auth0 Setup
slug: 5efbf553
---

### Auth0

**create application**

- 裡面有 <client-id>

**Tenant Settings 建立 Signing Key**

**Tenant Settings 建立 Custom Domains**

add CNAME Records, verify

### Google OAuth2

https://console.cloud.google.com/auth/clients/
建立好 Client 後，有 Client ID & Client secret
    
**記得加上層的 callback-url**
    
**記得加上層的 callback-url**
    
### Cloudflare -> Auth0

**Login Method**
Okta 

填入:
- Single sign-on URL
    ```
    https://<domain>/samlp/<client-id>
    ```

- IdP Entity ID or Issuer URL
    ```
    urn:<domain>
    ```
- Signing Certificate
    
### Cloudflare -> Google

**Login Method**
Google 

填入:
- Client ID
- Client secret
