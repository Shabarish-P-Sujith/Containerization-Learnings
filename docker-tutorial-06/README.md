# Docker Compose

- Docker Compose is a tool that lets you define and run multi-container Docker applications using a single configuration file.

- When to use Docker Compose :
✅ Local development
✅ Small to medium deployments
✅ Microservices testing
❌ Large-scale orchestration (use Kubernetes instead)

## Typical Dev Workflow (Commands which are Mostly used !!!)
```bash
docker compose up -d
docker compose watch
docker compose logs -f
docker compose down
```

## NOTE
Here, as a beginner, we will be "mostly" working with --->>> docker-compose.yml

## COMMANDS

1. Custom File Names
```bash
# Single custom file
docker compose -f my-compose.yml up -d

# Multiple files (merged)
docker compose -f docker-compose.yml -f docker-compose.prod.yml up -d

# Different file in different directory
docker compose -f /path/to/compose.yml up -d
```

2. Start your services defined in docker-compose.yml.
- Builds images if needed
- Creates networks/volumes
- Attaches to logs by default

- Common options:
```bash
docker compose up          # start and attach
docker compose up -d       # start in detached mode (background)
docker compose up --build  # force rebuild images
```

3. Stops and removes everything created by up.
- Stops containers
- Removes containers, networks
- Keeps volumes by default

- Common options:
```bash
docker compose down            # stop and remove containers
docker compose down -v         # also remove volumes (⚠ data loss)
docker compose down --rmi all  # remove images too
```

4. Live-reloads services when files change (newer feature).
- Watches source files
- Rebuilds/restarts containers automatically
- Useful for development

- Usage:
```bash
docker compose watch
```

5. View container logs.
- Common options:
```bash
docker compose logs            # show all logs
docker compose logs -f         # follow (tail -f)
docker compose logs service    # logs for one service
docker compose logs --tail=50  # last 50 lines
```

6. Execute command in running service
```bash
# Open a shell in a running service
docker compose exec <service> sh
docker compose exec <service> bash

# Run a command in a running service
docker compose exec <service> <command> [args...]

# Run a command as a specific user
docker compose exec -u <user> <service> <command>

# Database backup (stdout redirected on host)
docker compose exec <db_service> pg_dump -U <db_user> <db_name> > <backup_file>.sql

# Database restore (stdin redirected into container)
docker compose exec -T <db_service> psql -U <db_user> <db_name> < <backup_file>.sql
```

7. Control service lifecycle
```bash
# Start stopped services
docker compose start

# Stop running services (doesn't remove)
docker compose stop

# Restart services
docker compose restart

# Restart specific service
docker compose restart <service>
```