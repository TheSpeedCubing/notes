---
date: 2025-06-08 11:49:00
slug: f6905dc6
title: "[Tutorial] Github Actions + ghcr for Docker"
---

# Overview

從 GitHub Actions 推送 Docker Image 至 GHCR 的配置

## Action Secrets

- **REGISTRY_URL**: `ghcr.io/<username>` 或 `ghcr.io/<organizationName>`  
- **REGISTRY_USERNAME**: 擁有 token 的使用者名稱  
- **REGISTRY_PASSWORD**: Classic token（需具備 packages 的讀寫權限）  


> [!NOTE]
> `docker login "$REGISTRY_URL"` 中的 URL 也可以直接使用 `ghcr.io`，不一定要加上 `/username`

## Example workflow.yml

File: `.github/workflows/workflow.yml`

```yaml
name: Build Docker Image

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest

    env:
      REGISTRY_URL: ${{ secrets.REGISTRY_URL }}
      REGISTRY_USERNAME: ${{ secrets.REGISTRY_USERNAME }}
      REGISTRY_PASSWORD: ${{ secrets.REGISTRY_PASSWORD }}

    steps:
      - name: Checkout repository
        uses: actions/checkout@v4

      - name: Build Docker Image
        run: |
          docker build --progress=plain -t "$REGISTRY_URL/cgit" .

      - name: Log in to Docker Registry
        run: echo "$REGISTRY_PASSWORD" | docker login "$REGISTRY_URL" -u "$REGISTRY_USERNAME" --password-stdin

      - name: Push Docker Image
        run: docker push "$REGISTRY_URL/cgit"
