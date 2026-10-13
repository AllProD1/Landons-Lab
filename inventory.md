# Hardware Inventory

**Status:** Updated with currently confirmed hardware and infrastructure details. Some specifications and service assignments remain to be verified.

## Physical Hardware

| System | Hardware | Operating System / Role | Notes |
|---|---|---|---|
| `pve3` | Intel NUC8BEH, 16 GB RAM, SATA SSD | Proxmox VE | Primary low-power virtualization host. |
| TrueNAS | AMD Ryzen 3 3200G, 16 GB RAM, no discrete GPU | TrueNAS | Dedicated physical NAS server. Storage configuration, TrueNAS version, network address, and services to be documented. |
| `raspberrypi` | Raspberry Pi 3 Model B  | Debian GNU/Linux 13 (Trixie) | Connected to the NETGEAR GS605 switch. Exact model, RAM, storage, IP address, and utility services to be confirmed. |
| Router | Ubiquiti UniFi Dream Machine 7 | Primary router and network gateway | Receives 1 Gbps fiber internet through the ONT. Connected to an EcoFlow battery backup. |
| Network switch | NETGEAR GS605 | Wired LAN connectivity | Connects the Proxmox NUC, dedicated TrueNAS server, and Raspberry Pi to the LAN. |
| Fiber ONT | Model to be confirmed | Fiber internet termination | Receives the ISP's fiber connection and provides the connection to the UniFi Dream Machine 7. Connected to battery-backed power. |
| UPS | APC Back-UPS BX1000M, 1000 VA / 600 W | Power protection | Provides backup power for the homelab equipment. |
| Battery backup | EcoFlow Delta 3 | Backup power | Provides backup power for the UniFi Dream Machine 7. 1024Wh Capacity |

## Network Infrastructure

### Internet Connection

- **ISP connection:** 1 Gbps fiber internet.
- **Fiber termination:** Optical Network Terminal (ONT).
- **Primary router:** Ubiquiti UniFi Dream Machine 7.
- **Wired switching:** NETGEAR GS605.

### Wired Connections

The following systems are connected to the NETGEAR GS605:

- Proxmox VE host (`pve3`)
- Dedicated TrueNAS server
- Raspberry Pi (`raspberrypi`)

The UniFi Dream Machine 7 serves as the primary router and gateway. 

## Power Protection

The homelab uses two backup-power systems:

- **APC Back-UPS BX1000M:** Provides backup power for the homelab equipment and the Fiber ONT.
- **EcoFlow DELTA 3 battery backup:** Provides backup power for the UniFi Dream Machine 7.

The exact division of equipment between the APC UPS and EcoFlow, their runtime under load, and any automated shutdown procedures should be verified.

## Operating System Details

### Proxmox VE — `pve3`

- Hardware: Intel NUC8BEH
- Memory: 16 GB RAM
- Storage: SATA SSD
- Proxmox VE version: 9.2.20
- Guest VMs and containers: 100-114

## TrueNAS — Dedicated NAS

- **Hardware:** AMD Ryzen 3 3200G
- **Memory:** 16 GB RAM
- **Discrete GPU:** None
- **TrueNAS version:** 25.10.7 — Goldeye
- **Storage pools:**
  - **biggy:** 480.9 GiB / 3.5 TiB (13%)
  - **media1:** 937.8 GiB / 1.8 TiB (52%)
  - **media2:** 356.6 GiB / 445.8 GiB (80%)
  - **media3:** 146.6 GiB / 445.8 GiB (33%)

### Raspberry Pi 3 — `raspberrypi`

- Model: Raspberry Pi 3 Model B Rev 1.2
- Operating system: Debian GNU/Linux 13 (Trixie)
- Kernel: `6.18.39+rpt-rpi-v8`
- Architecture: `arm64`
- RAM: 1 Gig
- SD card storage: 8 Gigs
- Utility and remote-access services: Pi-Hole and Wireguard

## Decommissioned Hardware

The following systems are no longer part of the active homelab inventory:

- **AI box:** Intel Core i7-7700, NVIDIA RTX 2060 Super, 16 GB RAM. Fully decommissioned.
- **Other AI-capable PC:** Ryzen 5 5600X, NVIDIA RTX 3060, 32 GB RAM. Removed from the active inventory.
- **Other PC:** Intel system with NVIDIA RTX 2070 and 16 GB RAM. Removed from the active inventory.

These systems are excluded from the active hardware inventory and are not considered part of the current infrastructure.
