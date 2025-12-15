# Homelab Infrastructure & Automation Project
## Overview

This homelab is a personal DevOps and Systems Administration playground designed for continuous learning, experimentation, and real-world infrastructure practice. It mirrors production-style environments while remaining fully self-hosted and rebuildable.

# Primary use cases:
- Hosting business web services securely via Cloudflare Tunnel
- Providing remote access to a personal file server
- Monitoring system performance, metrics, and logs
- Practicing container orchestration, automation, and CI/CD
- Implementing network segmentation and security controls

My technical focus centers on DevOps, Linux systems administration, monitoring/metrics, and networking.

# Infrastructure Overview
The environment consists of a 4-node Proxmox VE cluster with additional bare-metal and workstation systems. All hardware is refurbished and upgraded with SSD/NVMe storage, additional RAM, and improved cooling.
## Proxmox VE Cluster
### pveBlack (Lenovo ThinkCentre 710 MT)
- 500GB HDD, 500GB SSD, 500GB NVMe
- 16GB RAM, Intel i5 (4-core)
- Hosts: Proxmox VE, Primary Proxmox Backup Server

### pveRed (Dell OptiPlex 3020)
- 500GB HDD
- 16GB RAM, Intel i5 (4-core)
- Hosts: Proxmox VE

### pveGreen (Dell Inspiron 3650)
- 1TB HDD
- 500 GB SSD
- 16GB RAM, Intel i5 (4-core)
Hosts: Proxmox VE, Secondary PBS instance (synced from pveBlack)

## Bare Metal Servers
### debGold (Toshiba Satellite S55T)
- 500GB SSD, 16GB RAM, Intel i7 (8-core)
Debian Server (bare metal)

### debBlue (Gateway 557)
- 250GB SSD, 8GB RAM, Intel i5 (4-core)
Debian Server (bare metal)

## Workstations / Clients
- HP Pavilion G7 – Debian Linux workstation, RDP client
- Dell Latitude 5491 (Windows 11 Dev Laptop) – Docker Desktop, VS Code
- MacBook Pro A1506 – Debian Desktop with i3 WM, RDP client
- MacBook Pro (2011) – Legacy macOS system

All systems are connected through a managed switch with ongoing VLAN segmentation work.

# Key Services & Platforms
## Core Technologies
- Proxmox Backup Server (2 VM-based instances)
- Docker containers:
- NGINX, Prometheus, Grafana, MySQL, Python services
- Kubernetes
- K3s: 3-node cluster (public-facing via Cloudflare Tunnel)
- kubeadm-based Kubernetes: 5-node cluster (public-facing)
- Grafana + Prometheus
- Metrics from systemd, Docker, Python scripts, and MySQL
- Heimdall – Service dashboard
- Jellyfin – Personal media server
- Cloudflare Tunnel – Secure external access without port forwarding
- Tailscale – Remote SSH and file access
- LAMP stacks – Legacy website hosting
- ELK Stack – Deployed on bare metal for centralized log ingestion and analysis, collecting system, network, and security-related logs to support troubleshooting, visibility, and future SIEM-style workflows
- OPNsense – VLAN routing and firewall services
- Ansible – Daily maintenance and log-collection playbooks
- Jenkins – Automates Ansible workflows
- Vaultwarden (LXC) – Credential storage
- Restic – Systemd-driven backups from bare metal to file server

## File Sharing
- Samba-based file server, accessible securely via Tailscale

## Automation & Scripting
Automation is a core focus of this project, emphasizing repeatability and recovery.

#### Bash Scripts
- docker-containerd.sh – Docker + containerd installation
- kube-install.sh – Docker + Kubernetes tooling (kubeadm, kubelet, kubectl)
- docker-kube-deploy.sh – Deploys updated web content to Kubernetes pods
- lamp_install.sh – LAMP stack provisioning
- prometheus-monitor.sh – Auto-configures Prometheus on new VMs
- initial-git-setups.sh – SSH keys and repo initialization
- port_scanner.sh – Nmap-based port scanner
- tailscale-*.sh – OS-specific Tailscale installers

### Additional Automation
- Automated full + incremental backups via PBS
- Daily motivational quote script sent to my partner (because not all automation has to be serious)

### Planned: Full migration toward Ansible-driven infrastructure-as-code.

### Networking
- Migration from flat network to VLAN-segmented architecture
- OPNsense configured as router-on-a-stick
- Planned CARP implementation for high-availability routing
- Encrypted external access via Cloudflare Tunnel and Tailscale

## Monitoring & Logging
### Grafana + Prometheus deployment
- Homelab servers and Proxmox nodes (Ubuntu Server VM)
- Custom Dashboards
- CPU usage and temperature
- Disk health, lifecycle, and temperature
- Memory utilization per node and VM

### ELK Stack
- Centralized log analysis 
- Authentication events
- System activity
- Network traffic

## Challenges & Lessons Learned
Problems Worked Through
- LVM – From intimidating to foundational
 -VLANs – Planned and executed a full Proxmox cluster network rearchitecture, including hardware role realignment and VLAN segmentation, using systematic VM backup/restore workflows to achieve zero data loss and no significant downtime- Cloudflare Tunnels – DNS, HTTPS, and edge routing concepts
- Systemd – Powerful, unforgiving, and worth mastering
- Kubernetes – Complex, humbling, and deeply educational

## Key Takeaway
You never understand a tool the first time. Rebuilding, breaking, and documenting is what turns exposure into skill.

### Future Plans
-  Finalize VLAN migration -HW dependent,current switch can't manage CARP
-  Migrate ELK stack into K3s
-  Expand PBS coverage (Windows + additional bare metal)
-  Deepen Ansible and Python automation
-  Advance Docker and Kubernetes proficiency

## Canonical Portfolio Project (In Progress)
This homelab also serves as the foundation for a **canonical portfolio project** focused on integrating modern infrastructure with LLM-driven workflows.
### Current work includes:
- Self-hosted LLM infrastructure (Ollama-based) running on Debian bare metal
- Secure containerized deployment via Docker Compose
- CLI-driven interaction for system-aware task execution
- Ongoing design of a FastAPI-based service layer for controlled LLM access
### The goal of this project is to demonstrate:
- Practical LLM integration into Linux systems
- Secure service boundaries and automation workflows
- Infrastructure-first AI experimentation aligned with real DevOps practices

### Contact
- GitHub: @justynlarry
- LinkedIn: linkedin.com/in/justynlarry

### Built, not bought. Learned by breaking.
