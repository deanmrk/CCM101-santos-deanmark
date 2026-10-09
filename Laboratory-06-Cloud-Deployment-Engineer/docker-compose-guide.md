# Docker Compose Guide

## Overview

In this document i explains the `docker-compose.yml` file i used to deploy the Nextcloud private cloud storage system alongside its MariaDB database. It is written for engineers who need to understand the configuration before deploying or modifying the stack.

---

## The `docker-compose.yml` File

```yaml
version: '3'

services:
  database:
    image: mariadb:10.6
    environment:
      - MYSQL_ROOT_PASSWORD=cloudnova_root
      - MYSQL_PASSWORD=cloudnova_pass
      - MYSQL_DATABASE=nextcloud_db
      - MYSQL_USER=nextcloud_user

  app:
    image: nextcloud
    ports:
      - 8080:80
    environment:
      - MYSQL_PASSWORD=cloudnova_pass
      - MYSQL_DATABASE=nextcloud_db
      - MYSQL_USER=nextcloud_user
      - MYSQL_HOST=database
```

---

## Concept Explanations

### 1. What does the `services:` block do?

The `services:` block is the **core section** of a `docker-compose.yml` file. It defines all the individual containers (called "services") that make up your application. Each entry under `services:` represents one container with its own configuration — including what image to use, what environment variables to pass, what ports to expose, and more.

In our file, there are **two services** defined:

| Service Name | Container Image | Purpose |
|---|---|---|
| `database` | `mariadb:10.6` | Runs the MariaDB database engine |
| `app` | `nextcloud` | Runs the Nextcloud web application |

When you run `docker-compose up -d`, Docker reads the `services:` block and automatically **creates, configures, and starts all defined containers simultaneously**, connecting them on a shared internal network.

---

### 2. How did the Nextcloud app container know how to find the database container?

The Nextcloud app container found the database container using Docker Compose's **built-in internal networking** combined with the `MYSQL_HOST` environment variable.

When Docker Compose starts a stack, it automatically creates a **private virtual network** and connects all defined services to it. Each service is reachable by its **service name** as a hostname within that network.

In our configuration, the database service is named `database`. Because of this, the Nextcloud app container can reach it simply by using `database` as the host address — no IP address needed.

This is configured by the following line in the `app` service:

```yaml
environment:
  - MYSQL_HOST=database
```

This tells the Nextcloud application: *"Look for the database server at the hostname `database`."* Docker Compose resolves `database` to the correct container's internal IP address automatically. This is a key feature of Docker Compose — **automatic service discovery** through named services.

---

### 3. What is the difference between `docker run` and `docker-compose up -d`?

| Feature | `docker run` | `docker-compose up -d` |
|---|---|---|
| **Purpose** | Starts a **single** container manually | Starts **multiple** containers as a defined stack |
| **Configuration** | All settings are passed as long CLI flags | Settings are defined in a `docker-compose.yml` file |
| **Networking** | Requires manual network creation and linking | Automatically creates a shared network for all services |
| **Reusability** | Commands must be retyped every time | The YAML file is reusable and version-controllable |
| **Scalability** | Difficult to manage multiple containers | Easily manages complex multi-container deployments |
| **IaC Principle** | Imperative (command-by-command) | Declarative (define desired state in a file) |
| **Example** | `docker run -d -p 8080:80 nextcloud` | `docker-compose up -d` (reads from YAML) |

**In summary:** `docker run` is like building furniture piece by piece with manual instructions, while `docker-compose up -d` is like following a complete blueprint that assembles everything at once. Docker Compose promotes **Infrastructure as Code (IaC)** — the practice of managing infrastructure through machine-readable configuration files rather than manual commands.

---

## Key Configuration Breakdown

### Environment Variables

Environment variables are used to pass configuration settings into containers at runtime. In our file, they serve as the **shared credentials** between the two services:

| Variable | Set In | Purpose |
|---|---|---|
| `MYSQL_ROOT_PASSWORD` | `database` | Sets the MariaDB root administrator password |
| `MYSQL_DATABASE` | Both | The name of the database to create / connect to |
| `MYSQL_USER` | Both | The username for database access |
| `MYSQL_PASSWORD` | Both | The password for the above user |
| `MYSQL_HOST` | `app` | Tells Nextcloud where to find the database (service name) |

### Port Mapping

```yaml
ports:
  - 8080:80
```

This maps **port 80 inside the container** (where Nextcloud's web server listens) to **port 8080 on the host machine**. This allows users to access the Nextcloud interface by visiting `http://localhost:8080` or through KillerCoda's traffic routing.

---

