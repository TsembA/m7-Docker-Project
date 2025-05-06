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

---

## 🧩 Demo App: User Profile with Docker

This demo app consists of:

- ✅ `index.html` (vanilla JS & CSS)
- ✅ Node.js backend with Express
- ✅ MongoDB database
- ✅ Docker & Docker Compose setup

---

## 🚀 Getting Started

### 🔧 Option 1: Run with Docker CLI

#### Step 1: Create Network (optional)

```bash
docker network create mongo-network
```

#### Step 2: Start MongoDB

```bash
docker run -d \
  -p 27017:27017 \
  -e MONGO_INITDB_ROOT_USERNAME=admin \
  -e MONGO_INITDB_ROOT_PASSWORD=password \
  --name mongodb \
  --net mongo-network \
  mongo

```

#### Step 3: Start Mongo Express

```bash
docker run -d \
  -p 8081:8081 \
  -e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
  -e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
  -e ME_CONFIG_MONGODB_SERVER=mongodb \
  --net mongo-network \
  --name mongo-express \
  mongo-express

```

#### Step 4: Open Mongo Express UI

```
http://localhost:8081
```

Use it to create:

- Database: `user-account`
- Collection: `users`

#### Step 5: Start Node.js App

```bash
cd app
npm install
node server.js
```

#### Step 6: Open the App

```
http://localhost:3000
```

---

### 🐳 Option 2: Run with Docker Compose

#### Step 1: Start All Services

```bash
docker-compose -f docker-compose.yaml up
```

Mongo Express will be accessible at:

```
http://localhost:8080
```

#### Step 2: Create MongoDB Database & Collection

- Database: `user-account`
- Collection: `users`

#### Step 3: Start Node Server

```bash
cd app
npm install
node server.js
```

#### Step 4: Open the App

```
http://localhost:3000
```

---

## 🛠️ Build Image from Dockerfile

```bash
docker build -t my-app:1.0 .
```

> The dot (`.`) refers to the location of your Dockerfile.

---

## 📁 Folder Structure

```
.
├── app/
│   ├── index.html
│   ├── server.js
│   ├── package.json
├── docker-compose.yaml
├── Dockerfile
└── README.md
```

---

## ✅ Features

- Minimal and clean container setup
- MongoDB GUI via mongo-express
- Reusable across environments
- Hands-on with CLI and Compose

---

## 🙌 Final Notes

- Replace hardcoded creds in production!
- Use `.env` files for better secrets management

---
