## Device IP Address Inventory

| Device / Service | IP Address | Status / Notes |
|---|---|---|
| UniFi Dream Machine 7 | `192.168.1.1` | Confirmed gateway |
| Proxmox VE (`pve3`) | `192.168.1.222` | Confirmed management address |
| TrueNAS | `192.168.1.211` | Confirmed NAS address |
| Raspberry Pi (`raspberrypi`) | `192.168.1.201` | Confirmed address |
| Pi-hole | `192.168.1.205` | Confirmed DNS service hosted on Proxmox |
| Primary WireGuard | `192.168.1.217` | Runs on Proxmox |
| Backup WireGuard | `192.168.1.201` | Runs on Raspberry Pi |

All confirmed device addresses belong to the current `192.168.1.0/24` LAN.

## Current Network Configuration

| Setting | Value |
|---|---|
| LAN subnet | `192.168.1.0/24` |
| Subnet mask | `255.255.255.0` |
| Default gateway | `192.168.1.1` |
| DHCP pool | `192.168.1.6` – `192.168.1.254` |
| DNS server | `192.168.1.205` |
| DNS service | Pi-hole on Proxmox |

## Historical Network Configuration

The LAN was migrated from `192.168.0.0/24` to `192.168.1.0/24` in September 2026.

| Historical Reference | Previous Value | Notes |
|---|---|---|
| Old LAN subnet | `192.168.0.0/24` | Previous network |
| Raspberry Pi | `192.168.0.201` | Replaced by `192.168.1.201` |
| Legacy Proxmox DNS | `192.168.0.203` | Old DNS configuration; check for remaining references |

Historical addresses may remain in old logs, backups, and configuration files. Verify any active configuration that still references the previous subnet before modifying it.
