# CasaGrito - Infrastructure & Deployment

This repository showcases the **DevOps and Infrastructure** architecture for **CasaGrito**, a full-stack transactional platform for event ticketing. 

The focus of this setup is **security, automation, and high availability** using a containerized approach.

## 🛠 Tech Stack & Tools
* **Orchestration:** Docker & Docker Compose.
* **Web Server & Proxy:** Nginx (configured as a Reverse Proxy with SSL hardening).
* **CI/CD:** GitHub Actions for automated deployment.
* **Environment:** Linux (Ubuntu Server) hosted on DigitalOcean.
* **Database:** PostgreSQL (Containerized with persistent volumes).

## 🛡 Security Implementations
As a **Vulnerability Analyst**, I implemented the following security measures:
* **SSL/TLS Encryption:** Secured via Certbot and Let's Encrypt.
* **Nginx Hardening:** Custom configurations to prevent common web vulnerabilities and hide server signatures.
* **Network Isolation:** Docker internal networking to isolate the database from public access.
* **Environment Management:** Use of `.env` files to manage sensitive credentials (not included in this repo).

## 🚀 Deployment Workflow
1. **Continuous Integration:** Every push to the main branch triggers a GitHub Action.
2. **Build:** Docker images are built and validated.
3. **Continuous Deployment:** Automatic deployment to the VPS via SSH, ensuring zero-downtime (or minimal) by using optimized container restarts.

## 📂 Key Files in this Repository
* `docker-compose.yml`: Defines the multi-container architecture (Backend, Frontend, DB).
* `nginx.conf`: Production-ready reverse proxy configuration.
* `Dockerfile`: Optimized build stages for the NestJS backend.
* `.github/workflows/`: Automated deployment pipelines.

---
*Note: This repository only contains infrastructure-related code to demonstrate DevOps practices.*
