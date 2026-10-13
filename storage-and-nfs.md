# Storage and NFS

## Design

The Proxmox host `pve3` uses local LVM-thin storage for guest disks and mounts three NFS exports for media storage. The exports were reported from TrueNAS at `192.168.1.211`; 

| Proxmox host mount point | NFS export | Consumer |
|---|---|---|
| `/mnt/jellyfin/media1` | `192.168.1.211:/mnt/media1` | Jellyfin CT 110 |
| `/mnt/jellyfin/media2` | `192.168.1.211:/mnt/media2` | Jellyfin CT 110 |
| `/mnt/jellyfin/media3` | `192.168.1.211:/mnt/media3` | Jellyfin CT 110 |

Jellyfin's LXC configuration passes the host paths into the container at matching paths using `mp0`, `mp1`, and `mp2`.

## TrueNAS storage

TrueNAS at `192.168.1.211` provides NAS and media storage to Proxmox host `pve3`.

- **Hardware:** AMD Ryzen 3 3200G, 16 GB RAM
- **Version:** TrueNAS 25.10.7 — Goldeye

### Storage pools

| Pool | Layout | Usable capacity | Used |
|---|---|---:|---:|
| `biggy` | RAIDZ1, 5-wide | 3.51 TiB | 13.4% |
| `media1` | Single disk | 1.76 TiB | 52.1% |
| `media2` | Single disk | 445.75 GiB | 80.0% |
| `media3` | Single disk | 445.75 GiB | 32.9% |

The `media1`, `media2`, and `media3` pools provide the NFS exports mounted by Proxmox and passed to Jellyfin LXC 110. These single-disk pools have no disk redundancy.

**Capacity note:** `media2` was at 80% usage with approximately 89 GiB available at the time of capture. Monitor capacity and plan for additional space as needed.

`biggy` is an SMB share for the network with redundancy for preserving important data.

Pool usage and health figures reflect the dashboard at the time of documentation and should be rechecked periodically.

## Persistent mounts

The following entries were present in `/etc/fstab`:

```fstab
192.168.1.211:/mnt/media1 /mnt/jellyfin/media1 nfs defaults,_netdev,soft,timeo=150,retrans=5,noatime,nofail 0 0
192.168.1.211:/mnt/media2 /mnt/jellyfin/media2 nfs defaults,_netdev,soft,timeo=150,retrans=5,noatime,nofail 0 0
192.168.1.211:/mnt/media3 /mnt/jellyfin/media3 nfs defaults,_netdev,soft,timeo=150,retrans=5,noatime,nofail 0 0
```

The observed mounts were active and using NFSv4.2 over TCP. The `_netdev` option marks them as network mounts. `nofail` allows boot to continue if a share cannot be mounted.

**Caution:** `soft` mounts can return I/O errors to applications during server/network problems. Review this trade-off for the workload rather than blindly copying these options to another system.

## Proxmox local storage

| Storage | Type | Capacity | Used | Available | Utilization |
|---|---|---:|---:|---:|---:|
| `local` | Directory | 65.4 GiB | 36.4 GiB | 29.0 GiB | 55.69% |
| `local-lvm` | LVM-thin | 129.8 GiB | 114.1 GiB | 15.7 GiB | 87.91% |

At the time of capture, LVM-thin data allocation was 87.91% and metadata allocation was 4.06%. Monitor data usage before growing disks or creating guests. The root filesystem was an XFS volume of about 66 GiB, 56% used.


