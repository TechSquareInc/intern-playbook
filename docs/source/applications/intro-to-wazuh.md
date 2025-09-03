# Intro to Wazuh

*Wazuh is a free and open-source security platform primarily used for threat detection and incident response.*

---

## What is Wazuh?

Wazuh is an open-source security monitoring platform designed for securing data assets across diverse environments including on-site, virtualized, containerized, and cloud-based systems. It is commonly used in security operation centers or high performance computing environments to gain visibility into system activity and detect suspicous behavior. Wazuh has a variety of different cababilities including:
- Intrusion detection (or HIDS - Host Intrusion Detection Software)
- Log data analysis and correlation
- File integrity monitoring
- Vulnerability detection
- Compliance monitoring
- Incident response

Wazuh is most commonly referred to as a **SIEM** (System, Information, and Event Management) and **XDR** (Extended Detection and Response) solution to help monitor systems, detect threats, and ensure compliance with industry standards. It collects logs from systems, analyzes them for suspicious activity, and generates alerts when it detects potential issues from attacks, system misconfigurations, or unusual system behavior.

### Wazuh Architecture

Wazuh follows a client-server distributed architecture made up of components that work together to collect, process, and analyze security data.


|**Component**|**Description**|
|:------------|:--------------|
|Agents|<ul><li>Installed on monitored endpoints (servers, workstations, cloud instances)</li><li>Collect logs, system information, file integrity data, and more</li><li>Perform local analysis and forward relevant data to the Wazuh server</li><li>Lightweight and cross-platform (Linux, Windows, MacOS)</li></ul>|
|Wazuh Server|<ul><li>Acts as the central processing hub</li><li>Recieves data from agents</li><li>Performs deeper analysis of logs and events</li><li>Generates alerts and manages agents</li><li>Can also ingest logs from agentless sources</li></ul>|
|Indexer|<ul><li>Stores security events and alerts</li><li>Enables search and analysis of historical data</li><li>Scales to handle large amounts of data from many agents</li></ul>|
|Visualization (Wazuh Dashboard)|<ul><li/>Web-based user interface</li><li>Displays security alerts, dashboards, compliance reports, and system status</li><li>Allows users to drill down into specific events and customize dashboards</li></ul>|


### Wazuh Core Features

1. **Log Analysis:** Centralized visibility and correlation
2. **Intrusion Detection:** Detects suspicious activty on endpoints
3. **File Integirty Monitoring:** Protects sensitive files and detects tampering
4. **Rootkit Detection:** Scans for hidden or malicious processes at the kernel level
5. **Vulnerabilty Detection:** Reduces risk exposure
6. **Active Incident Response:** Automates containment actions of threat detections
7. **Compliance Monitoring:** Evaluates system settings for compliance with industry standards like PCI DSS, HIPAA, GDPR, NIST frameworks, CIS Benchmarks, and MITRE Attack frameworks

## Installation

The easiest way to get Wazuh up and rolling for exploration is to use the Wazuh installation assistant.
1. Download and run the Wazuh installation assistant:
```bash
curl -sO https://packages.wazuh.com/4.12/wazuh-install.sh && sudo bash ./wazuh-install.sh -a
```

2. Once finished, an output with credentials and ways to access the dashboard will show in the output:
```bash
INFO: --- Summary ---
INFO: You can access the web interface https://<WAZUH_DASHBOARD_IP_ADDRESS>
    User: admin
    Password: <ADMIN_PASSWORD>
INFO: Installation finished.
```

At this point, you should be able to open your browser and log into the Wazuh dashboard to begin exploring the platform.

> **Note:** When accessing the dashboard for the first time, the browser shows a warning message stating the certficate is not trusted by a trusted authority. This is expected, and you can choose to accept the certificate anyway, or alternatively configure the system to use a certificate from a trusted authority.

### Adding an Agent
Up to this point, this installation will allow you to explore the Wazuh dashboard, and become more familair with its features. If you are curious about adding additional endpoints to monitor, follow the steps laid out in the Wazuh [adding an agent](https://documentation.wazuh.com/current/installation-guide/wazuh-agent/wazuh-agent-package-linux.html) documentation.

## Wazuh Tutorials
- [Crash Course](https://documentation.wazuh.com/current/installation-guide/wazuh-agent/wazuh-agent-package-linux.html): An in-depth and complete guide to using Wazuh, configuring endpoints, and exploring its features. This tutorial also walks through deploying Wazuh with docker. 
- [Creating Dashboards](https://www.youtube.com/watch?v=QrcAhd5P7xw): Wazuh offers the ability to create different dashboards that highlight certain or specific pieces of log data. This tutorial walks you through how to do that.

---
## Resources
- [Quickstart](https://documentation.wazuh.com/current/quickstart.html): Steps to get starting with Wazuh quick isntallation guide. 
- [Adding an Agent(Linux)](https://documentation.wazuh.com/current/installation-guide/wazuh-agent/wazuh-agent-package-linux.html): Steps to deploy the Wazuh agent on Linux endpoints.
- [Wazuh Architecture](https://documentation.wazuh.com/current/getting-started/architecture.html): A run down of how Wazuh works as a distributed system.
- [Getting Started](https://documentation.wazuh.com/current/getting-started/index.html): Getting started with Wazuh.
- [Overview of Wazuh](https://wazuh.com/platform/overview/): Overview of Wazuh with feature descriptions.
