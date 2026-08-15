# Antigravity Skills Collection

A curated collection of modular skills, automation runbooks, and offensive/defensive tooling for Google Antigravity and AI coding assistants.

---

## Available Skills

### 1. [`cve-fingerprint-lab`](./cve-fingerprint-lab/)
**Automated CVE Research, Quarantined Docker Lab Orchestration & Defensive Fingerprinting**

* **Advisory & Image Intelligence (`lookup_cve.py`):** Queries open vulnerability databases (OSV.dev, CIRCL) to map software versions to Docker Hub / Vulhub container images.
* **Isolated Sandbox Provisioning (`deploy_lab.py`):** Generates resource-throttled Docker compose sandboxes bound strictly to local loopback (`127.0.0.1`).
* **Detection Rule Synthesis (`generate_fingerprint.py`):** Probes live container endpoints and synthesizes multi-layer defensive rules:
  * **Nuclei Scanner Templates (`.yaml`)**
  * **Suricata / Snort NIDS Rules (`.rules`)**
  * **Sigma SIEM Access Log Queries (`.yml`)**
  * **WAF / Reverse Proxy Filters**
* **Clean Teardown (`teardown_lab.py`):** Dismantles containers, networks, and prunes temporary volumes.
* **Master Lifecycle Playbook:** Includes end-to-end procedures and real-world zero-day case studies (e.g. GeoServer `jsonArrayContains`).

---

## Installation & Workspace Setup

To use these skills in any Antigravity workspace:
1. Clone or copy the desired skill directory into your project's `.agents/skills/` folder:
   ```bash
   mkdir -p .agents/skills/
   cp -r cve-fingerprint-lab .agents/skills/
   ```
2. The Antigravity agent will automatically discover the skill and activate its runbooks when relevant tasks or CVE investigations are requested.
