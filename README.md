# 🐳 Docker Command Cheat Sheet for personal use
![hN4lt](https://miro.medium.com/v2/resize:fit:1372/0*X34tDynHLvheJOKN)

---

## 🚀 Basic Docker Commands

| Command | Description |
|--------|-------------|
| `docker version` | Show Docker version |
| `docker info` | Display system-wide Docker info |
| `docker help` | Show general Docker help |

---

## 📦 Image Management

| Command | Description |
|--------|-------------|
| `docker pull <image>` | Download an image from registry |
| `docker images` | List all local images |
| `docker rmi <image>` | Remove an image |
| `docker build -t <name>:<tag> .` | Build image from Dockerfile |
| `docker image prune` | Remove dangling images |

---

## 🧱 Container Management

| Command | Description |
|--------|-------------|
| `docker run -it <image> bash` | Run a container interactively |
| `docker run -d -p 8080:80 <image>` | Run container in detached mode with port mapping |
| `docker run --name <name> <image>` | Run container with custom name |
| `docker ps` | List running containers |
| `docker ps -a` | List all containers (including stopped) |
| `docker stop <id|name>` | Stop container |
| `docker start <id|name>` | Start container |
| `docker restart <id|name>` | Restart container |
| `docker rm <id|name>` | Remove a container |
| `docker exec -it <id|name> bash` | Open shell in running container |
| `docker logs -f <id|name>` | Follow logs of a container |

---

## 🗃️ Volume Management

| Command | Description |
|--------|-------------|
| `docker volume create <name>` | Create a new volume |
| `docker volume ls` | List all volumes |
| `docker volume inspect <name>` | View details of a volume |
| `docker volume rm <name>` | Remove a volume |
| `docker run -v <volume>:/data <image>` | Mount volume into container |

---

## 🌐 Network Management

| Command | Description |
|--------|-------------|
| `docker network ls` | List all Docker networks |
| `docker network create <name>` | Create a custom network |
| `docker network inspect <name>` | Show network details |
| `docker network rm <name>` | Remove a network |
| `docker run --network=<name> <image>` | Connect container to a network |

---

## 🧭 Docker Networking Types

| Network Type | Description |
|--------------|-------------|
| `bridge` (default) | Default for standalone containers. Provides NAT'd network via a bridge interface. |
| `host` | Shares host’s networking namespace. No isolation—container uses host’s IP and ports. |
| `none` | No network access. Container is fully isolated from networking. |
| `overlay` | Multi-host network using Docker Swarm or other orchestrators. |
| `macvlan` | Assigns a MAC address to the container so it appears as a physical device on the network. |
| `ipvlan` | Like `macvlan`, but relies on IP address isolation. |

> 💡 To specify a network:  
> `docker run --network=host <image>`  
> `docker network create --driver=overlay my_overlay_net`

---

## 📤 Registry & Docker Hub

| Command | Description |
|--------|-------------|
| `docker login` | Authenticate to Docker Hub |
| `docker tag <local> <user>/<repo>:<tag>` | Tag image for push |
| `docker push <user>/<repo>:<tag>` | Push image to registry |
| `docker pull <user>/<repo>:<tag>` | Pull image from registry |

---

## 🧹 Cleanup & Pruning

| Command | Description |
|--------|-------------|
| `docker system prune` | Clean up unused resources (images, containers, volumes) |
| `docker container prune` | Remove all stopped containers |
| `docker image prune` | Remove unused images |
| `docker volume prune` | Remove unused volumes |

---

## 🕵️ Debug & Inspect

| Command | Description |
|--------|-------------|
| `docker inspect <id|name>` | Detailed inspection (JSON) |
| `docker diff <id|name>` | Changes made to container filesystem |
| `docker top <id|name>` | Running processes in container |
| `docker stats` | Real-time resource usage stats |

---

## 🧰 Useful Options

| Option | Description |
|--------|-------------|
| `-d` | Detached mode (run in background) |
| `-it` | Interactive + TTY |
| `--rm` | Auto-remove container after exit |
| `--name <name>` | Name the container |
| `-v <vol>:/path` | Bind volume |
| `-p host:container` | Port mapping |
| `--env KEY=val` | Set environment variable |
| `--network <name>` | Use specific network |

---

## 🛠 Docker Compose

| Command | Description |
|--------|-------------|
| `docker-compose up -d` | Start services in detached mode |
| `docker-compose down` | Stop and remove containers, networks |
| `docker-compose build` | Build images |
| `docker-compose logs -f` | Follow service logs |
| `docker-compose exec <svc> bash` | Open shell in service container |

---

## 📚 Helpful Resources

| Resource | Link |
|---------|------|
| Docker Docs | [https://docs.docker.com/](https://docs.docker.com/) |
| Docker CLI Reference | [https://docs.docker.com/engine/reference/commandline/cli/](https://docs.docker.com/engine/reference/commandline/cli/) |

---

✅ With these commands, you're well on your way to mastering containerization with Docker!
