# Troubleshooting Guide for Local n8n Setup

This document helps diagnose common issues when running n8n locally with Docker + PostgreSQL.

---

## 🟥 n8n is not accessible at http://localhost:5678
**Possible causes:**

1. Container is not running  
   → Run:
   ```bash
   docker ps
   ```

2. Port already in use  
   → Check:
   ```bash
   netstat -ano | findstr :5678
   ```

3. Compose not configured correctly  
   → Run:
   ```bash
   docker compose down
   docker compose up -d
   ```

---

## 🟥 Database connection errors
**Symptoms:**
- n8n container restarts endlessly  
- Logs show `"ECONNREFUSED"` or `"database does not exist"`

**Fix:**
- Check Postgres logs:
  ```bash
  docker logs -f n8n_postgres
  ```

- Ensure env variables match:
  ```
  POSTGRES_USER
  POSTGRES_PASSWORD
  POSTGRES_DB
  ```

---

## 🟥 Basic Auth login failing
**Fix:**
Check values in `.env`:

```
N8N_BASIC_AUTH_ACTIVE=true
N8N_BASIC_AUTH_USER=admin
N8N_BASIC_AUTH_PASSWORD=admin123
```

Restart container:
```bash
docker compose up -d
```

---

## 🟥 Cannot create n8n owner account
**Common cause: invalid host configuration**

Ensure `.env` has:

```
N8N_HOST=localhost
WEBHOOK_URL=http://localhost:5678/
```

If these values point to non-existent domains, the onboarding breaks.

---

## 🟥 pgAdmin does not open
Check if container is running:
```bash
docker ps
```

Access:
```
http://localhost:8080
```

If port is in use, update compose file.

---

## 🟩 Need more help?
Most issues are related to:

- Wrong environment variables  
- Missing volumes  
- Incorrect host/webhook URL  
- Port conflicts  

Feel free to extend this file with new problems & solutions.
