# Containerized Web Application with PostgreSQL (Docker + Macvlan)

##  Project Overview
This project demonstrates a containerized web application using:
- Node.js + Express (Backend API)
- PostgreSQL (Database)
- Docker & Docker Compose
- Macvlan networking with static IPs

---

## Architecture

Client (Postman / Curl)
        ↓
Backend Container (192.168.64.10)
        ↓
PostgreSQL Container (192.168.64.11)

---

##  Technologies Used

- Docker
- Docker Compose
- Node.js
- PostgreSQL
- Macvlan Networking
- Ubuntu (UTM VM)

---

## Features

- REST API (GET, POST, Health Check)
- Database integration
- Auto table creation
- Multi-stage Docker build
- Non-root user
- Persistent storage (volume)
- Static IP networking

---

##  Run Project

```bash
docker compose up -d --build

---

##  Step 1: Install Docker

```bash
sudo apt update
sudo apt install -y docker.io docker-compose
sudo systemctl start docker
sudo systemctl enable docker
sudo usermod -aG docker $USER
## create project structure
mkdir containerized-webapp
cd containerized-webapp
mkdir backend database screenshots
## backend setup
nano backend/app.js
nano backend/package.json
nano backend/Dockerfile
nano backend/.dockerignore
## database setup
nano database/init.sql
nano database/Dockerfile
nano database/.dockerignore
ip a
## create network
docker network create -d macvlan \
--subnet=192.168.64.0/24 \
--gateway=192.168.64.1 \
-o parent=enp0s1 \
mynet
## docker-compose.yml
nano docker-compose.yml
## fix and run
docker compose build
docker compose up -d
## macvlan isolation host
sudo ip link add macvlan-shim link enp0s1 type macvlan mode bridge
sudo ip addr add 192.168.64.50/24 dev macvlan-shim
sudo ip link set macvlan-shim up
## test api
curl http://192.168.64.10:3000/health
## insert data
curl -X POST http://192.168.64.10:3000/users \
-H "Content-Type: application/json" \
-d '{"name":"Omi"}'
## fetch data
curl http://192.168.64.10:3000/users
## test persistance 
docker compose down
docker compose up -d
## push to git
git init
git add .
git commit -m "Docker project"
git remote add origin https://github.com/ommishrx/containerized-webapp.git
git branch -M main
git push -u origin main
