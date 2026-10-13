# WireGuard Remote Access

**Status:** Primary WireGuard instance with a secondary backup.

## Known Configuration

| Component | Host | Role |
|---|---|---|
| Primary WireGuard | Proxmox CT 100 | Main VPN server |
| Backup WireGuard | Raspberry Pi | Secondary VPN instance |
| WireGuard Dashboard | Both hosts | Web management interface |

The Proxmox host provides the primary VPN service, while the Raspberry Pi maintains a separate backup instance.
