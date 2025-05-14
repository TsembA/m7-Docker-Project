# 🐳 Module 7 Demo Project: Deploy Docker App on Remote Server with Docker Compose

## 🛠️ Technologies Used
- **Docker & Docker Compose** – For container orchestration and service definition.
- **Amazon ECR** – Private container registry to store application images.
- **Node.js** – Backend service containerized for deployment.
- **MongoDB** – NoSQL database container.
- **MongoExpress** – Web-based UI to interact with MongoDB.

---

## 📄 Project Description

This project demonstrates how to deploy a Dockerized application on a remote server using Docker Compose. It includes:

- Copying the `docker-compose.yml` file to a cloud server
- Logging into a private Docker registry (Amazon ECR)
- Pulling a prebuilt application image
- Running services for the app, MongoDB, and MongoExpress

---

## ✅ Step-by-Step Guide

### Step 1: Copy `docker-compose.yml` to the Remote Server
```bash
scp docker-compose.yml user@<REMOTE_SERVER_IP>:/home/user/app/
```

---

### Step 2: SSH into the Remote Server
```bash
ssh user@<REMOTE_SERVER_IP>
cd /home/user/app/
```

---

### Step 3: Login to Amazon ECR
Use the AWS CLI to authenticate Docker with ECR:

```bash
aws ecr get-login-password --region us-west-1 | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.us-west-1.amazonaws.com
```

---

### Step 4: Pull the Application Image
```bash
docker pull <aws_account_id>.dkr.ecr.us-west-1.amazonaws.com/your-app-image:latest
```

> Make sure your `docker-compose.yml` references this image correctly.

---

### Step 5: Start All Services with Docker Compose
```bash
docker-compose up -d
```

---

## 📦 Example `docker-compose.yml`
```yaml
version: "3.8"

services:
  app:
    image: <aws_account_id>.dkr.ecr.us-west-1.amazonaws.com/your-app-image:latest
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
      - ME_CONFIG_BASICAUTH_USERNAME=admin
      - ME_CONFIG_BASICAUTH_PASSWORD=admin

volumes:
  mongo-data:
```

---

## 🎯 Result

Your Dockerized Node.js application is now running on a remote server with MongoDB and MongoExpress, with images pulled securely from Amazon ECR.

You can access:
- App: `http://<REMOTE_SERVER_IP>:3000`
- MongoExpress: `http://<REMOTE_SERVER_IP>:8081`
