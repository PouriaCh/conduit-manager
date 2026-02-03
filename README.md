# Conduit Manager - macOS Edition

A management tool for running Psiphon Conduit nodes on macOS (Apple Silicon). Help users access the open internet during network restrictions.

> **Note:** For Linux servers, use the [main branch](https://github.com/SamNet-dev/conduit-manager/tree/main).

## Quick Install

```bash
curl -sL https://raw.githubusercontent.com/SamNet-dev/conduit-manager/macos-edition/conduit.sh | bash
```

Or download and run manually:

```bash
curl -sL https://raw.githubusercontent.com/SamNet-dev/conduit-manager/macos-edition/conduit.sh -o conduit.sh
bash conduit.sh
```

## Requirements

- macOS with Apple Silicon (M1/M2/M3/M4)
- Homebrew (installed automatically if missing)
- Internet connection

## What Gets Installed

- **Docker Desktop** (via Homebrew cask, if not present)
- **Conduit container** running in Docker
- **`conduit` CLI** command for management

## CLI Commands

```bash
conduit status       # Show current status
conduit stats        # Live statistics
conduit logs         # View Docker logs
conduit health       # Run diagnostics
conduit peers        # Live peer traffic by country (requires sudo)

conduit start        # Start container
conduit stop         # Stop container
conduit restart      # Restart container
conduit update       # Update to latest image

conduit settings     # Change max-clients and bandwidth
conduit menu         # Interactive menu

conduit backup       # Backup node identity key
conduit restore      # Restore from backup
conduit uninstall    # Remove everything
```

## Configuration

| Option | Default | Range | Description |
|--------|---------|-------|-------------|
| `max-clients` | 200 | 1-1000 | Maximum concurrent proxy clients |
| `bandwidth` | 5 | 1-40, -1 | Bandwidth limit per peer (Mbps). -1 = unlimited |

## macOS-Specific Notes

- Docker runs via **Docker Desktop** (not Docker Engine)
- Uses **port publishing** (443/TCP+UDP) instead of host networking
- **No auto-start on boot** (launchd not implemented yet)
- `conduit peers` requires **sudo** (uses tcpdump)
- GeoIP uses free **DB-IP Lite** database (no account needed)

## Uninstall

```bash
conduit uninstall
```

Or manually:
```bash
docker stop conduit && docker rm conduit
docker volume rm conduit-data
rm -rf /opt/conduit
rm /usr/local/bin/conduit
```

---

## License

MIT License

## Links

- [Psiphon](https://psiphon.ca/)
- [Psiphon Conduit](https://github.com/Psiphon-Inc/conduit)
- [Linux Version (main branch)](https://github.com/SamNet-dev/conduit-manager/tree/main)
