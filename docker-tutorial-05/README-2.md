# Commands

1. List all the Networks:
```bash
docker network ls
```

- Usages/Examples :
```bash 
docker network ls --filter name=my_network   # Shows networks with specific names
docker network ls --filter driver=bridge     # Show only bridge networks
docker network ls --filter scope=local       # Show only scopes - local

docker network ls --format "{{.Name}}"       # Show only names
docker network ls --format "{{.Driver}} - {{.Scope}}"    # Show drivers and scopes
docker network ls --format "table {{.Driver}} - {{.Scope}}"    # Show drivers and scopes as a TABLE 
```

---

2. Display detailed information about a network
```bash
docker network inspect <network_name>
docker network inspect <network_id>
```

- It shows complete details: subnet, gateway, connected containers, IPs, etc.

- Output includes:
  - All connected/disconnected containers with their IPs
  - Network ID and name
  - Driver type
  - Subnet and gateway
  - Network configuration 

---

3. Create a new network (default: bridge type)
```bash
docker network create <network_name>
```
- It is used when you need containers to communicate by name, or want network isolation

- Usages:
```bash
# Basic creation
docker network create <network_name>

# Different driver
docker network create --driver bridge <bridge-network-name>
docker network create --driver host <host-network-name>
docker network create --driver none <none-network-name>

# With custom subnet
docker network create --subnet=172.20.0.0/16 <custom-network-name>

# With gateway
docker network create --subnet=172.20.0.0/16 --gateway=172.20.0.1 <custom-network-name>
```

---

4. Create containers in the network
```bash
docker run -d --name <container-name-01> --network <network-name> <image-name-01> 
docker run -d --name <container-name-02> --network <network-name> <image-name-02>
```

---

5. Connect Container(s) to the Network
```bash
docker network connect <network-name> <container-name-01>
docker network connect <network-name> <container-name-02>
```
- Verify the connection:
```bash
docker network inspect <network-name>
```

---

6. Disconnect Container(s) from the Network
```bash
docker network disconnect <network-name> <container-name-01>
docker network disconnect <network-name> <container-name-02>
```
- Verify the connection:
```bash
docker network inspect <network-name>
```

---

7. Remove a Network
- Stop and remove containers first:
```bash
docker stop <container-name-01> <container-name-02> 
docker rm <container-name-01> <container-name-02>
```

- Now remove the network:
```bash
docker network rm <network-name>
```

---

8. Prune Unused Networks

- It removes all the User created Docker networks that are NOT being used by any container.

```bash
docker network prune
docker network prune -f
```

- More precisely, it deletes:
  - Custom networks (bridge, overlay, macvlan, etc.)
  - That have zero containers attached

- It does NOT remove:
  - Networks currently in use by at least one container
  - Default Docker networks:
    - bridge
    - host
    - none
