# Proxmox VE

## Overview

`pve3` is the primary Proxmox VE host for the homelab. It provides virtualization for infrastructure services, application containers, media services, and Home Assistant.


## Host Hardware and Software

| Property | Value |
|---|---|
| Hostname | `pve3` |
| Hardware | Intel NUC8i5BEHS |
| CPU | Intel Core i5-8260U |
| CPU topology | 4 cores / 8 threads |
| Memory | 16 GiB |
| Boot/storage drive | 240 GB TeamGroup SSD |
| Operating system | Debian GNU/Linux 13 (Trixie) |
| Proxmox VE | 9.2.0 |
| Proxmox manager | 9.2.20 |
| Kernel | `7.0.14-17-pve` |
| Architecture | x86-64 |

Software versions and hardware details reflect the captured system information and should be rechecked after upgrades or hardware changes.

## Network Configuration

| Setting | Value |
|---|---|
| Host management IP | `192.168.1.222/24` |
| Linux bridge | `vmbr0` |
| Bridge port | `nic0` |
| Default gateway | `192.168.1.1` |
| DNS server | `192.168.1.205` |
| Search domain | `johnson.local` |
| LAN subnet | `192.168.1.0/24` |
| Wi-Fi interface | `wlp0s20f3` — down at capture |

The host management address is configured on `vmbr0`, which bridges traffic to the physical network interface `nic0`.

The host uses Pi-hole at `192.168.1.205` for DNS. See the network documentation for the overall LAN design and address assignments.

## Virtual Machines and Containers

VM and LXC details are maintained in the separate [VM and container inventory](guests.md) document.

That inventory includes:

- VMIDs and CTIDs, names, and purposes
- Guest IP addresses and resource allocations
- Configured startup behavior
- Guest-specific settings and dependencies

### Guest Management Commands

Run these commands on the Proxmox host:

```bash
qm list
pct list
qm config 109
pct config 100
pct config 102
```

Replace the example IDs with the relevant VMID or CTID when inspecting another guest.


## Operational Notes

- Proxmox is the central virtualization platform for the homelab.
- The host uses a single local SSD for the operating system and virtual disks.
- Jellyfin depends on TrueNAS NFS exports mounted on the Proxmox host.
