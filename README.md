# BSCS-2112197 — DevOps Final Project

> **Student:** Shehzeen Apsara (2112197)
> **Course:** DevOps Fundamentals
> **Instructor:** Afaq Ahmed
> **Repository:** https://github.com/S-Apsara/2112197-Devops-Project
> **Live Health Endpoint:** http://98.81.210.203:8000/health

---

# Project Overview

This project demonstrates a complete DevOps workflow using **FastAPI**, **PostgreSQL**, **Docker**, **GitHub Actions**, and **AWS EC2**.

The application provides REST APIs for managing student records and includes:

* Containerized FastAPI application
* PostgreSQL database with persistent storage
* Docker Compose for multi-container orchestration
* CI pipeline using GitHub Actions (flake8 + pytest)
* CD pipeline using GitHub Actions and SSH deployment to EC2
* Feature branches and Pull Request workflow
* Public deployment on AWS EC2

---

# Architecture

```text
Developer Pushes Code to GitHub
            │
            ▼
 ┌───────────────────────┐
 │ GitHub Actions (CI)   │
 │-----------------------│
 │ • flake8 linting      │
 │ • pytest testing      │
 └───────────────────────┘
            │
            ▼
 ┌───────────────────────┐
 │ GitHub Actions (CD)   │
 │-----------------------│
 │ • SSH into EC2        │
 │ • git pull            │
 │ • docker compose up   │
 └───────────────────────┘
            │
            ▼
 ┌───────────────────────┐
 │ AWS EC2 Instance      │
 │-----------------------│
 │ FastAPI + PostgreSQL  │
 │ Docker Containers     │
 └───────────────────────┘
```

---

# Technologies Used

| Technology     | Purpose               |
| -------------- | --------------------- |
| FastAPI        | Backend REST API      |
| PostgreSQL 15  | Database              |
| SQLAlchemy     | ORM                   |
| Docker         | Containerization      |
| Docker Compose | Multi-container setup |
| Git & GitHub   | Version control       |
| GitHub Actions | CI/CD                 |
| AWS EC2        | Cloud deployment      |
| pytest         | Automated testing     |
| flake8         | Code linting          |

---

# Services

### web

* FastAPI application
* Runs on **port 8000**
* Exposes REST APIs

### db

* PostgreSQL 15
* Persistent named Docker volume
* Stores student records

---

# API Endpoints

| Method | Endpoint             | Description                        |
| ------ | -------------------- | ---------------------------------- |
| GET    | `/health`            | Health check and database status   |
| POST   | `/students`          | Create a student                   |
| GET    | `/students`          | Get all students                   |
| GET    | `/students/{reg_no}` | Get student by registration number |

---

# Health Endpoint Response

Example:

```json
{
  "status": "ok",
  "db": "connected",
  "student": "2112197"
}
```

---

# Local Setup

## Prerequisites

* Docker
* Docker Compose
* Python 3.12

## Clone Repository

```bash
git clone https://github.com/S-Apsara/2112197-Devops-Project.git

cd 2112197-Devops-Project
```

## Configure Environment

```bash
cp .env.example .env
```

Edit `.env` according to your environment.

## Run Application

```bash
docker compose up --build
```

Application:

```text
http://localhost:8000
```

Health Check:

```bash
curl http://localhost:8000/health
```

---

# Testing

Run tests locally:

```bash
pip install -r requirements.txt

pytest app/tests/ -v
```

Linting:

```bash
flake8 app/ --max-line-length=100
```

---

# Continuous Integration (CI)

GitHub Actions CI pipeline performs:

* Code checkout
* Python 3.12 setup
* Dependency installation
* flake8 linting
* pytest execution

Workflow file:

```text
.github/workflows/ci.yml
```

---

# Continuous Deployment (CD)

Deployment pipeline is configured to:

1. Trigger on push to `main`
2. SSH into EC2
3. Pull latest code
4. Rebuild Docker containers
5. Restart services

Workflow file:

```text
.github/workflows/cd.yml
```

Required GitHub Secrets:

| Secret      | Description                 |
| ----------- | --------------------------- |
| EC2_HOST    | Public IP of EC2 instance   |
| EC2_SSH_KEY | Contents of PEM private key |

---

# AWS EC2 Deployment

EC2 Configuration:

* Instance Type: t3.micro
* OS: Ubuntu
* Region: us-east-1
* Open Ports:

  * 22 (SSH)
  * 8000 (FastAPI)

Deployment Commands:

```bash
git clone https://github.com/S-Apsara/2112197-Devops-Project.git

cd 2112197-Devops-Project

docker compose -f docker-compose.prod.yml up -d --build
```

---

# Git Workflow

This project follows a feature-branch workflow.

Implemented:

* Main branch
* Feature branches
* Pull Requests
* Merged branches into main

Example commit messages:

```text
feat: initial project setup
feat: update health documentation
docs: update architecture section
fix: resolve flake8 lint errors
```

---

# Project Checklist

* Public GitHub repository
* FastAPI + PostgreSQL application
* Dockerized services
* Docker Compose orchestration
* Health endpoint with DB status
* Student CRUD APIs
* Persistent PostgreSQL storage
* GitHub Actions CI
* GitHub Actions CD
* AWS EC2 deployment
* Feature branches and Pull Requests
* Automated tests with pytest
* Linting with flake8

---

## Live Demo

Health Endpoint:

http://98.81.210.203:8000/health

Swagger Documentation:

http://98.81.210.203:8000/docs

---

**DevOps Fundamentals Final Project**

**Student:** Shehzeen Apsara (2112197)
