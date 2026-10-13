# Virtual Machines and Containers

**Source:** Proxmox guest list and guest configuration capture. Status and resource values are a point-in-time snapshot; verify live state before operational changes.

## Virtual machines

| VMID | Name | Purpose | Status | IPv4 | vCPU | Memory | Disk |
|---:|---|---|---|---|---:|---:|---:|
| 109 | `Home Assistant` | Home automation | Running | `192.168.1.219` | 2 | 2 GiB | 32 GiB |

Home Assistant's virtual NIC is attached to `vmbr0`.

## LXC containers

| CTID | Hostname | Known purpose | IPv4 from config | Status | vCPU | Memory | Root disk |
|---:|---|---|---|---|---:|---:|---:|
| 100 | `wireguard` | WireGuard VPN | `192.168.1.217` | Running | 2 | 512 MiB | 8 GiB |
| 102 | `Pi-Hole` | Pi-hole DNS | `192.168.1.205` | Running | 1 | 512 MiB | 8 GiB |
| 103 | `pi-hole2` | Secondary Pi-hole instance | `192.168.1.206` | Running | 1 | 512 MiB | 6 GiB |
| 104 | `homepage` | Homepage dashboard | `192.168.1.204` | Running | 2 | 4 GiB | 6 GiB |
| 105 | `portainer` | Portainer / container management | `192.168.1.208` | Running | 2 | ~4.2 GiB | 40 GiB |
| 106 | `nginx` | Nginx service / proxy (exact role to verify) | `192.168.1.209` | Running | 2 | 2 GiB | 8 GiB |
| 107 | `rustdeskserver` | RustDesk server | `192.168.1.210` | Running | 2 | 512 MiB | 2 GiB |
| 108 | `n8n` | Workflow automation | `192.168.1.218` | Running | 2 | 2 GiB | 10 GiB |
| 110 | `jellyfin` | Media server | `192.168.1.212` | Running | 2 | 2 GiB | 30 GiB |
| 111 | `octoprint-SV6` | OctoPrint instance | `192.168.1.213` | Stopped | 1 | 1 GiB | 4 GiB |
| 112 | `octoprint-SV1` | OctoPrint instance | `192.168.1.214` | Stopped | 1 | 1 GiB | 4 GiB |
| 113 | `pterodactyl-panel` | Pterodactyl Panel | `192.168.1.215` | Running | 4 | 8 GiB | 50 GiB |
| 114 | `pterodactyl-wings` | Pterodactyl Wings | `192.168.1.216` | Running | 4 | ~7.9 GiB | 15 GiB |

The addresses above come from Proxmox LXC network configuration, not an independent ping or DHCP-reservation check. The values should be reconciled with the router and live guest state. Disk figures are configured virtual/root-disk capacities, not actual data usage.

## Startup behavior

All listed LXC containers (except CT 111 and CT 112) and VM 109 have `onboot: 1`. CT 100 has startup order 1 and a 10-second startup delay. No explicit startup order was shown for the other guests.

Stopped guests configured to not start on boot:

- CT 111 — OctoPrint-SV6
- CT 112 — OctoPrint-SV1

## Dependencies and follow-up

- **Jellyfin (CT 110):** receives three host NFS mount points: `/mnt/jellyfin/media1`, `/mnt/jellyfin/media2`, and `/mnt/jellyfin/media3`. Verify the mounts before starting Jellyfin after a NAS outage.
- **DNS:** the Proxmox host uses `192.168.1.205`, which is configured for CT 102 (Pi-hole).

## Useful commands

On the Proxmox host:

```bash
qm list
pct list
qm config 109
pct config 100
pct config 102
```
