# Option 2: Run PostgreSQL using Docker (Alternative)
**1. Pull and run PostgreSQL container**
Set `yourusername`, `yourpassword` and `yourdatabasename`:
```bash
# Run PostgreSQL container
docker run --name postgres-db \
  -e POSTGRES_PASSWORD=yourpassword \
  -e POSTGRES_USER=yourusername \
  -e POSTGRES_DB=yourdatabasename \
  -p 5432:5432 \
  -d postgres:latest
```

Check if container is running
```bash
docker ps
```

**2. Connect to PostgreSQL in Docker**
Connect using Docker exec
```bash
docker exec -it postgres-db psql -U yourusername -d yourdatabasename
```

Or install PostgreSQL client and connect
```bash
sudo apt install postgresql-client
```

```bash
psql -h localhost -p 5432 -U yourusername -d yourdatabasename
```
