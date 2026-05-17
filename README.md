# homelab-monitoring-stack

Ansible playbook and runbooks for deploying a complete monitoring stack on Proxmox VE.

## Stack

| Component | Version | Role |
|---|---|---|
| Ansible | latest | Deployment automation |
| Prometheus | 3.10.0 | Metrics collection |
| Node Exporter | 1.10.2 | Host metrics (OBS + Proxmox) |
| pve_exporter | latest | Proxmox API metrics |
| Grafana | latest | Visualization |
| Alertmanager | 0.27.0 | Alert routing |

## Architecture

```
Proxmox VE 9.1 (172.29.25.30)       Monitoring VM / OBS (172.29.25.29)
├── Node Exporter :9100         →    ├── Prometheus :9090
└── Proxmox API :8006           →    ├── pve_exporter :9221
                                     ├── Grafana :3000
                                     └── Alertmanager :9093
```

## Prerequisites

- Proxmox VE 9.1
- Debian 13 VM (monitoring node)
- Ansible installed on Proxmox
- SSH key without passphrase dedicated to Ansible

## Quick Start

```bash
# Clone the repo
git clone https://github.com/am6t3r4su/homelab-monitoring-stack.git
cd homelab-monitoring-stack

# Edit inventory
nano ansible/inventory.ini

# Deploy
ansible-playbook -i ansible/inventory.ini ansible/deploy_monitoring.yml
```

## Dashboards

Import in Grafana :
- **1860** — Node Exporter Full
- **10347** — Proxmox via Prometheus

## Documentation

See [docs/RUNBOOK.md](docs/RUNBOOK.md) for complete step-by-step guide including :
- Known issues and fixes
- Risk zones
- Manual configuration steps

## Author

**Olsen CAVALLERO** — Systems, Network & Security Administrator  
[Portfolio](https://github.com/am6t3r4su)

## License

MIT
