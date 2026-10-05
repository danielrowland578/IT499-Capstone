# IT499-Capstone

# What is it?
Automated Endpoint Configuration Management Pipeline Capstone Presentation

# Who is in it?
Daniel Rowland / Jordan Puentes

# Description:
This capstone project addresses enterprise system deployment by constructing an Ansible control framework capable of automated zero-touch provisioning, domain integration, and security baseline enforcement across Linux and Windows systems.

# Overview
The Automated Cross-Platform Endpoint Provisioning and Configuration Management Framework establishes an automated lifecycle pipeline for enterprise environments. By integrating a network boot server with a centralized configuration management such as Ansible, the pipeline automates OS deployment through continuous security compliance across Debian Linux and Windows 11/Server hosts.

# Problem Statement:
Traditional IT operations rely on manual endpoint setup procedures that lead to bottlenecks and security risks:
  High Onboarding Overhead: Manually installing operating systems via USB installation media and configuring domain settings consumes up to 45–60 minutes per workstation.
  Inconsistent System Baselines: Differences in manual configuration create security vulnerabilities and compliance drift across endpoints.
  Siloed Identity Administration: Managing Linux local user accounts separately from Active Directory infrastructure fragments access policies and security group permissions.
  Configuration Drift: Unauthorized manual changes (e.g., stopping host firewall services or modifying local privileges) remain undetected without continuous state enforcement.

# Project goals and objectives
1. Eliminate manual bare-metal and virtual machine setup times using network PXE deployment.
2. Unify cross-platform configuration enforcement (Linux and Windows) under a single Infrastructure as Code (IaC) control node.
3. Enforce security compliance standards across all endpoints.

# Key Features:
1. Zero-Touch Provisioning Pipeline: Network boot sequence automatically triggers initial OS installation and registers hosts into the Ansible management inventory.
2. Role-Based Identity Mapping: Automatically assigns administrative privileges on Linux based on Active Directory group memberships (e.g., AD Domain Admins -> sudo rights).
3. Cross-Platform Firewall & Hardening Enforcement: Synchronized playbook deployment of host network filter rules across Linux and Windows systems.
4. Continuous Drift Remediation Engine: Scheduled cron jobs execute playbooks in check mode; any out-of-spec configurations trigger automated playbook runs to restore compliant baselines.

# System components
1. Debian 12 Control Node: Operates Ansible and coordinates execution across Linux (via SSH/OpenSSH) and Windows (via WinRM/PowerShell) endpoints.
2. Windows Server 2022 Active Directory Host: Handles domain identity (AD DS), DNS resolution, Group Policy Objects (GPOs), and centralized authentication.
3. PXE Network Boot Server: Delivers zero-touch network OS deployments to bare-metal or virtual client machines over TFTP/HTTP.
4. Managed Endpoints: Debian 12 workstations and Windows 11 Enterprise instances managed via Ansible inventory files.

# Planned Technologies, Tools & Languages

Infrastructure & Orchestration
| Component / Layer | Technology | Operational Role |
| **Control Node Platform** | Debian 12 (Bookworm) | Central management host running Ansible core execution engine |
| **Identity & Policy Host** | Windows Server 2022 | Hosts Active Directory Domain Services (AD DS), DNS, and GPOs |
| **Configuration Orchestrator** | Ansible Core | Infrastructure as Code (IaC) agentless engine using YAML playbooks |
| **Bare-Metal OS Deployment** | FOG Project / iPXE | Automated PXE network boot deployment over TFTP/HTTP |
| **Managed Linux Endpoints** | Debian 12 (Bookworm) | Managed host automated via OpenSSH and native Linux identity tools |
| **Managed Windows Endpoints** | Windows 11 Enterprise | Managed host automated via WinRM and PowerShell modules |

Identity, Automation & Protocols
* **Linux AD Integration:** `sssd`, `realmd`, `adcli`, `krb5-user` (PAM/NSS domain authentication)
* **Scripting Languages:** Bash, PowerShell, YAML
* **Network & Management Protocols:** SSH, WinRM, Kerberos, DNS, DHCP, TFTP
* **Version Control & Repository Management:** Git / GitHub

# Implementation Plan & Project Timeline

Phase 1: Core Lab & Identity Infrastructure (Weeks 1–3)
├── Deploy Debian 12 Control Node and Windows Server 2022 Domain Controller
├── Configure static networking, DNS zone records, AD forest, and baseline OUs
└── Provision SSH key pairs and WinRM certificates for agentless management

Phase 2: Configuration Automation & Playbook Development (Weeks 4–6)
├── Author Ansible playbooks for Linux AD domain join (sssd / realmd)
├── Develop PowerShell playbooks for Windows configuration via WinRM
└── Harden network security baselines (UFW, Windows Firewall, SSH key-only access)

Phase 3: Network Boot & Continuous Compliance Engine (Weeks 7–9)
├── Deploy FOG Project server and configure DHCP options 66/67 for iPXE network boot
├── Automate post-installation registration into Ansible control inventory
└── Establish automated drift detection and remediation cron jobs

Phase 4: Testing, Metrics & Documentation (Weeks 10–12)
├── Conduct end-to-end OS deployment and time-to-compliance benchmarking
├── Complete operational playbook for onboarding endpoints in < 5 minutes
└── Finalize Git repository documentation, architectural diagrams, and demo video

