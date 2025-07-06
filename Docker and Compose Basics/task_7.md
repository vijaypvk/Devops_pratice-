
# 🚀 Task 7: Docker-Compose to Run Two Containers

## 🧩 Objective

Set up **Adminer** and **PostgreSQL** containers using `docker-compose`.  
Ensure **PostgreSQL** is **only accessible from Adminer** (i.e., not exposed to the host/public).

---

## 📖 Reference

- PostgreSQL Tutorial: [Sample Database – DVD Rental](https://www.postgresqltutorial.com/postgresql-getting-started/postgresql-sample-database/)

---

## 📝 Requirements

1. Create a `docker-compose.yml` that runs:
   - A PostgreSQL container (with a sample database)
   - An Adminer container (for web-based database interaction)

2. Ensure:
   - PostgreSQL **does not expose any public port**
   - Adminer can connect to PostgreSQL internally via Docker network

---

## 📦 Sample `docker-compose.yml`

```yaml
version: '3.8'

services:
  db:
    image: postgres:15
    container_name: pg-dvd
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: password
      POSTGRES_DB: dvdrental
    volumes:
      - ./dvdrental.tar:/docker-entrypoint-initdb.d/dvdrental.tar
    networks:
      - backend
    # No ports exposed → db is NOT accessible publicly

  adminer:
    image: adminer
    container_name: adminer-ui
    ports:
      - 8080:8080  # Adminer UI accessible on host
    depends_on:
      - db
    networks:
      - backend

networks:
  backend:
    driver: bridge
```

> 💡 Note: Place `dvdrental.tar` in the same directory as `docker-compose.yml`.

---

## ✅ Assessment

1. **Start containers**:
   ```bash
   docker-compose up -d
   ```

2. **Access Adminer**:
   - Open `http://localhost:8080`
   - Use the following credentials:
     - **System**: PostgreSQL
     - **Server**: `db` (Docker container name)
     - **Username**: `admin`
     - **Password**: `password`
     - **Database**: `dvdrental`

3. **Restore the DVD Rental Database**:
   - Ensure it's loaded from `dvdrental.tar` automatically at startup.
   - Or manually import via Adminer UI if needed.

---

## 🎯 Learning Outcomes

- ✅ Deploy multiple containers using `docker-compose`
- ✅ Enable **internal-only** communication between services using Docker networks
- ✅ Understand **service isolation** and **secure access control** in containerized environments
