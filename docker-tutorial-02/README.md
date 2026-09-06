# 🐳 Docker Database Setup

A simple guide to running popular databases using **Docker** and **Docker Compose**.

## 📋 Databases

| Database   | Version |           Port |
| ---------- | ------: | -------------: |
| PostgreSQL |    15.1 |         `5432` |
| MongoDB    |     6.0 |        `27017` |
| Redis      |       7 |         `6379` |
| MySQL      |     8.0 |         `3306` |
| Neo4j      |     4.4 | `7474`, `7687` |
| Cassandra  |     4.1 |         `9042` |

---

## 📁 Files

### `db-scripts.txt`

Contains individual `docker run` commands for each database.

Use this if you want to **run databases individually**.

### `docker-compose.yml`

Contains all databases as Docker Compose services.

Use this if you want to **manage multiple databases from one file**.

---

# 1. Docker Run

The `db-scripts.txt` file contains commands for running each database separately.

Example:

```bash
docker run -d --rm \
  -v pgdata:/var/lib/postgresql/data \
  -e POSTGRES_USER=myuser \
  -e POSTGRES_PASSWORD=mypass \
  -e POSTGRES_DB=mydb \
  -p 5432:5432 \
  postgres:15.1-alpine
```

Run the required database command from `db-scripts.txt`.

---

# 2. Docker Compose

To start all databases defined in `docker-compose.yml`:

```bash
docker compose up -d
```

Check running services:

```bash
docker compose ps
```

Stop the services:

```bash
docker compose stop
```

Stop and remove containers:

```bash
docker compose down
```

> Database data is stored in Docker volumes, so `docker compose down` does not delete the data.

To remove containers **and database data**:

```bash
docker compose down -v
```

⚠️ Use `-v` carefully because it deletes the database volumes.

---

## 🔐 Default Credentials

| Database   | Username | Password   | Database |
| ---------- | -------- | ---------- | -------- |
| PostgreSQL | `myuser` | `mypass`   | `mydb`   |
| MongoDB    | `myuser` | `mypass`   | `mydb`   |
| MySQL      | `myuser` | `mypass`   | `mydb`   |
| Neo4j      | `neo4j`  | `password` | —        |
| Redis      | —        | —          | —        |
| Cassandra  | —        | —          | —        |

> ⚠️ These credentials are for **local development/learning only**. Do not use them in production.

---

## 🆚 Which One Should I Use?

**Use `db-scripts.txt`** → When learning Docker or running a single database.

**Use `docker-compose.yml`** → When running and managing multiple databases together.

---

## 🛠️ Prerequisites

Install Docker and make sure it is running.

Check your installation:

```bash
docker --version
docker compose version
```
