# Setup Postgres on Ubuntu

## Option 1: Install PostgreSQL directly on Ubuntu (Recommended for development)
**Step 1: Install Postgres**

- Update package list
```bash
sudo apt update
```

- Install PostgreSQL and additional contributed packages
```bash
sudo apt install postgresql postgresql-contrib
```

- Check PostgreSQL version
```bash
psql --version
```

**Step 2: Start PostgreSQL service**
- Start PostgreSQL service
```bash
sudo service postgresql start
```
- Enable auto-start on boot
```bash
sudo systemctl enable postgresql
```

**Step: 3. Set up PostgreSQL user and database**

- Switch to postgres user
```bash
sudo -i -u postgres
```

 - Access PostgreSQL prompt
```bash
psql
```

- Create a new user (replace 'yourusername' with your actual username)
```bash
CREATE USER yourusername WITH PASSWORD 'yourpassword';
```

- Create a database for your user
```bash
CREATE DATABASE yourdatabase OWNER yourusername;
```
- Grant all privileges
```bash
GRANT ALL PRIVILEGES ON DATABASE yourdatabase TO yourusername;
```

- Exit PostgreSQL prompt
```bash
\q
```

- Exit postgres user
```bash
exit
```

**Step 4. Configure PostgreSQL for easier access**
Create a PostgreSQL user that matches your Ubuntu username
```bash
sudo -u postgres createuser --interactive
```
- Follow the prompts:
- Enter name of role to add: [your ubuntu username]
- Shall the new role be a superuser? (y/n) y

Create a database with your username
```bash
sudo -u postgres createdb $USER
```

**Step 5: Connect to PostgreSQL**
Connect to your database
```bash
psql
```

Or connect to a specific database
```bash
psql -d yourdatabase
```

Or connect with specific user
```bash
psql -U yourusername -d yourdatabase
```

## Common PostgreSQL Commands
### Basic operations
```sql
-- List all databases
\l

-- Connect to a database
\c database_name

-- List all tables
\dt

-- List all users
\du
```
Create a table
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    email VARCHAR(100) UNIQUE
);
```
Insert data
```sql
INSERT INTO users (name, email) VALUES ('John Doe', 'john@example.com');
```
Select data
```sql
SELECT * FROM users;
```

Exit PostgreSQL
```sql
\q
```

### Useful management commands
```sql
# Check PostgreSQL status
sudo service postgresql status

# Stop PostgreSQL
sudo service postgresql stop

# Restart PostgreSQL
sudo service postgresql restart

# View PostgreSQL logs
sudo journalctl -u postgresql

# Access PostgreSQL configuration
sudo nano /etc/postgresql/16/main/postgresql.conf
``
