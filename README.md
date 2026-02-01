# Wazuh Docker Project

Personal **SIEM / XDR laboratory** based on **Wazuh**, deployed using Docker.
The project demonstrates centralized log collection, event correlation,
and real-time security alerting across multiple operating systems.

Alerts are delivered to **Slack** using OpenSearch Alerting.

---

## 📦 Deployment

Single-node Wazuh deployment using Docker Compose.

```bash
cd docker/single-node
docker compose up -d
```

Access the web interface:
```https://localhost```

## 🖥️ Monitored systems

The following operating systems are integrated as Wazuh agents:

- **Linux:** Ubuntu 24.04.3 LTS
- **Windows:** Windows 11 Pro
- **macOS:** macOS 12.6.1

Each host forwards security events to the centralized Wazuh Manager.

## 🚨 Alerting & detections

Security monitoring is implemented using:

- Wazuh built-in rules (no custom decoders)
- OpenSearch Per Query Monitors
- Slack Incoming Webhooks for notifications

Implemented use cases
1. Linux
    - SSH brute-force detection
    - Sudo usage monitoring
    - Critical system file integrity monitoring (/etc/passwd, /etc/shadow, /etc/sudoers)
2. Windows
    - Failed logon detection (rule-based mapping of Event ID 4625)
    - Privilege escalation (Administrators group membership changes)
    - User account management (create, modify, enable, disable, delete)
3. macOS
    - Screen sharing authentication failures
    - Application permission changes (TCC / privacy events)
    - User login and session activity

All detections were tested and confirmed via Slack notifications.

## 📚 Documentation

Detailed technical documentation is available in the docs/ directory
and includes alert logic, screenshots, and verification steps.
```
docs/
├── agents/
│   ├── linux.md
│   ├── windows.md
│   └── macos.md
├── alerting/
│   ├── linux/
│   ├── windows/
│   └── macos/
```

### 🧩 agents

The `agents` section describes the **installation, configuration, and validation**
of Wazuh agents for each supported operating system:
- **Linux** — agent installation, registration with the manager, and basic status checks
- **Windows** — agent deployment, service verification, and initial connectivity
- **macOS** — agent installation, permissions, and operational validation

Each document includes step-by-step instructions and screenshots
to confirm that the agent is correctly installed and actively communicating
with the Wazuh manager.

### 🚨 alerting

The `alerting` section contains documentation for security alerting logic,
organized by operating system.  
Each subdirectory describes:
- alert purpose and detection logic
- configuration details
- verification steps and screenshots

## ✅ Project status

- ✔ Wazuh single-node deployment completed
- ✔ Linux, Windows, and macOS agents connected
- ✔ Alerting rules implemented and tested
- ✔ Slack notifications operational
- ✔ Documentation completed

This repository represents a complete, reproducible SIEM implementation
suitable for educational and demonstration purposes.
