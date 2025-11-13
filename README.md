# Configuring n8n Locally (Docker + PostgreSQL)

A clean, production-ready environment to run **n8n locally** using Docker, with PostgreSQL as the database engine and automatic backups.

<p align="center">
  <img src="https://n8n.io/images/home/header/home-header-bg.png" width="70%" />
</p>

---

## ⭐ Overview

This repository provides a fully functional setup to run **n8n self-hosted** on your local machine using:

- **Docker & Docker Compose**
- **PostgreSQL 15** for robust database performance
- **Automatic daily database backups**
- **Persistent Docker volumes**
- **Clean, reproducible configuration**

This setup is ideal for:

✔ Learning and experimenting with n8n  
✔ Local automation workflows  
✔ ETL pipelines and API integrations  
✔ Webhook testing  
✔ Preparing for future production deployment

---

## 📦 Stack Components

| Service | Description |
|--------|-------------|
| **n8n** | Main automation tool |
| **PostgreSQL 15** | Primary database |
| **pgAdmin (optional)** | Database GUI |
| **Backup container** | Creates daily `.sql` dumps |

---

## 🚀 Getting Started

### **1. Clone the repository**
```bash
git clone https://github.com/yourusername/Configuring-n8n-Locally.git
cd Configuring-n8n-Locally
```

### **2. Copy the environment template**
```bash
cp .env.example .env
```

(Optional) Edit values inside `.env`.

---

### **3. Start the full stack**
```bash
docker compose up -d
```

---

### **4. Access n8n**

#### Local machine  
👉 `http://localhost:5678`

#### Local network  
👉 `http://<your-local-ip>:5678`

You will pass through two authentication layers:

1. **Basic Auth** (configured in `docker-compose.yml`)
2. n8n’s **Owner Account Setup**  
   → This is the first-time local account; any email/password will work.

---

## 🗂 Project Structure

```
Configuring-n8n-Locally/
│
├── docker-compose.yml
├── .env.example
├── README.md
│
├── docs/
│   ├── troubleshooting.md
│   └── useful-commands.md
│
├── data/
│   ├── postgres/
│   ├── n8n/
│   └── db_backups/
│
└── .gitignore
```

The folders inside **data/** are auto-created by Docker and must not be committed to Git.

---

## ⚙ docker-compose.yml

This compose file includes:

- n8n service  
- PostgreSQL database  
- Automatic daily backups  
- Persisted data volumes  
- Ready for local development  

You can later extend this to include:

- HTTPS with **Nginx Proxy Manager (highly recommended for secure production use)**
- Cloudflare tunnels  
- Multi-instance setups  
- Remote server deployment  

---

## 🔧 Useful Docker Commands

### Stop the whole stack:
```bash
docker compose down
```

### Restart with updated configuration:
```bash
docker compose down
docker compose up -d
```

### View logs:
```bash
docker logs -f n8n
docker logs -f n8n_postgres
```

---

## 🔐 Authentication

### Basic Auth  
Configured directly in the compose file:

```
username: admin
password: admin123
```

### Owner Account  
After passing Basic Auth, n8n will ask you to create an owner account that is stored locally in PostgreSQL.

---

## 🔄 Database Backups

Daily automatic backups are stored in:

```
data/db_backups
```

You can adjust the retention period in the `docker-compose.yml` (`BACKUP_KEEP_DAYS`).

---

## 🧪 Why This Setup?

- No installation required (everything runs inside containers)
- Zero system pollution — clean and safe
- Suitable for testing workflows and integrations
- Reproducible environment for learning
- Smooth path to production environments
- No dependency on SQLite (Postgres is faster & safer)

---

## 📝 Future Improvements

Here are recommended enhancements for a production-grade setup:

### **✔ Add Nginx Proxy Manager for HTTPS and Domain Routing**

Implementing **Nginx Proxy Manager (NPM)** allows you to:

- Secure your instance with **HTTPS / SSL certificates** (Let’s Encrypt)
- Serve n8n behind a **custom domain**
- Add a protective reverse-proxy layer before n8n
- Improve webhook reliability with valid SSL
- Use multiple services behind one server (n8n, dashboards, API apps, etc.)

This is *the most important upgrade* when taking your environment from local testing to real production use.

### Additional improvements:
- Deploy to a VPS (DigitalOcean, Hetzner, AWS)
- Use Cloudflare DNS + Firewall hardening
- Add CI/CD for workflow export automation
- Implement secrets manager (Vault, Doppler, 1Password)
- Enable monitoring (Grafana + Prometheus)

---

## 📜 License
MIT License — feel free to use, modify, and distribute.

---

## ⭐ Support
If this project helps you, please consider leaving a **⭐ star** on GitHub!

---

## License
MIT License — feel free to use, modify, and distribute.
