Headless Linux Network Gateway & DNS Security Node

A performance-focused, headless home lab infrastructure project built on low-power ARM architecture. This system functions as a secure, local edge routing gateway, recursive DNS sinkhole, and encrypted private network bridge. 

The entire configuration state is tracked here under version control to enforce infrastructure transparency and configuration reproducibility.

---

## Architecture Overview

.[ Local Home Network Client Devices ]│▼ (Port 53: DNS Traffic)┌─────────────────────────────────────────────────────────────────────────────┐│ RASPBERRY PI GATEWAY NODES                                                  ││                                                                             ││  ┌───────────────────────────┐         ┌─────────────────────────────────┐  ││  │   AdGuard/Pi-hole Engine  │ ──────> │    NetworkManager Routing       │  ││  │  (Domain Filtering & DHCP)│         │ (Traffic Forwarding / Firewall) │  ││  └───────────────────────────┘         └─────────────────────────────────┘  ││                                                         │                   │└─────────────────────────────────────────────────────────┼───────────────────┘▼┌───────────────────────────────────┐│       Tailscale VPN Mesh          ││  (WireGuard Encrypted Overlay)    │└───────────────────────────────────┘
---

## Key Technical Core Capabilities

* **Automated DNS Sinkholing & Ingress Filtering:** Orchestrates local DNS queries utilizing granular upstream filtering blocklists to eliminate telemetry trackers, malicious domains, and network-wide advertisements.
* **Encrypted Network Overlay:** Runs a zero-configuration **Tailscale** overlay network (powered by the **WireGuard** protocol), configuring the headless host to behave as a secure remote ingress gateway to local infrastructure without relying on open incoming public ports.
* **Headless Infrastructure Operation:** Maintained and configured exclusively via terminal CLI streams over SSH, utilizing lean Linux system dependencies for resource efficiency and 24/7 runtime durability.
* **State Management via Version Control:** System configurations, network deployment connection profiles, and package structures are continuously managed under Git, preventing configuration drift and simplifying node migrations.

---

## Repository File Structure

The configurations collected in this backup repository target the following core infrastructure frameworks on Debian/Pi OS:

* `/network/` - Modern **NetworkManager** infrastructure profile properties, interface state tracking sheets, and local interface bonding definitions. *(Note: plain-text security passwords and pre-shared keys have been safely scrubbed from source templates).*
* `/pihole/` - Upstream server allocations, custom local domain routing sheets, conditional forwarders, and core DNS block configurations.
* `/tailscale/` - System environmental configurations and routing parameter templates enabling remote node traffic encapsulation.

---

## 🚀 Future Roadmap & Scaling Target

This edge-routing repository forms the initial baseline for a multi-layered infrastructure layout. The next phase of expansion shifts this logic into an isolated, high-availability architecture on a bare-metal hypervisor:

1. **Bare-Metal Virtualization:** Deploying an open-source **Proxmox VE** Type-1 Hypervisor on dedicated x86 hardware.
2. **Dedicated Enterprise Routing:** Offloading edge firewall handling and network segmentation to an explicit virtualized **OPNsense** operating system backed by physical Intel multi-port PCIe NIC hardware.
3. **Identity & Client Management:** Spinning up segmented virtual machines running **Red Hat Enterprise Linux (RHEL)** for containerized workloads and **Windows Server Evaluation** to construct a localized Active Directory Domain Controller domain environment.
