Here’s a comprehensive list of **Docker interview questions and answers for DevOps roles**, divided into **basic**, **intermediate**, and **advanced** levels — including **scenario-based questions** frequently asked in DevOps interviews.

---

### 🟢 **Basic Docker Questions**

#### 1. **What is Docker?**

**Answer:** Docker is an open-source containerization platform that allows you to package applications and their dependencies into containers. These containers are portable and run consistently across different environments.

---

#### 2. **What is a Docker container?**

**Answer:** A container is a lightweight, standalone, executable package that includes everything needed to run a piece of software — code, runtime, system tools, libraries, and settings.

---

#### 3. **What is the difference between Docker containers and virtual machines (VMs)?**

**Answer:**

| Docker Container     | Virtual Machine    |
| -------------------- | ------------------ |
| Shares OS kernel     | Has its own OS     |
| Lightweight and fast | Heavy and slow     |
| Uses fewer resources | Resource-intensive |

---

#### 4. **What is Dockerfile?**

**Answer:** A Dockerfile is a text file that contains a set of instructions to build a Docker image. It defines what goes into the container, such as base image, environment variables, commands, etc.

---

#### 5. **What is a Docker image?**

**Answer:** An image is a lightweight, immutable template used to create containers. It is built using a Dockerfile and contains the application and its environment.

---

### 🟡 **Intermediate Docker Questions**

#### 6. **What is the difference between `CMD` and `ENTRYPOINT` in Dockerfile?**

**Answer:**

* `CMD`: Provides default arguments for the container.
* `ENTRYPOINT`: Defines the main command to run inside the container.
* They can be combined for flexibility.

---

#### 7. **How do you persist data in Docker?**

**Answer:** By using **Volumes** or **Bind Mounts**.

* **Volumes**: Managed by Docker, recommended for production.
* **Bind Mounts**: Map host file system directories into containers.

---

#### 8. **How do you expose a port in Docker?**

**Answer:** Use the `-p` flag in `docker run`, like:

```bash
docker run -p 8080:80 nginx
```

This maps port 80 inside the container to port 8080 on the host.

---

#### 9. **How do you copy files into a Docker container?**

**Answer:** Using `COPY` or `ADD` in Dockerfile, or

```bash
docker cp myfile.txt container_id:/app/
```

---

#### 10. **What is Docker Compose?**

**Answer:** Docker Compose is a tool to define and run multi-container Docker applications using a `docker-compose.yml` file. It simplifies the orchestration of services, networks, and volumes.

---

### 🔴 **Advanced Docker Questions**

#### 11. **How do you optimize Docker images for production?**

**Answer:**

* Use minimal base images (like `alpine`)
* Combine `RUN` commands
* Use `.dockerignore`
* Clean up unnecessary files (e.g., apt caches)
* Use multi-stage builds

---

#### 12. **What are multi-stage builds in Docker?**

**Answer:** Multi-stage builds help reduce image size by using intermediate containers to build dependencies, and then copying only necessary files into the final image.

```Dockerfile
FROM golang:alpine AS builder
WORKDIR /app
COPY . .
RUN go build -o app

FROM alpine
COPY --from=builder /app/app .
CMD ["./app"]
```

---

#### 13. **How do you handle secret management in Docker?**

**Answer:**

* Avoid adding secrets directly into images.
* Use environment variables or Docker secrets (in Swarm).
* Use tools like HashiCorp Vault or AWS Secrets Manager.

---

#### 14. **What is the difference between `docker stop` and `docker kill`?**

**Answer:**

* `docker stop`: Sends `SIGTERM`, allows graceful shutdown.
* `docker kill`: Sends `SIGKILL`, forcefully terminates the container.

---

#### 15. **How do you troubleshoot a failing Docker container?**

**Answer:**

* `docker ps -a` to see status
* `docker logs <container>` to view logs
* `docker inspect <container>` for config/debug info
* `docker exec -it <container> sh` to access the container shell

---

### 🧩 **Scenario-Based Docker Questions**

#### 16. **Your container keeps restarting. How do you investigate the cause?**

**Answer:**

* Check `docker ps -a` for restart reason.
* View logs using `docker logs <container>`.
* Use `docker inspect` to view restart policies.
* Verify entrypoint or CMD is valid.

---

#### 17. **You want to deploy a Python app with Redis and Nginx in Docker. How would you set it up?**

**Answer:** Use Docker Compose:

```yaml
version: '3'
services:
  app:
    build: .
    ports:
      - "5000:5000"
    depends_on:
      - redis
  redis:
    image: redis:alpine
  nginx:
    image: nginx
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
```

---

#### 18. **How do you ensure zero downtime deployments using Docker?**

**Answer:**

* Use rolling updates (in Swarm or Kubernetes)
* Load balancers with health checks
* Run new containers before stopping old ones

---

#### 19. **You need to reduce the Docker image size of a Node.js app. What steps will you take?**

**Answer:**

* Use `node:alpine` base image
* Remove dev dependencies
* Use `.dockerignore`
* Use multi-stage builds

---

#### 20. **How would you patch a container running in production without redeploying?**

**Answer:**

* Use `docker exec` to access and apply temporary fixes
* Commit changes using `docker commit` (not recommended for long-term)
* Best practice: Update Dockerfile → rebuild → redeploy

---

### ✅ **Quick Commands Cheat Sheet**

| Task             | Command                        |
| ---------------- | ------------------------------ |
| List containers  | `docker ps -a`                 |
| Start container  | `docker start <id>`            |
| Stop container   | `docker stop <id>`             |
| Remove container | `docker rm <id>`               |
| Build image      | `docker build -t myapp .`      |
| Run container    | `docker run -d -p 80:80 myapp` |
| Show logs        | `docker logs <id>`             |

---

Let me know if you'd like:

* A **Docker MCQ quiz**
* Docker questions for **SRE/Cloud interviews**
* **Kubernetes + Docker combined** scenario questions
