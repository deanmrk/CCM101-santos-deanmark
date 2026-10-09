# 🏗️ Multi-Tier Architecture

## What is a Two-Tier Architecture?

A **Two-Tier Architecture** is a software design pattern that divides an application into two distinct layers or "tiers," each responsible for a specific function. In this model, the **first tier** handles the presentation and application logic (what the user interacts with), while the **second tier** manages data storage and retrieval (the database). These two tiers communicate with each other over a network — or in our case, through Docker's internal container network.

In our Nextcloud deployment, the **Nextcloud web application** acts as the first tier (the app/web layer), and **MariaDB** acts as the second tier (the database layer). Each runs in its own isolated container but is connected through Docker Compose.

---

## 🌐 The Web / Application Tier

**Role:** The Web/Application Tier is the front-facing layer of the system. It is responsible for:

- **Serving the User Interface (UI):** It delivers web pages, dashboards, and interactive elements that users see in their browser.
- **Handling HTTP Requests:** Every time a user uploads a file, logs in, or navigates the platform, the application tier processes that request.
- **Executing Business Logic:** It applies rules, processes data input from users, and decides what information to retrieve from the database.
- **Communicating with the Database:** After processing a request, it queries the database tier to store or retrieve the necessary data (e.g., user credentials, file metadata).

In our mission, **Nextcloud** fulfills this role. It serves the web interface on port `8080` and connects to MariaDB to manage user data and file records.

---

## 🗄️ The Database Tier

**Role:** The Database Tier is the back-end layer responsible for persistent data management. Its responsibilities include:

- **Storing Persistent Data:** All information — user accounts, passwords, file metadata, settings — is stored here and survives even if the application restarts.
- **Handling Database Queries:** It receives structured queries (SQL) from the application tier and returns the appropriate data.
- **Ensuring Data Integrity:** It enforces rules to keep data consistent, valid, and protected from corruption.
- **Access Control:** It uses credentials (username, password) to ensure only authorized services can read or write data.

In our mission, **MariaDB** fulfills this role. It stores the Nextcloud database (`nextcloud_db`) and is accessed using the credentials defined in the environment variables.

---

## ❓ Why Separate Them?

Separating the web application and the database into two distinct containers — rather than combining them into one — offers significant advantages in reliability, scalability, and security.

First, **separation of concerns** means that each container has one job and does it well; if the web server crashes or needs to be updated, the database remains unaffected and data is not lost. Second, **scalability becomes simpler**: if the web application receives heavy traffic, you can spin up multiple Nextcloud containers without duplicating the database, whereas a single-container design would require scaling everything together inefficiently. Finally, **security is greatly improved** because the database tier is not directly exposed to the internet — only the application tier can communicate with it through Docker's internal network, reducing the attack surface and protecting sensitive user data.

---

## 🖼️ Architecture Diagram

```
┌─────────────────────────────────────────────────────┐
│                    User's Browser                   │
│                  (Port 8080 / HTTP)                 │
└─────────────────────┬───────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────┐
│              TIER 1: Application Layer              │
│                                                     │
│   ┌─────────────────────────────────────────────┐   │
│   │         Nextcloud Container (app)           │   │
│   │   - Serves web interface                    │   │
│   │   - Handles HTTP requests                   │   │
│   │   - Processes user actions                  │   │
│   │   - Port Mapped: 8080 → 80                  │   │
│   └───────────────────┬─────────────────────────┘   │
└───────────────────────┼─────────────────────────────┘
                        │ Internal Docker Network
                        │ (MYSQL_HOST=database)
                        ▼
┌─────────────────────────────────────────────────────┐
│               TIER 2: Database Layer                │
│                                                     │
│   ┌─────────────────────────────────────────────┐   │
│   │         MariaDB Container (database)        │   │
│   │   - Stores user credentials                 │   │
│   │   - Stores file metadata                    │   │
│   │   - Manages nextcloud_db                    │   │
│   │   - Not exposed to the internet             │   │
│   └─────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────┘
```

---

*Part of the Cloud Computing Portfolio — CCM101 | Mission 6*
