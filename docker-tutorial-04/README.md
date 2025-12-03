# Docker Volumes

- Persist data (databases, logs, uploads)
- Share data between containers
- Edit files without rebuilding image

# Simple Rule: Need to save Data ? Use VOLUMES !! 

## Volume Commands

1. Create Volume
```bash
docker volume create <my-volume>
```

2. List Volumes
```bash
docker volume ls
```

3. Inspect Volume (Check Volume Location)
```bash
docker volume inspect <my-volume>
```

4. Remove Volume
```bash
docker volume rm <my-volume>
```

5. Remove Unused Volumes
```bash
docker volume prune
```

# Using Volumes

### Method 1: Named Volume
```bash
# Create and use
docker run -v <my-volume>:/app/data nginx
# Data in /app/data persists even after container is deleted
```
### Method 2: Bind Mount (Host folder)
```bash
# Mount host folder to container
docker run -v /host/path:/container/path nginx

# Example
docker run -v $(pwd)/website:/usr/share/nginx/html nginx
```

- Left side [$(pwd)/website] = folder on YOUR computer
- Right side [/usr/share/nginx/html] = folder INSIDE container
- They're connected! Changes on left show up on right

### Method 3: Anonymous Volume
```bash
docker run -v /app/data nginx
# Docker creates unnamed volume automatically
```

| Type             | Syntax                       | Use Case                      |
|------------------|------------------------------|-------------------------------|
| Named Volume     | -v volume-name:/path         | Databases, production         |
| Bind Mount       | -v /host/path:/path          | Development, config files     |
| Anonymous Volume | -v /path                     | Temporary data                |


# Common Use Cases
```bash
# MySQL database
docker run -d --name msq01 -v mysql-data:/var/lib/mysql mysql

# PostgreSQL
docker run -d --name pg1 -v pg-data:/var/lib/postgresql/data postgres

# Logs
docker run -v logs:/app/logs myapp

# Config files
docker run -v /host/config.json:/app/config.json myapp
```

# Simple Usage

## VOLUMES 
```bash
# Create and use a Volume

docker volume create <my-volume>
docker run -v <my-volume>:/app/data <image>
# docker run -v $(pwd):/app <image>
```

## BIND MOUNTS 
```bash
# Mount host directory to container

docker run -v /host/path:/container/path <image>
docker run --mount type=bind,src=/host/path,target=/container/app <image>
# docker run --mount type=bind,src=$(pwd),target=/app <image>
```