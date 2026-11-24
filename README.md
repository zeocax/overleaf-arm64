# Overleaf Community Edition (Native ARM64 + TeX Live Full)

Automated native `linux/arm64` Docker builds of official [overleaf/overleaf](https://github.com/overleaf/overleaf) Community Edition with full TeX Live (`scheme-full`), built on GitHub-hosted `ubuntu-24.04-arm` runners and published to GitHub Container Registry (`ghcr.io`).

## Published Tags

- `ghcr.io/zeocax/overleaf-arm64:latest` — Latest Overleaf CE `main` build (`linux/arm64`)
- `ghcr.io/zeocax/overleaf-arm64:sha-<commit>` — Pinned to exact `overleaf/overleaf` commit SHA
- `ghcr.io/zeocax/overleaf-arm64:<YYYYMMDD>` — Build date snapshot
- `ghcr.io/zeocax/overleaf-arm64:base-<hash>` / `base-latest` — Cached base layer (Ubuntu 24.04 Phusion + Node.js + TeX Live `scheme-full`)

## How Updates Work

1. A daily scheduled check compares `overleaf/overleaf` (`main`) against existing `:sha-<commit>` tags in GHCR.
2. If upstream has not changed, the workflow exits in ~3 seconds.
3. When upstream updates:
   - Reuses `:base-<hash>` if `server-ce/Dockerfile-base` is unchanged (~5–10 min build).
   - Automatically rebuilds `:base-<hash>` only when `server-ce/Dockerfile-base` changes or `force_rebuild_base` is triggered manually.
