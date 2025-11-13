# Useful Docker & n8n Commands

A reference list of frequently used commands for managing your local n8n environment.

---

## 🐳 Docker Commands

### Start all services
```bash
docker compose up -d
```

### Stop all services
```bash
docker compose down
```

### View running containers
```bash
docker ps
```

### View logs of a specific container
```bash
docker logs -f n8n
docker logs -f n8n_postgres
docker logs -f pgadmin
```

### Restart a single container
```bash
docker restart n8n
```

---

## 🗄 Managing Volumes

### List all volumes
```bash
docker volume ls
```

### Remove unused volumes
```bash
docker volume prune
```

---

## 📦 PostgreSQL Commands (via container)

### Access PostgreSQL shell
```bash
docker exec -it n8n_postgres psql -U n8n -d n8n_db
```

### List tables
```sql
\dt;
```

### Exit PostgreSQL
```sql
\q
```

---

## 🔄 Backup & Restore

### Backups are automatically stored in:
```
data/db_backups/
```

### Restore example (inside container):
```bash
psql -U n8n n8n_db < /backups/backup.sql
```

---

## 🧪 n8n Tools

### Export workflow
Inside n8n interface:  
→ Settings → Workflow → Export

### Import workflow
→ Settings → Workflow → Import

---

## ⚙ System Diagnostics

### Check open ports
```bash
netstat -ano
```

### Check local IP
```bash
ipconfig
```

---

Add more commands as needed while you expand your workflow development!
