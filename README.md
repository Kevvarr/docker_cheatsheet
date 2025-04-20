# 🐳 Docker Command Cheat Sheet for Personal Use

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
| `docker build --no-cache -t <name>:<tag> .` | Build without using cache |
| `docker image prune -a` | Remove all unused images |
| `docker image ls -a` | Show all images, including intermediate |
| `docker commit <container> <image>:<tag>` | Create a new image from a container’s changes |


---

## 🧱 Container Management

| Command | Description |
|--------|-------------|
| `docker run -it <image> bash` | Run a container interactively |
| `docker run -d -p 8080:80 <image>` | Run container in detached mode with port mapping |
| `docker run --name <name> <image>` | Run container with custom name |
| `docker run --rm <image>` | Auto-remove container after it exits |
| `docker run -e VAR=value <image>` | Pass environment variables |
| `docker run --mount type=bind,source="$(pwd)",target=/app <image>` | Mount a host directory |
| `docker ps` | List running containers |
| `docker ps -a` | List all containers (including stopped) |
| `docker stop <id\|name>` | Stop container |
| `docker start <id\|name>` | Start container |
| `docker restart <id\|name>` | Restart container |
| `docker rm <id\|name>` | Remove a container |
| `docker exec -it <id\|name> bash` | Open shell in running container |
| `docker logs -f <id\|name>` | Follow logs of a container |

---

## 🗃️ Volume Management

| Command | Description |
|--------|-------------|
| `docker volume create <name>` | Create a new volume |
| `docker volume ls` | List all volumes |
| `docker volume inspect <name>` | View details of a volume |
| `docker volume rm <name>` | Remove a volume |
| `docker run -v <volume>:/data <image>` | Mount volume into container |
| `docker run --mount source=<volume>,target=/data <image>` | Alternative mounting method |

---

## 🌐 Network Management

| Command | Description |
|--------|-------------|
| `docker network ls` | List all Docker networks |
| `docker network create <name>` | Create a custom network |
| `docker network inspect <name>` | Show network details |
| `docker network rm <name>` | Remove a network |
| `docker run --network=<name> <image>` | Connect container to a specific network |
| `docker network create --driver bridge <name>` | Create bridge network |
| `docker network create --driver overlay <name>` | Create overlay network |

---

## 🧭 Docker Networking Types

![Networking Types](https://miro.medium.com/v2/resize:fit:1372/0*X34tDynHLvheJOKN)

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
| `docker system prune -a` | Clean up unused resources + all unused images |
| `docker container prune` | Remove all stopped containers |
| `docker image prune` | Remove unused images |
| `docker volume prune` | Remove unused volumes |
| `docker builder prune` | Remove build cache |

---

## 🕵️ Debug & Inspect

| Command | Description |
|--------|-------------|
| `docker inspect <id\|name>` | Detailed inspection (JSON) |
| `docker diff <id\|name>` | Changes made to container filesystem |
| `docker top <id\|name>` | Running processes in container |
| `docker stats` | Real-time resource usage stats |
| `docker events` | Stream Docker events in real-time |

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
| `--mount type=bind\|volume` | More control over mounts |

---

## 🛠 Docker Compose

| Command | Description |
|--------|-------------|
| `docker-compose up -d` | Start services in detached mode |
| `docker-compose down` | Stop and remove containers, networks |
| `docker-compose build` | Build images |
| `docker-compose logs -f` | Follow service logs |
| `docker-compose exec <svc> bash` | Open shell in service container |
| `docker-compose ps` | List status of services |
| `docker-compose stop` | Stop services |
| `docker-compose restart` | Restart services |

---
