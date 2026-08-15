# Antigravity Skills & CVE Testbeds Collection

A curated collection of modular skills, automation runbooks, defensive tooling, and reproducible CVE benchmark testbeds for Google Antigravity and AI coding assistants.

---

## 📂 Repository Structure

```text
julwright/-skills/
├── README.md
├── cve-fingerprint-lab/              # The core Antigravity skill
│   ├── SKILL.md
│   ├── scripts/
│   │   ├── lookup_cve.py             # Query vulnerability databases (OSV/CIRCL)
│   │   ├── deploy_lab.py             # Loopback Docker sandbox orchestrator
│   │   ├── generate_fingerprint.py   # Nuclei, Suricata, Sigma rule generator
│   │   ├── simulate_telemetry.py     # Multi-tier forensic log synthesizer
│   │   ├── export_cve_test.py        # Automated test package generator & git sync
│   │   └── teardown_lab.py           # Container cleanup utility
│   ├── references/
│   │   ├── cve_reproduction_playbook.md
│   │   ├── containeryard_and_sources.md
│   │   ├── fingerprint_methodology.md
│   │   └── isolation_guidelines.md
│   └── examples/
└── cve-tests/                         # Dedicated benchmark packages for tested CVEs
    └── GeoServer-jsonArrayContains/  # Sample testbed package
        ├── README.md                 # Threat summary, affected versions, IoCs
        ├── docker-compose.yml        # Quarantined sandbox definition
        ├── rules/                    # Nuclei, Suricata, Sigma, and WAF rules
        └── logs/                     # Multi-tier access, error, auditd, and Falco logs
```

---

## 🛠️ How to Export & Push a New CVE Test

When you research and test a new CVE, generate and push its dedicated package with one command:

```bash
python cve-fingerprint-lab/scripts/export_cve_test.py \
  --cve "CVE-2023-46604" \
  --image "vulhub/activemq:5.11.1" \
  --port "8161:8161" \
  --git-push
```

This automatically:
1. Fetches advisory metadata and affected version matrices.
2. Creates the isolated `docker-compose.yml`.
3. Scaffolds detection rules (`rules/nuclei.yaml`, `rules/suricata.rules`, `rules/sigma.yml`, `rules/nginx_waf.conf`).
4. Generates multi-tier telemetry logs (`logs/access.log`, `logs/application_error.log`, `logs/auditd.log`, `logs/falco_alert.json`).
5. Generates the comprehensive `README.md`.
6. Commits and pushes the package to `cve-tests/<CVE-NAME>/` on GitHub.
