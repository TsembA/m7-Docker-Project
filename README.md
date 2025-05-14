# 🐳 What is Docker? + Project

Docker is an **open-source containerization platform** that allows developers to package applications and their dependencies into **containers**. Containers provide a **consistent environment** to run applications across development, testing, and production.

---

## 📦 What is a Docker Container?

A **Docker container** is a **lightweight**, **portable**, and **isolated** environment used to run applications.

### ✅ Key Features:

- **Portability**: Runs consistently across any system that supports Docker.
- **Isolation**: Applications run independently for better security and stability.
- **Lightweight**: Shares host OS kernel, unlike virtual machines.

---

## 🖼️ What is a Docker Image?

A **Docker image** is a file that defines a container. It includes:

- Base OS or environment
- Application code
- Dependencies and configs
- Startup command

Images are read-only templates used to create containers.

---

## 🛠️ Docker Architecture

- **Docker Engine**: Core of Docker, manages containers.
  - Docker Server
  - Docker API
  - Docker CLI
- **Container Runtime**: Runs containers
- **Volumes**: Persistent data storage
- **Networks**: Container communication
- **Build System**: Uses Dockerfiles to build images

---

## 🖥️ Common Docker Commands

### 📁 Image & Container Management

```bash
docker images               # List images
docker pull <image>        # Download image
docker run <image>         # Start container
docker run -d <image>      # Detached mode
docker stop <id>           # Stop container
docker start <id>          # Start stopped container
docker ps                  # Running containers
docker ps -a               # All containers
docker rm <id>             # Remove container
docker rmi <id>            # Remove image
```

### 🔗 Networking & Volumes

```bash
docker network ls                  # List networks
docker network create <name>      # Create network
docker volume create <name>       # Create volume
```

### ⚙️ Interacting with Containers

```bash
docker run -p 3000:3000 <image>     # Port mapping
docker exec -it <id> sh             # Shell inside container
docker logs <id>                    # View logs
```

---

## 📄 Dockerfile Example

```dockerfile
FROM node:20-alpine

ENV MONGO_DB_USERNAME=admin 
ENV MONGO_DB_PWD=password

RUN mkdir -p /home/app
COPY ./app /home/app
WORKDIR /home/app
RUN npm install

CMD ["node", "server.js"]
```

---

## 📋 Docker Best Practices

### ✅ Image Building

- **Use official base images** (e.g., `node:20-alpine`)
- **Pin versions** to avoid breaking changes
- **Minimize image size**: Keep it clean
- **Add `.dockerignore`** to exclude unnecessary files
- **Write clean, commented Dockerfiles**
