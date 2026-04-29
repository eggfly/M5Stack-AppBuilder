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

A **Fine-grained PAT** is required to clone the private upstream repo during CI.

1. Create a [Fine-grained PAT](https://github.com/settings/tokens?type=beta) with:
   - Resource owner: `m5stack`
   - Repository access: Only select repositories → `m5stack/CardputerZero-AppBuilder`
   - Permissions: Contents → Read-only
   - Expiration: 1 year (max)
2. Add as secret `UPSTREAM_PAT` in this repo → Settings → Secrets and variables → Actions → New repository secret

## Workflows

| Workflow | Trigger | Description |
|----------|---------|-------------|
| `build-tauri.yml` | push to main, manual | Build Tauri desktop app from upstream source |
| `build-deb.yml` | manual (workflow_dispatch) | Build DEB packages for device |

## License

MIT
