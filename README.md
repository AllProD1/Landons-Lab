# Landon's Lab

> Documentation for my homelab infrastructure, services, networking, and recovery procedures.

This repository is the operational notebook for my homelab. It records how the environment is organized, what runs where, how systems depend on one another, and how to troubleshoot common failures.

> [!IMPORTANT]
> This documentation is a living draft. Entries marked **Verify** are based on historical notes and should be checked against the live system before being used for changes.

## Documentation

| Area | Description |
|---|---|
| [Architecture overview](overview.md) | Major systems, dependencies, and conceptual diagram |
| [Network topology](network-topology.md) | Logical network layout and migration notes |
| [Hardware inventory](inventory.md) | Hosts, hardware, and power protection |
| [Proxmox VE](proxmox.md) | Host operations and useful diagnostic commands |
| [VM and container inventory](guests.md) | Guest IDs, roles, and verification status |
| [Storage and NFS](storage-and-nfs.md) | TrueNAS exports, mounts, and Jellyfin dependencies |
| [IP address plan](ip-addresses.md) | Current and historical network addresses |
| [DNS](dns.md) | Pi-hole and resolver migration notes |
| [WireGuard](wireguard.md) | VPN verification and troubleshooting |
| [Maintenance](maintenance.md) | Routine checks and post-reboot checklist |
| [Troubleshooting](troubleshooting.md) | Historical incidents and investigation steps |

## Infrastructure at a glance

|Component|Known role                                                                                  |Documentation note                                                                                                             |
|---------|--------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------|
|pve3     |Primary Proxmox VE host running on an Intel NUC8i5BEHS with an Intel Core i5-8260U (4 cores)| Dedicated Hypervisor                  |
|TrueNAS  |NAS providing network storage for homelab services and media                                | Dedicated NAS             |

## Status labels

- **Verified** — checked against the live configuration.
- **Verify** — historical or incomplete information; confirm before relying on it.
- **Planned** — intended design, not confirmed as implemented.

## Documentation workflow

When changing the infrastructure, update the related page in the same commit. Record the date, what changed, how it was verified, and a rollback or recovery path when relevant.
