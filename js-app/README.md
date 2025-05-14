# 🐳 Module 7 Demo Project: Use Docker for Local Development

## 🛠️ Technologies Used
- **Docker** – Container platform for building and running isolated applications.
- **Node.js** – JavaScript runtime used for the backend application.
- **MongoDB** – NoSQL database container.
- **MongoExpress** – Web-based MongoDB UI container.

---

## 📄 Project Description

This project demonstrates how to use **Docker** to containerize a local development environment. It includes:

- A Node.js backend application running in a Docker container.
- A MongoDB database container for persistence.
- A MongoExpress container as a web UI for managing MongoDB.

---

## ✅ Step-by-Step Guide

### Step 1: Create a `Dockerfile` for the Node.js App
```dockerfile
# Dockerfile
FROM node:18

WORKDIR /app

COPY package*.json ./
RUN npm install

COPY . .

EXPOSE 3000
CMD ["npm", "start"]
```

---

### Step 2: Create a `docker-compose.yml` File
```yaml
version: "3.8"

services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - MONGO_URL=mongodb://mongo:27017/mydatabase
    depends_on:
      - mongo

  mongo:
    image: mongo
    ports:
      - "27017:27017"
    volumes:
      - mongo-data:/data/db

  mongo-express:
    image: mongo-express
    ports:
      - "8081:8081"
    environment:
      - ME_CONFIG_MONGODB_SERVER=mongo
      - ME_CONFIG_MONGODB_PORT=27017
      - ME_CONFIG_BASICAUTH_USERNAME=admin
      - ME_CONFIG_BASICAUTH_PASSWORD=admin

volumes:
  mongo-data:
```

---

### Step 3: Build and Start the Environment
```bash
docker-compose up --build
```

---

### Step 4: Access the Services

- **Node.js App**: [http://localhost:3000](http://localhost:3000)
- **MongoExpress UI**: [http://localhost:8081](http://localhost:8081)

---

### Step 5: Manage and Verify

- Use MongoExpress to verify documents in your MongoDB collections.
- Modify your Node.js app and restart the container to reflect changes.

---

## 🎯 Result

You now have a fully containerized local development environment using Docker Compose with:

- A live-running Node.js backend
- Persistent MongoDB database
- Visual MongoDB management UI via MongoExpress

This setup boosts productivity and ensures consistency across development environments.
