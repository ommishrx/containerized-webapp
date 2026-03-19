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
