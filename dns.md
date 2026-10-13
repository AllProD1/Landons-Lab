## DNS Infrastructure

Pi-hole provides DNS filtering and local DNS resolution for the homelab. Three Pi-hole instances are deployed across the Proxmox server and Raspberry Pi, each serving a distinct role.

### Pi-hole Instances

| Role | IP Address | Host Platform | Description |
|---|---|---|---|
| Primary DNS | `192.168.1.205` | Proxmox VE (`pve3`) | Primary DNS server for the local network |
| VPN DNS | `192.168.1.206` | Proxmox VE (`pve3`) | Dedicated DNS server for VPN clients |
| Backup DNS | `192.168.1.201` | Raspberry Pi | Backup Pi-hole instance for DNS redundancy |

### DNS Configuration

- **Local network:** Uses `192.168.1.205` as its primary DNS server.
- **VPN clients:** Use `192.168.1.206` for DNS resolution and filtering.
- **Backup DNS:** The Raspberry Pi at `192.168.1.201` provides a separate Pi-hole instance for backup DNS service.

### Infrastructure Notes

- The primary and VPN-specific Pi-hole instances run on the Proxmox VE host `pve3`.
- The backup Pi-hole runs independently on the Raspberry Pi, providing DNS redundancy if the Proxmox host becomes unavailable.
