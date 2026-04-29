# CardputerZero AppBuilder Release

CI/CD wrapper for [m5stack/CardputerZero-AppBuilder](https://github.com/m5stack/CardputerZero-AppBuilder).

This repo **does not contain source code**. It only hosts GitHub Actions workflows that:
1. Check out the source from `m5stack/CardputerZero-AppBuilder` (private repo)
2. Build the Tauri desktop app (Windows / macOS / Linux)
3. Build DEB packages for M5CardputerZero devices
4. Publish release artifacts

## Why a separate repo?

The upstream `m5stack/CardputerZero-AppBuilder` is a private repository with limited GitHub Actions minutes. This repo runs CI/CD under a different quota.

## Setup

A **deploy key** or **PAT** is required to clone the private upstream repo during CI.

### Option A: Deploy Key (recommended, least privilege)

1. Generate an SSH key pair:
   ```bash
   ssh-keygen -t ed25519 -C "ci-cardputerzero-appbuilder" -f deploy_key -N ""
   ```
2. Add the **public key** (`deploy_key.pub`) as a **Deploy Key** in [m5stack/CardputerZero-AppBuilder](https://github.com/m5stack/CardputerZero-AppBuilder/settings/keys) → Settings → Deploy keys → Add deploy key (read-only)
3. Add the **private key** (`deploy_key`) as a **Secret** in this repo → Settings → Secrets and variables → Actions → New repository secret, name it `UPSTREAM_DEPLOY_KEY`
4. Delete the local key files after setup

### Option B: Personal Access Token (PAT)

1. Create a [Fine-grained PAT](https://github.com/settings/tokens?type=beta) with:
   - Repository access: `m5stack/CardputerZero-AppBuilder` only
   - Permissions: Contents → Read-only
2. Add as secret `UPSTREAM_PAT` in this repo

## Workflows

| Workflow | Trigger | Description |
|----------|---------|-------------|
| `build-tauri.yml` | push to main, manual | Build Tauri desktop app from upstream source |
| `build-deb.yml` | manual (workflow_dispatch) | Build DEB packages for device |

## License

MIT
