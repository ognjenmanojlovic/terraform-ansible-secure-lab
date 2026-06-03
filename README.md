# Terraform & Ansible Secure Gitea Lab

## Overview

This project demonstrates how to automate the deployment and hardening of a self-hosted Git service using **Terraform**, **Ansible**, **Docker**, and **Linux security best practices**.

The main goal of this project was to gain practical experience with:

- Infrastructure as Code (IaC)
- Configuration Management
- Linux Server Automation
- Dockerized Deployments
- SSH Hardening
- Firewall Management
- Secure Remote Administration

The environment was built inside a local lab using:

- macOS (Control Node)
- Ubuntu Server VM on VirtualBox (Managed Host)

---

# Project Goals

The objective of this project was to automate the provisioning and configuration of a secure Linux server environment instead of configuring everything manually.

The project includes:

- Automated Docker installation
- Automated Gitea deployment
- Automated firewall configuration
- Automated Fail2Ban installation
- SSH hardening
- Infrastructure validation using GitHub Actions

---

# Why Terraform?

Terraform is an Infrastructure as Code (IaC) tool used to define infrastructure in a reproducible way.

In this project, Terraform was used to:

- Learn Infrastructure as Code concepts
- Create a structured infrastructure workflow
- Validate Terraform configurations
- Simulate infrastructure provisioning inside a local lab

Although the infrastructure was deployed locally inside a VM environment, the same Terraform concepts can later be applied to cloud platforms.

---

# Why Ansible?

Ansible is a configuration management and automation tool.

Instead of manually typing commands on the server, Ansible automates the entire server setup process.

This project uses Ansible to automate:

- Linux package installation
- Docker installation
- Firewall configuration
- Fail2Ban installation
- Gitea deployment
- SSH hardening

This allows the server to be recreated quickly and consistently.

---

# Architecture

```text
MacBook (Control Node)
│
├── Terraform
├── Ansible
├── VS Code
├── SSH
└── GitHub

            │ SSH
            ▼

Ubuntu Server VM (Managed Host)
│
├── Docker
├── Gitea
├── UFW Firewall
├── Fail2Ban
└── Hardened SSH Configuration
```

---

# Technologies Used

## Infrastructure & Automation

- Terraform
- Ansible
- GitHub Actions

## Operating System

- Ubuntu Server

## Containerization

- Docker
- Docker Compose

## Self-Hosted Service

- Gitea

## Security

- UFW Firewall
- Fail2Ban
- SSH Hardening
- SSH Key Authentication

---

# Project Structure

```text
terraform-ansible-secure-infra/
│
├── terraform/
│   └── main.tf
│
├── ansible/
│   ├── inventory/
│   │   └── hosts.ini
│   │
│   ├── playbooks/
│   │   ├── site.yml
│   │   └── group_vars/
│   │       └── gitea.yml
│   │
│   └── roles/
│       ├── common/
│       ├── docker/
│       ├── security/
│       ├── ssh_hardening/
│       └── gitea/
│
├── .github/
│   └── workflows/
│       └── validate.yml
│
├── ansible.cfg
├── .gitignore
└── README.md
```

---

# Environment Setup

## VirtualBox Networking

The Ubuntu VM was configured using:

- NAT Networking
- Port Forwarding

Forwarded Ports:

| Service | Host Port | Guest Port |
|---|---|---|
| SSH | 2222 | 22 |
| Gitea Web UI | 3000 | 3000 |

Alternatively, the VM can also be configured using:

- Bridged Adapter

which would allow direct access to the VM using its own IP address.

---

# SSH Access

SSH access was configured between the macOS control node and the Ubuntu VM.

## SSH Connection Example

```bash
ssh user@192.168.x.x -p 2222
```

---

# Ansible Inventory

The inventory defines which server Ansible should manage.

Example:

```ini
[gitea]
ubuntu-vm ansible_host=192.168.x.x ansible_port=2222 ansible_user=user
```

---

# Ansible Roles

## Common Role

Installs common Linux packages such as:

- curl
- git
- wget
- unzip

---

## Docker Role

Installs and configures:

- Docker Engine
- Docker Compose

The Docker role also:

- Enables the Docker service
- Starts Docker automatically
- Adds the user to the Docker group

---

## Security Role

Configures:

- UFW Firewall
- Fail2Ban
- Firewall rules

Allowed ports:

| Port | Purpose |
|---|---|
| 22 | SSH |
| 3000 | Gitea Web Interface |

Default firewall policy:

```text
deny incoming
```

---

## SSH Hardening Role

The SSH hardening role improves remote access security.

Implemented hardening measures:

- Disabled root login
- Disabled password authentication
- Enabled SSH key authentication
- Disabled empty passwords

This project also demonstrates troubleshooting modern Ubuntu SSH configurations using:

```text
/etc/ssh/sshd_config.d/
```

---

## Gitea Role

The Gitea role:

- Creates the deployment directory
- Deploys the Docker Compose configuration
- Starts the Gitea container automatically

---

# Dockerized Gitea Deployment

Gitea runs inside a Docker container.

The deployment includes:

- Persistent Docker volume storage
- Custom environment variables
- Automatic container restart

---

# GitHub Actions

GitHub Actions were added to validate the infrastructure code automatically.

The workflow validates:

- Terraform formatting
- Terraform configuration
- Ansible syntax
- YAML formatting

This simulates a lightweight CI pipeline commonly used in DevSecOps workflows.

---

# Security Features

This project includes several security-focused components:

- SSH Hardening
- SSH Key Authentication
- UFW Firewall
- Fail2Ban
- Docker Isolation
- Infrastructure as Code
- Automated Configuration Management

---

# Screenshots

## Gitea Dashboard

![Gitea Dashboard](./docs/screenshots/gitea-dashboard.png)

---

## Successful Ansible Playbook Execution

![Ansible Playbook](./docs/screenshots/ansible-playbook.png)

---

## Docker Container

![Docker Container](./docs/screenshots/docker-container.png)

---

## UFW Firewall Status

![UFW Status](./docs/screenshots/ufw-status.png)

---

## SSH Hardening Validation

![SSH Hardening Validation](./docs/screenshots/ssh-hardening-validation.png)

---

# Learning Outcomes

This project provided hands-on experience with:

- Infrastructure as Code
- Linux Administration
- Docker Automation
- Secure Remote Access
- Configuration Management
- Infrastructure Validation
- DevSecOps Workflows
- Troubleshooting Linux Services
- Troubleshooting SSH Configurations

---

# Conclusion

This project demonstrates how modern infrastructure and server configuration can be automated using Infrastructure as Code and Configuration Management tools.

Instead of manually configuring servers, the entire environment can now be recreated consistently and securely using Ansible and Terraform.

The project also demonstrates practical Linux hardening and DevSecOps concepts in a realistic local lab environment.
