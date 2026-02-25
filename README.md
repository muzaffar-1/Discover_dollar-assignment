# DevOps Engineer Internship Assignment

## 📌 Project Overview

This assignment demonstrates the containerization and deployment of a full-stack MEAN (MongoDB, Express, Angular 15, Node.js) application using Docker, Docker Compose, GitHub Actions, and AWS EC2.

The application provides full CRUD functionality to manage tutorials (Create, Read, Update, Delete).

---

## 🏗️ Architecture Overview

GitHub → GitHub Actions → Docker Hub → AWS EC2 → Docker Compose → MongoDB + Backend + Frontend (Nginx)

### Services Used

- MongoDB (Database)
- Node.js + Express (Backend API)
- Angular 15 (Frontend)
- Nginx (Serving frontend on port 80)
- Docker & Docker Compose
- GitHub Actions (CI/CD)
- AWS EC2 (Deployment server)

---

## 🐳 Containerization

### Backend

- Base Image: `node:18`
- Working Directory: `/app`
- Dependencies installed using `npm install`
- Port Exposed: `8080`
- Runs using `node server.js`

### Frontend

- Multi-stage Docker build
- Stage 1: Angular production build
- Stage 2: Nginx Alpine image (lightweight)
- Final image size optimized (~60MB)
- Served via port `80`

---

## 🐙 Docker Compose Setup

Three services are defined:

- `mongo`
- `backend`
- `frontend`

Containers communicate using Docker internal networking.

MongoDB connection uses service name instead of localhost:
mongodb://mongo:27017/tutorials

Run locally using:

docker compose up -d


---

## ☁️ AWS Deployment

- EC2 Instance: Ubuntu (Free Tier)
- Docker & Docker Compose installed
- Security Group Ports Open:
  - 22 (SSH)
  - 80 (Frontend)
  - 8080 (Backend - optional)
  - 27017 (MongoDB - optional)

Application is accessible at:
http://<EC2-PUBLIC-IP>

---

## 🔄 CI/CD Pipeline (GitHub Actions)

Pipeline triggers automatically on push to `main` branch.

### Workflow Steps

1. Checkout repository
2. Login to Docker Hub using GitHub Secrets
3. Build backend Docker image
4. Push backend image to Docker Hub
5. Build frontend Docker image (multi-stage)
6. Push frontend image to Docker Hub
7. SSH into EC2
8. Execute:
   - `docker compose down`
   - `docker compose pull`
   - `docker compose up -d`

This ensures automated deployment after every update.

---

## 🔐 GitHub Secrets Used

- DOCKER_USERNAME
- DOCKER_PASSWORD
- EC2_HOST
- EC2_USER
- EC2_SSH_KEY

---

## 📸 Screenshots

### Docker Containers Running
![Docker PS](screenshots/docker-ps.png)

### Docker Images Built
![Docker Images](screenshots/docker-images.png)

### Images Pushed to Docker Hub
![Docker Hub Push](screenshots/images-pushed-to-dockerhub.png)

### Docker Hub Repositories
![Docker Hub Repos](screenshots/dockerhub-repos.png)

### GitHub Actions Successful Run
![GitHub Actions](screenshots/github-actions-success.png)

### Application UI
![Application UI](screenshots/app-ui.png)

---

## 🎯 DevOps Concepts Demonstrated

- Docker containerization
- Multi-stage Docker builds
- Docker Compose orchestration
- Service-to-service networking
- AWS EC2 deployment
- CI/CD automation
- Nginx reverse proxy setup
- Infrastructure persistence

---

## ✅ Final Result

The MEAN stack application is successfully:

- Containerized using Docker
- Orchestrated using Docker Compose
- Deployed on AWS EC2
- Exposed via port 80
- Automated using GitHub Actions CI/CD
- Ready for live demonstration
