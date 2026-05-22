# Halison Works software — install artifacts

This repository is the **public distribution channel** for software from [Halison Works](https://github.com/halisonworks). Source code for the products lives in private repositories; **only the install artifacts and release notes are published here.**

## Available products

### App Studio

A lightweight JSX component viewer + packager for React developers. Paste or load a `.jsx` file and see it rendered live via runtime Babel with auto-resolved dependencies from esm.sh. Save canvases to a local library, reopen them later, and package any canvas as a standalone Windows installer.

**Current release**: [`app-studio-v0.2.0`](https://github.com/halisonworks/halison-software/releases/tag/app-studio-v0.2.0) (pre-release for testers).

**Install:**

```powershell
# WinGet (cleanest install, no SmartScreen warning)
winget install HalisonWorks.AppStudio

# Scoop
scoop bucket add app-studio https://github.com/halisonworks/app-studio-app
scoop install app-studio

# Chocolatey
choco install app-studio

# Direct MSI download — expect a SmartScreen warning, see below
```

See [App Studio's installation guide](https://github.com/halisonworks/app-studio-app/blob/main/docs/install-windows.md) for the full walkthrough, including how to bypass the SmartScreen warning if you download the MSI directly.

## Release tag naming

Releases are namespaced per product: `<product>-v<version>`. Examples:

- `app-studio-v0.2.0`
- `app-studio-v0.2.1`
- `runtime-v1.0.0` (future)

This lets a single repository host releases for multiple products without tag collisions.

## What's not here

- **Source code** — lives in product-specific private repositories. Visible to maintainers; not currently licensed for public use.
- **Issue tracking** — open issues against the product's primary repo (e.g. [`halisonworks/app-studio-app/issues`](https://github.com/halisonworks/app-studio-app/issues)).
- **Documentation** — same; product docs live with the source.

## Code signing

Install artifacts published here are **currently unsigned**. Windows users installing directly via MSI will see a SmartScreen "unknown publisher" warning. Bypass guidance lives in the product's installation docs.

A code-signing pipeline using Azure Trusted Signing is wired (inert) into the App Studio build workflow; it activates when six `AZURE_*` GitHub secrets are set. Tracking item, expected to land for App Studio v0.3 or earlier.

For users who want clean installs today: use WinGet / Chocolatey / Scoop (any of the package-manager paths above) — those bypass SmartScreen entirely.
