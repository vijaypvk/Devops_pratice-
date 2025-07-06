
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
    image: postgres:latest
    container_name: test_postgres
    environment:
      POSTGRES_USER: admin
      POSTGRES_PASSWORD: test
      POSTGRES_DB: test
    ports:
      - "5432"
    volumes:
      - db_data:/var/lib/postgresql/data
    networks:
      - internal
  
  adminer:
    image: adminer:latest
    container_name: adminer_ui
    ports:
      - "8080:8080"
    depends_on:
      - db
    networks:
      - internal

volumes:
  db_data:
  
networks:
  internal:
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
