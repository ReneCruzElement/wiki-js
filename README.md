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

## Local PostgreSQL (Docker)

This repo includes `docker-compose.yml` with a PostgreSQL service for Wiki.js.

1. Start PostgreSQL:
   ```bash
   docker compose up -d postgres
   ```
2. Start Wiki.js (from `wiki/`):
   ```bash
   node server
   ```

PostgreSQL data is bind-mounted to `wiki/data/postgres`, and init SQL files can be added to `wiki/data/postgres-init`.

Important:
- The database "image" is not stored in git; teammates pull `postgres:16-alpine` automatically from Docker Hub.
- This setup allows committing DB files, but PostgreSQL data folders are large and can cause noisy diffs. For team sharing, SQL dumps/migrations are usually better long-term.
