# 📚 Element Home

Welcome to the central knowledge hub for **Element**.  
This wiki contains the shared context, standards, and project documentation needed to build, operate, and improve our systems.

> **Purpose:** Make knowledge easy to find, easy to trust, and easy to maintain.

---

## 🧭 How to Use This Wiki

- Start with the **Project Overview** if you're joining a new project
- Use **Area Documentation** to understand domain responsibilities
- Refer to **Role Starters** when onboarding or changing roles
- Keep documentation **accurate, owned, and up to date**

📌 *If something is unclear or missing, that is a documentation bug.*

---

## 🗂️ Documentation Structure

### 🏢 Company
High-level, stable information about how we work.

- 📖 How We Work
- 🧱 Architecture Overview
- 📐 Engineering Standards
- 📘 Glossary & Definitions

➡️ `company`

---

### 🧩 Areas
Domain-specific documentation owned by each area or team.

- 🎯 Mission & Scope
- 🛠️ Systems & Services Owned
- 🔁 Processes & Workflows
- 📊 Data Domains & Definitions
- 👥 Role Starters (area-specific)

➡️ `/areas`

---

### 🚀 Projects
Documentation for active and completed projects.

Each project includes:
- One-page project overview
- Architecture & data documentation
- Delivery and operational details

➡️ `/projects`

---

### 👤 Roles
One-page starters for each role across the organization.

- Responsibilities & expectations
- First-week checklist
- Tools, access, and key contacts

➡️ `/roles`

---

## 🧪 Templates & Standards

Use templates to keep documentation consistent and useful.

- 📄 Project Starter Template
- 👤 Role Starter Template
- 🗃️ Data Dictionary Template
- 🏗️ Architecture Decision Record (ADR)

➡️ `/templates`

---

## ✍️ Documentation Principles

1. **Every page has an owner**
2. **Document what exists, not what’s ideal**
3. **Start small, then go deeper**
4. **Keep docs close to the work**
5. **If it’s not documented, it doesn’t scale**

➡️ Read more: `/company/documentation-principles`

---

## 🔎 Looking for Something?

- Use search for quick answers
- Check the **Glossary** for shared terminology
- Visit the relevant **Area** or **Project** page

If you still can’t find it:
> 👉 Create or update the documentation.

---

## 🛠️ Contributing

Documentation is part of our delivery process.

- Anyone can propose changes
- Owners are responsible for reviews
- Outdated documentation should be flagged or fixed

➡️ How to contribute: `/company/contributing-to-docs`

---

## 🗓️ Last Updated
**{{DATE}}**

📩 Questions or suggestions? Contact **{{Documentation Owner / Team}}**

---

## Local Containers (Docker Compose)

This project runs as a multi-container stack with:
- `nginx` (reverse proxy)
- `wiki` (Wiki.js app)
- `postgres` (database)
- `redis` + `redis-exporter` (cache + metrics exporter)
- `prometheus` (metrics collection)
- `grafana` (dashboards)

### Start the stack

```bash
docker compose up -d
```

### Access services

- Wiki.js (through Nginx): `http://localhost`
- Prometheus: `http://localhost:9090`
- Grafana: `http://localhost:3001`
- PostgreSQL from host: `localhost:5433`  
  DB: `wiki` | User: `wikijs` | Password: `wikijsrocks`

### Common container commands

Check status:
```bash
docker compose ps
```

Follow logs:
```bash
docker compose logs -f
```

Follow logs for a single service:
```bash
docker compose logs -f wiki
docker compose logs -f nginx
docker compose logs -f postgres
docker compose logs -f prometheus
docker compose logs -f grafana
```

Restart or stop:
```bash
docker compose restart
docker compose stop
docker compose start
docker compose down
```

Open a shell in a running container:
```bash
docker compose exec wiki sh
docker compose exec postgres sh
docker compose exec redis sh
```

### Monitoring notes

- Prometheus is preconfigured with `monitoring/prometheus.yml`.
- Default scrape targets include: Prometheus, Redis exporter, and Grafana.
- In Grafana, add Prometheus as a data source with URL: `http://prometheus:9090`.

### Persistence and config

- Nginx config: `nginx/default.conf`
- Prometheus config: `monitoring/prometheus.yml`
- PostgreSQL init scripts: `wiki/data/postgres-init`
- PostgreSQL data: Docker named volume (`postgres_data`)
- Redis data: `wiki/data/redis`
- Prometheus and Grafana data: Docker named volumes (`prometheus_data`, `grafana_data`)

Important:
- Docker images are pulled automatically by Compose on first run.
- `redis` is internal-only (not published to the host).
- Wiki.js is intentionally exposed through Nginx (`http://localhost`) instead of directly on host port `3000`.

### Windows / WSL note for PostgreSQL

If you see errors like `chmod ... Operation not permitted` for PostgreSQL, it means bind-mount permissions are incompatible on that host filesystem.

This stack uses a named Docker volume for PostgreSQL to avoid that issue. If a previous failed container exists, run:

```bash
docker compose down
docker compose up -d
```

If it still fails because of old state, run:

```bash
docker compose down -v
docker compose up -d
```

Warning: `down -v` deletes local Docker volumes for this stack (database/monitoring data).
