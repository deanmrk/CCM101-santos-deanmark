# 🚀 Mission 6: The Cloud Deployment Engineer

## Mission Overview

CloudNova Technologies has been tasked by a university client to deploy a private, secure cloud storage system as a replacement for Google Drive. The solution chosen is **Nextcloud**, an enterprise-grade private cloud platform that requires a backend database to manage user credentials and file metadata.

In this mission, I transitioned from manually running individual Docker containers to using **Infrastructure as Code (IaC)** via **Docker Compose**. I deployed a two-tier architecture — a **MariaDB** database container and a **Nextcloud** web container — linked together and launched simultaneously with a single command.

---

## 🎯 Objectives

- Explain the concept of a multi-tier application architecture
- Understand the purpose and structure of a `docker-compose.yml` file
- Use a Linux command-line text editor (`nano`) to create configuration files
- Deploy a multi-container application (Nextcloud + MariaDB) using Docker Compose
- Document deployment procedures and Infrastructure as Code (IaC) principles using Markdown
- Expand my professional GitHub Cloud Computing Portfolio

---

## 💻 Commands Executed

```bash
# Create project directory and navigate into it
mkdir nextcloud-deployment
cd nextcloud-deployment

# Create the Docker Compose configuration file using nano
nano docker-compose.yml

# Deploy the multi-container stack in detached (background) mode
docker-compose up -d

# Verify both containers are running
docker-compose ps

# Gracefully shut down and remove all containers
docker-compose down
```

---

## 🧠 Skills Learned

| Skill | Description |
|---|---|
| **Multi-Tier Architecture** | Understood how to separate application logic and data storage into distinct service layers |
| **Docker Compose** | Learned how to define and manage multi-container Docker applications using a single YAML file |
| **Infrastructure as Code (IaC)** | Practiced writing deployment configuration as code instead of manual commands |
| **YAML Syntax** | Gained experience writing strictly space-sensitive YAML configuration files |
| **Nano Text Editor** | Used the Linux CLI text editor to create and edit configuration files in the terminal |
| **Container Networking** | Understood how Docker Compose links containers via internal service names (e.g., `MYSQL_HOST=database`) |
| **Port Mapping** | Mapped internal container ports to host ports for browser access |

---

## 📁 Repository Structure

```
Laboratory-06-Cloud-Deployment-Engineer/
├── README.md
├── multi-tier-architecture.md
├── docker-compose-guide.md
├── reflection.md
└── screenshots/
    ├── compose-deployment.png
    ├── nextcloud-web.png
    └── compose-teardown.png
```

---

## 📸 Evidence / Screenshots

| Screenshot | Description |
|---|---|
| `compose-deployment.png` | Terminal showing successful `docker-compose up -d` and running containers |
| `nextcloud-web.png` | Browser displaying the Nextcloud installation/setup page |
| `compose-teardown.png` | Terminal showing containers being stopped and removed via `docker-compose down` |

---

*Part of the Cloud Computing Portfolio — CCM101*
