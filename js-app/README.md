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
