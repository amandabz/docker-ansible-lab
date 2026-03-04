# 🐳 Docker + Ansible Ubuntu Automation Project

<div align="center">

<strong>Automate the setup of multiple Ubuntu 22.04 containers using Docker and Ansible</strong>

<br>
<a href="#-prerequisites">Prerequisites</a> •
<a href="#-quick-start">Quick Start</a> •
<a href="#-project-structure">Project Structure</a> •
<a href="#-usage">Usage</a> •
<a href="#-contributing">Contributing</a>
<br>

</div>

## 📋 Table of Contents
- [About](#-about)
- [Features](#-features)
- [Prerequisites](#-prerequisites)
- [Project Structure](#-project-structure)
- [Quick Start](#-quick-start)
- [Usage](#-usage)
- [Configuration](#-configuration)
- [Troubleshooting](#-troubleshooting)
- [Logs](#-logs)
<hr style="border:0.05px solid gray">

## 🎯 About

This project demonstrates how to **automate the setup of multiple Ubuntu 22.04 containers** using **Docker** and **Ansible**. The containers come pre-configured with **Python 3**, enabling Ansible to manage them seamlessly and install additional software like curl and PostgreSQL.
<hr style="border:0.05px solid gray">

### ✨ Features

- 🐧 **Ubuntu 22.04 LTS** base image
- 🐍 **Python 3 pre-installed** for Ansible compatibility
- 📦 **Docker Compose** for multi-container orchestration
- 🤖 **Ansible automation** for configuration management
- 🐘 **PostgreSQL** and **curl** automated installation
- 🔄 **Scalable architecture** - easily add more containers
<hr style="border:0.05px solid gray">

## 🔧 Prerequisites
Before you begin, ensure you have the following installed:

| Tool | Version | Installation Guide |
|------|---------|-------------------|
| **Docker** | 20.10+ | [Get Docker](https://www.docker.com/get-started) |
| **Docker Compose** | 2.0+ | [Install Docker Compose](https://docs.docker.com/compose/install/) |
| **Ansible** | 2.9+ | [Install Ansible](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html) |
<hr style="border:0.05px solid gray">

### 💡 Quick Check

```bash
# Verify Docker version
docker --version

# Verify Docker Compose version
docker-compose --version

# Verify Ansible version
ansible --version
```
<hr style="border:0.05px solid gray">

### 📁 Project Structure

```
docker-ansible-lab/
│
├── inventory.ini           # Ansible inventory for the containers
├── playbook.yml            # Ansible playbook to install curl & PostgreSQL
├── README.md               # Project documentation
├── .gitignore              # Files and folders to ignore in Git
│
└── docker/                 # Docker folder
    ├── Dockerfile                  # Base image with Ubuntu 22.04 and Python 3
    └── docker-compose.yml          # Defines and runs multiple containers
```
<hr style="border:0.05px solid gray">

### 🚀 Quick Start

Get up and running in less than 2 minutes!

```bash
# Clone the repository
git clone https://github.com/amandabz/docker-ansible-lab.git
cd docker-ansible-lab

# Build and start containers
cd docker
docker-compose up -d --build

# Run Ansible playbook
cd ..
ansible-playbook -i inventory.ini playbook.yml

# Verify installation
docker exec -it ansible_lab_1 curl --version
docker exec -it ansible_lab_1 psql --version

docker exec -it ansible_lab_2 curl --version
docker exec -it ansible_lab_2 psql --version
```
<hr style="border:0.05px solid gray">

### 📖 Usage
#### 1️⃣ Build the Docker image and start the containers

```bash
cd docker
docker-compose up -d --build
```

#### 2️⃣ Verify containers are running

```bash
docker ps -a
```

Expected output:

```
CONTAINER ID   IMAGE            COMMAND            STATUS         NAMES
xxxxxxxxxxxx   docker-ubuntu1   "sleep infinity"   Up X minutes   ansible_lab_1
yyyyyyyyyyyy   docker-ubuntu2   "sleep infinity"   Up X minutes   ansible_lab_2
```

#### 3️⃣ Check Python version inside containers

```bash
docker exec -it ansible_lab_1 python3 --version
docker exec -it ansible_lab_2 python3 --version
```

#### 4️⃣ Run Ansible playbook

```bash
ansible-playbook -i inventory.ini playbook.yml
```

This will:
<br>
• ✅ Install **curl** in both containers
<br>
• ✅ Install **PostgreSQL** and its dependencies


#### 5️⃣ Access containers interactively

```bash
# Access first container
docker exec -it ansible_lab_1 /bin/bash

# Access second container
docker exec -it ansible_lab_2 /bin/bash
```

#### 6️⃣ Delete containers

```bash
docker-compose down
```

Add *-v flag* to also remove volumes:
```bash
docker-compose down -v
```

#### Or maybe you prefer to stop the containers...
```bash
docker-compose stop
```
<hr style="border:0.05px solid gray">

### ⚙️ Configuration
#### 🐳 Dockerfile Configuration

The **Dockerfile** creates an Ubuntu 22.04 image with Python 3:

```Dockerfile
FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update && \
    apt install -y sudo && \
    apt install -y python3 openssh-server sudo && \
    apt clean

CMD ["sleep", "infinity"]
```

#### 🎼 Docker Compose Configuration

The **docker-compose.yml** defines the multi-container setup:

```yaml
services:
  ubuntu1:
    build: .
    container_name: ansible_lab_1

  ubuntu2:
    build: .
    container_name: ansible_lab_2
```

#### 🤖 Ansible Inventory

The **inventory.ini** file defines container hosts:

```ini
[docker_containers]
ansible_lab_1 ansible_connection=docker
ansible_lab_2 ansible_connection=docker
```
<hr style="border:0.05px solid gray">

### 🐛 Troubleshooting

Common Issues and Solutions

| Issue | Solution |
|-------|----------|
| Container not starting | Check Docker daemon: ```bash sudo systemctl status docker``` |
| Ansible connection failed | Ensure containers are running: ```bash docker ps -a``` |
| Python not found | Rebuild image: ```bash docker-compose build --no-cache``` |
| Permission denied | Run with sudo or add user to docker group |
<hr style="border:0.05px solid gray">

#### 📝 Logs

```bash
# View container logs
docker logs ansible_lab_1

# View Ansible verbose output
ansible-playbook -i inventory.ini playbook.yml -vvv
```
<hr style="border:0.05px solid gray">
<br>

<div align="center">

⭐ If you found this project helpful, please consider giving it a star!
<br>
<br>
Made with ❤️ by Amanda Benítez Hidalgo

</div>
