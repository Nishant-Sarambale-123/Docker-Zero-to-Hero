Here are **commonly asked Docker scenario-based questions in DevOps interviews**, with **clear, practical answers** tailored for **3–4 years experience** (like your profile). These are framed the way interviewers expect you to answer 👇

---

## 1️⃣ Container exits immediately after starting

**Scenario:**
A container starts and stops immediately. How do you troubleshoot?

**Answer:**

* Check container status:

```bash
docker ps -a
```

* View logs:

```bash
docker logs <container_id>
```

* Run container in interactive mode:

```bash
docker run -it <image> /bin/bash
```

* Check if the main process (CMD/ENTRYPOINT) is exiting.
* Verify application config, ports, and environment variables.

**Key point:**

> A container lives as long as its main process runs.

---

## 2️⃣ Application works locally but fails in Docker

**Scenario:**
The app runs fine locally but crashes inside the container.

**Answer:**

* Check missing dependencies in Dockerfile
* Verify correct base image
* Ensure correct environment variables
* Check file paths and permissions
* Compare local vs container OS differences (Alpine vs Ubuntu)

```bash
docker exec -it <container> sh
```

---

## 3️⃣ How do containers communicate with each other?

**Scenario:**
Two containers need to talk to each other.

**Answer:**

* Use **Docker user-defined bridge network**

```bash
docker network create mynet
docker run --network mynet --name app1 ...
docker run --network mynet --name app2 ...
```

* Containers communicate using **container names**, not IPs.

**Avoid:**
❌ Using `localhost`
❌ Hardcoding IP addresses

---

## 4️⃣ Environment variables differ per environment

**Scenario:**
Same image, different configs for dev, QA, prod.

**Answer:**
Use **env files**:

```bash
docker run --env-file dev.env myapp
```

Or pass variables directly:

```bash
docker run -e DB_HOST=prod-db myapp
```

**Best practice:**

> Image should be immutable; config should be external.

---

## 5️⃣ How do you reduce Docker image size?

**Scenario:**
Docker image is too large and slow to deploy.

**Answer:**

* Use smaller base images (Alpine)
* Use multi-stage builds
* Remove unnecessary files
* Combine RUN commands
* Clean package cache

```dockerfile
FROM node:18-alpine
```

---

## 6️⃣ How do you persist data in Docker?

**Scenario:**
Container restarts and data is lost.

**Answer:**
Use **volumes**:

```bash
docker volume create mydata
docker run -v mydata:/app/data myapp
```

Or **bind mounts** for local dev.

**Interview line:**

> Containers are ephemeral, data should live outside containers.

---

## 7️⃣ Container is running but application is not accessible

**Scenario:**
Container is up but app is not reachable.

**Answer:**

* Check port mapping:

```bash
docker ps
```

* Verify correct EXPOSE and application port
* Confirm app listens on `0.0.0.0`, not `localhost`
* Check firewall/security group (in AWS)

---

## 8️⃣ How do you debug a running container?

**Scenario:**
Production container has an issue.

**Answer:**

```bash
docker exec -it <container> /bin/bash
```

* Check logs
* Inspect environment variables
* Check disk, memory, CPU usage:

```bash
docker stats
```

---

## 9️⃣ How do you handle logs in Docker?

**Scenario:**
Need centralized logging.

**Answer:**

* Send logs to stdout/stderr
* Use logging drivers (json-file, awslogs, fluentd)
* In Kubernetes → use EFK / Prometheus

```bash
docker logs <container>
```

---

## 🔟 Docker image vs container (Scenario framing)

**Question:**
You updated code but running container still shows old version. Why?

**Answer:**

* Image was not rebuilt
* Container is running old image
* Need:

```bash
docker build -t myapp .
docker stop old
docker run myapp
```

---

## 1️⃣1️⃣ Docker in CI/CD pipeline

**Scenario:**
How do you use Docker in Jenkins/GitHub Actions?

**Answer:**

* Build image
* Run tests inside container
* Push image to registry (ECR/Docker Hub)
* Deploy via Kubernetes/ECS

---

## 1️⃣2️⃣ Security issue in Docker container

**Scenario:**
How do you secure containers?

**Answer:**

* Use non-root user
* Scan images (Trivy)
* Minimal base image
* Don’t store secrets in image
* Use read-only filesystem

---

## ⭐ Interview Tip (Very Important)

When answering **scenario questions**, always structure like:

1. **What I check first**
2. **Commands/tools used**
3. **Root cause**
4. **Best practice**

---

If you want, I can also give:

* 🔥 **Real production Docker issues & fixes**
* 📌 **Docker + Kubernetes scenario questions**
* 🎯 **One-line interview answers**

Just tell me 👍
