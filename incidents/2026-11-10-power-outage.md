# Incident: Power outage — host did not auto-start

- **Date:** Tuesday, November 10, 2026 (daytime)
- **Impact:** All home lab services down until the host was powered on manually
- **Duration:** Power was off during the day for electrical repairs; services stayed down until manual intervention (exact times not recorded)

## Summary

Power to the house was shut off during the day for electrical repairs.
When power returned, the Proxmox host (Lenovo ThinkCentre M80q) stayed
off — its BIOS was still on the factory default for power loss, which is
to stay off. Nothing was broken; the host simply never got the instruction
to turn itself back on.

## Timeline

- Daytime: power shut off for repairs.
- Power restored: host stayed off; all services (DNS, media server, dashboard) down.
- I powered the host on manually at the machine.
- On boot, Proxmox started the media server VM and Pi-hole container automatically.
- Verified: Uptime Kuma showed 18/18 services up; Pi-hole answering DNS again.

## Root cause

The BIOS "After Power Loss" setting was never configured — factory default
is "stay off." The autostart chain underneath it (VMs and containers set to
start at boot) was fine; it just never got the chance to run.

## What went well

- Once the host was on, everything came back on its own — no manual service restarts needed.
- Monitoring (Uptime Kuma) gave a fast, clear all-clear: 18/18.

## What went wrong

- No automatic recovery: a daytime outage meant services stayed down until someone was home to press the power button.
- The BIOS setting was an untested assumption — I believed the host would come back on its own, but had never verified it.

## Action items

- [ ] Set BIOS Power > Automatic Power On > After Power Loss to "Power On."
- [ ] Verify Pi-hole container is set to start at boot in Proxmox (media server VM already is; dev VM intentionally stays off).
- [ ] Test recovery after the next maintenance window: cut power, confirm the host and all services return without touching it.
