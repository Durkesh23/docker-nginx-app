# 🚀 Docker + Nginx Deployment on AWS EC2

This project demonstrates how to deploy a Node.js application using Docker and configure Nginx as a reverse proxy on an AWS EC2 instance.

---

## 📌 Project Overview

* A simple Node.js application is containerized using Docker
* The container runs on port **3000**
* Nginx is configured to route traffic from **port 80 → port 3000**
* The application is accessible via the EC2 public IP without specifying a port

---

## 🛠️ Tech Stack

* AWS EC2 (Ubuntu)
* Docker
* Node.js
* Nginx

---

## ⚙️ Setup Steps

### 1. Launch EC2 Instance

* Ubuntu Server
* Open ports: **22, 80, 3000**

---

### 2. Install Docker

```bash
sudo apt update
sudo apt install docker.io -y
```

---

### 3. Create Node.js App

**app.js**

```javascript
const http = require("http");

const server = http.createServer((req, res) => {
  res.write("Hello from Docker App 🚀");
  res.end();
});

server.listen(3000);
```

---

### 4. Create Dockerfile

```dockerfile
FROM node:18
WORKDIR /app
COPY . .
CMD ["node", "app.js"]
```

---

### 5. Build & Run Container

```bash
sudo docker build -t myapp .
sudo docker run -d -p 3000:3000 myapp
```

---

### 6. Install & Configure Nginx

```bash
sudo apt install nginx -y
```

Edit config:

```nginx
server {
    listen 80;

    location / {
        proxy_pass http://127.0.0.1:3000;
    }
}
```

Restart Nginx:

```bash
sudo systemctl restart nginx
```

---

## 🌐 Access Application

```
http://16.171.62.115
```

---

## ✅ Result

* Application runs inside Docker container
* Nginx acts as reverse proxy
* No need to expose port 3000 publicly

---

## 💡 Learning Outcomes

* Docker containerization
* Nginx reverse proxy setup
* AWS EC2 deployment
* Debugging real-world issues

---

## 🔗 Author

Durkesh A
