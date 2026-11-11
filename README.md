# homelab-platform

Home lab for practicing senior infrastructure and AI-Ops work: CI/CD, LLMOps, monitoring, security and compliance. This is a lab, not a production system. Each project has design notes, configs and evidence in this repo.

## Current lab architecture

```mermaid
flowchart TB
  Internet((Internet)) --- FG["FortiWiFi 60E firewall"]
  FG --- LAN["Wired LAN"]
  FG --- WIFI["Staff Wi-Fi: WPA2-Enterprise"]
  LAN --- ESXI["VMware ESXi host"]
  ESXI --- DC["Windows Server 2025 DC: AD DS, DNS, AD CS, NPS"]
  LAN --- K8S["Kubernetes cluster: control plane and worker"]
  LAN --- SWARM["Docker Swarm: manager and worker"]
  SWARM --- APPS["Portainer, Uptime Kuma, Nextcloud, Ollama, Open WebUI"]
  DC -.->|"LDAPS"| FG
  FG -.->|"RADIUS"| DC
  WIFI -.->|"802.1X login"| DC
```

## Target CI/CD and LLMOps pipeline (Project 1, planned)

```mermaid
flowchart LR
  A["Git commit"] --> B["Lint and tests"] --> C["Build image"] --> D["Image scan"] --> E["LLM evaluation gate"] --> F["Push to registry"] --> G["Argo CD"] --> H["Staging"] --> I["Production"]
```

## Projects

| # | Project | Main folders | Status |
|---|---------|--------------|--------|
| 1 | CI/CD and LLMOps pipeline | pipelines, k8s, iac | Not started |
| 2 | Design docs, ADRs and mentoring material | docs/design, docs/adr | Not started |
| 3 | Monitoring and staged incidents | monitoring, docs/incidents | Not started |
| 4 | LLM gateway and agent security | docs/security | Not started |
| 5 | Compliance as code | docs/security, k8s | Not started |
| 6 | Platform roadmap | docs/roadmap | Not started |
| 7 | On-call simulation | docs/runbooks | Not started |

Already built outside this repo: Active Directory with LDAPS, an Enterprise CA, NPS (RADIUS) and WPA2-Enterprise Wi-Fi on a FortiWiFi.

## Repo layout

- docs/design, docs/adr, docs/runbooks, docs/incidents, docs/security, docs/roadmap
- pipelines, iac, k8s, monitoring

## Security practices

- No secrets in Git. A .gitignore blocks common secret files, and gitleaks scans the repo.
- Internal addresses and credentials are never published.

Secrets scanning: gitleaks runs as a pre-commit hook on every commit.
