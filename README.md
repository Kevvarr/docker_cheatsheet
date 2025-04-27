# 🐳 Docker Command Cheat Sheet for Personal Use

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

## 📄 Docker Compose File Structure

| Section | Description |
|---------|-------------|
| `version` | Specifies the Compose file format (e.g., `3.9`). |
| `services` | Defines each container in the application. |
| `volumes` | Named or bind-mounted volumes for persistent data. |
| `networks` | Custom bridge networks for isolated communication. |

---

## ⚙️ Service Configuration Options (With Examples)

| Key | Description | Example |
|-----|-------------|---------|
| `image` | The Docker image to use. | `image: nginx:latest` |
| `build` | Build from a Dockerfile. | `build: ./backend` |
| `container_name` | Name your container. | `container_name: my_backend` |
| `ports` | Map host:container ports. | `ports: ["8080:80"]` |
| `volumes` | Mount host directories or named volumes. | `volumes: ["./data:/data"]` |
| `environment` | Set environment variables. | `environment: ["NODE_ENV=production", "PORT=3000"]` |
| `env_file` | Load env variables from a file. | `env_file: .env` |
| `depends_on` | Define service start order. | `depends_on: ["db"]` |
| `networks` | Connect to one or more networks. | `networks: ["frontend"]` |
| `restart` | Restart policy on failure or stop. | `restart: unless-stopped` |
| `command` | Override default container command. | `command: ["npm", "start"]` |
| `entrypoint` | Override Docker image entrypoint. | `entrypoint: /entrypoint.sh` |
| `logging` | Configure logging driver. | `logging: { driver: "json-file" }` |
| `healthcheck` | Check if container is healthy. | `healthcheck: { test: ["CMD", "curl", "-f", "http://localhost"], interval: 30s }` |

---

## 🧠 Advanced Service Options (With Examples)

| Key | Description | Example |
|-----|-------------|---------|
| `labels` | Add metadata labels to containers. | `labels: ["app=backend", "tier=api"]` |
| `cap_add` | Add Linux capabilities. | `cap_add: ["NET_ADMIN", "SYS_TIME"]` |
| `cap_drop` | Remove Linux capabilities. | `cap_drop: ["ALL"]` |
| `ulimits` | Set resource limits. | `ulimits: { nofile: 65535 }` |
| `dns` | Specify custom DNS servers. | `dns: ["8.8.8.8", "1.1.1.1"]` |
| `extra_hosts` | Add entries to `/etc/hosts`. | `extra_hosts: ["local.dev:127.0.0.1"]` |
| `secrets` | Use Docker secrets (Swarm only). | `secrets: ["db_password"]` |
| `configs` | External config files (Swarm). | `configs: ["nginx_config"]` |
| `security_opt` | Security options like seccomp. | `security_opt: ["no-new-privileges:true"]` |
| `tmpfs` | Mount tmpfs (in-memory). | `tmpfs: /run` |
| `read_only` | Mount container root as read-only. | `read_only: true` |
| `stdin_open` | Keep STDIN open (for `docker attach`). | `stdin_open: true` |
| `tty` | Allocate a pseudo-TTY. | `tty: true` |
| `working_dir` | Set the working directory in container. | `working_dir: /app` |
| `user` | Run container as specific user. | `user: "1000:1000"` |
| `shm_size` | Set shared memory size. | `shm_size: 256m` |

---

## ➡️ Most simple docker compose yaml

```yaml
version: "3.8"

services:
  app:
    image: myapp:latest
    ports:
      - "8080:80"
```

---

## ➡️ Setup a Volume (for data persistence)

```yaml
services:
  db:
    image: postgres:14
    volumes:
      - db_data:/var/lib/postgresql/data

volumes:
  db_data:
```

---

## ➡️ Use an Environment File
1. Create a .env file: 
```
DB_USER=admin
DB_PASS=secret
```
2. Reference it automatically in your compose.yml:
```yaml
services:
  db:
    image: postgres:14
    environment:
      - POSTGRES_USER=${DB_USER}
      - POSTGRES_PASSWORD=${DB_PASS}
```

---

## ➡️ Use a Custom Environment File
1. If your env file is named differently (e.g., myvars.env):
```yaml
services:
  app:
    image: node:18
    env_file:
      - myvars.env
```

## ➡️ Mount a Configuration File as a Config

```yaml
services:
  nginx:
    image: nginx:latest
    configs:
      - source: nginx_config
        target: /etc/nginx/nginx.conf

configs:
  nginx_config:
    file: ./nginx.conf
```

---

## 🧪 Example: MongoDB + Backend Service

```yaml
version: "3.9"

services:
  mongodb:
    image: mongo:6
    container_name: mongo_db
    restart: unless-stopped
    ports:
      - "27017:27017"
    volumes:
      - mongo_data:/data/db
    environment:
      MONGO_INITDB_ROOT_USERNAME: root
      MONGO_INITDB_ROOT_PASSWORD: example
    logging:
      driver: json-file
      options:
        max-size: "10m"
        max-file: "3"
    healthcheck:
      test: ["CMD", "mongo", "--eval", "db.adminCommand('ping')"]
      interval: 30s
      timeout: 10s
      retries: 5

  backend:
    build: ./backend
    container_name: backend_app
    restart: unless-stopped
    ports:
      - "3000:3000"
    environment:
      MONGO_URI: mongodb://root:example@mongodb:27017
      NODE_ENV: production
    depends_on:
      - mongodb
    networks:
      - app_network
    volumes:
      - ./backend:/app
    working_dir: /app
    command: ["npm", "run", "start"]
    tty: true
    stdin_open: true

volumes:
  mongo_data:

networks:
  app_network:
```
