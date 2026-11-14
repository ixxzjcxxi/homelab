# homelab
My home lab - Proxmox, media server, network docs, runbacks, and incident write ups
# Homelab

A home lab built for learning the skills behind data center operations:
Linux administration, networking, virtualization, monitoring, and
incident response — documented the way production work is documented.

## Hardware

| Host | Role | Specs |
| --- | --- | --- |
| Lenovo ThinkCentre M80q Gen 1 | Proxmox VE 9.2 host | i7-10700T, 16 GB RAM, 256 GB NVMe |
| 4 TB Seagate external drive | Media storage | Mounted at /mnt/media on the media VM |

## Network

- LAN: 192.168.1.0/24
- Proxmox host: 192.168.1.50:8006
- Pi-hole (LXC): 192.168.1.51 — network-wide DNS and ad blocking
- Media server (VM 101): 192.168.1.52
- Dev VM (VM 103): 192.168.1.53
- Remote access: Tailscale, media server as subnet router

## Services (media server, VM 101)

Jellyfin, Sonarr, Radarr, Prowlarr, qBittorrent, Seerr, Homepage,
Uptime Kuma, and a home dashboard I built from scratch in Flask.

## Runbooks

Step-by-step procedures in `runbooks/`.

## Incidents

Write-ups of real outages and what they taught in `incidents/`.
