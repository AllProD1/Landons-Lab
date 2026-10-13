# Maintenance

## Routine checks to follow 

### Weekly or after major changes

- [ ] Check Proxmox node and guest health.
- [ ] Check storage availability and NFS mounts.
- [ ] Confirm DNS resolution from host and guests.
- [ ] Check monitoring alerts and failed services.
- [ ] Review backup job status.
- [ ] Check available disk space on Proxmox, NAS, and Docker hosts.
- [ ] Review pending updates and release notes before applying them.
- [ ] Commit documentation changes to Git.

### After a reboot or power outage

1. Confirm router, switch, and access points are online.
2. Confirm Proxmox management access.
3. Confirm TrueNAS is healthy and its exports are available.
4. Confirm NFS mounts are present on Proxmox.
5. Confirm dependent services, especially Jellyfin, start correctly.
6. Confirm DNS, WireGuard, and monitoring work from an appropriate client.
7. Check logs for failed units or repeated errors.

## Updates

- Read release notes for major OS, Proxmox, TrueNAS, and application upgrades.
- Ensure a recent, usable backup exists before risky updates.
- Update one layer at a time and verify it before proceeding.
- Avoid upgrading the host, storage platform, and critical network services simultaneously.
- Record the change, result, and rollback plan.

## Backups

Document actual backup destination. 
