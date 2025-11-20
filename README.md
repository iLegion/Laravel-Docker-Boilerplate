# 🐳 Laravel Docker Minimal Boilerplate

A minimalist and lightweight starter template for Laravel development using Docker.

This build is optimized for local development, utilizes **Alpine Linux** to minimize image sizes, and resolves file permission issues (bind mounts) on Linux and macOS.

## 🛠 Tech Stack

* **PHP 8.4** (FPM Alpine) — includes global `laravel/installer`.
* **PostgreSQL 18** (Alpine).
* **Nginx** (Alpine).

---

## 🚀 Installation & Setup

### 1. Configuration .env
Create a `.env` file in the project root by copying the example below.

```dotenv
# .env

# Docker Project Name
COMPOSE_PROJECT_NAME=laravel-docker

# Path to project root (Relative to docker-compose.yml)
PROJECT_ROOT="../"

# Permissions (Default is 1000, change if your local ID differs)
UID=1000
GID=1000

# Nginx Settings
NGINX_PORT_EXTERNAL=80

# Database Settings
DB_DATABASE=database-name
DB_USERNAME=root
DB_PASSWORD=root
DB_PORT_EXTERNAL=5432
```

### 2. Configuration nginx/local.conf
Update the `server_name` directive in `nginx/local.conf` to match your local domain.

### 3. Useful commands

#### Launching containers
```bash
docker compose -f docker-compose.yml up -d
```

#### Force container builds
```bash
docker compose -f docker-compose.yml up -d --build --remove-orphans --force-recreate
```
