# engram-dist

Public distribution for **`engram-ingest`** — the customer-facing remote-ingest client for
[Engram](https://engram.network-ideas.net). Source lives in the private `engram` repo; this repo
only hosts released binaries via **GitHub Releases**.

`engram-ingest` pushes a repository's context to **your** Engram instance over the authenticated
write API. It needs **no .NET install, no database connection string, and no embeddings key**
(system `git` is required only for commit ingest).

## Download

Grab the binary for your platform from the [latest release](../../releases/latest):

| Platform | Asset |
| --- | --- |
| Windows (x64) | `engram-ingest-<version>-win-x64.exe` |
| Linux (x64) | `engram-ingest-<version>-linux-x64` |
| macOS (Apple Silicon) | `engram-ingest-<version>-osx-arm64` |

Each release also includes a **`SHA256SUMS`** file.

## Verify the download

```bash
# Linux / macOS
sha256sum -c SHA256SUMS          # (or: shasum -a 256 -c SHA256SUMS on macOS)
```
```powershell
# Windows (PowerShell)
(Get-FileHash -Algorithm SHA256 .\engram-ingest-<version>-win-x64.exe).Hash
# compare against the matching line in SHA256SUMS
```

## First run (v1 is unsigned)

These binaries are **not yet code-signed / notarized**. One-time per platform:

- **Windows (SmartScreen):** "More info → Run anyway".
- **macOS (Gatekeeper):**
  ```bash
  xattr -d com.apple.quarantine ./engram-ingest-<version>-osx-arm64
  chmod +x ./engram-ingest-<version>-osx-arm64
  ```
- **Linux:** `chmod +x ./engram-ingest-<version>-linux-x64`

## Usage

```bash
engram-ingest --version            # build version + targeted API version
engram-ingest --help
engram-ingest --root . --dry-run   # read-only preview (no upload)
engram-ingest --root . --commits   # real ingest (commit history needs system git)
```

Configuration (API URL, OAuth token endpoint, `client_id`/`client_secret`) is provided **outside**
the repo you ingest — via env vars (`ENGRAM_API_URL`, `ENGRAM_TOKEN_URL`, `ENGRAM_CLIENT_ID`,
`ENGRAM_CLIENT_SECRET`) or a user-level `--config <path>` JSON file. Your Engram onboarding package
includes these values. The access token is held in memory only and never written to disk.

## Support / changelog

See each [Release](../../releases) for notes. Issues: contact your Engram provider.