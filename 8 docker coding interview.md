Absolutely! Below are **detailed answers** to the **most common Docker coding questions** asked in **DevOps interviews**, covering basic to advanced levels:

---

### ✅ 1. **Write a Dockerfile to containerize a basic Python app**

#### **App file: `app.py`**

```python
from flask import Flask
app = Flask(__name__)

@app.route('/')
def home():
    return "Hello from Docker!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```

#### **Dockerfile**

```Dockerfile
# Use official Python image
FROM python:3.9-slim

# Set working directory
WORKDIR /app

# Copy requirements and install dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the application code
COPY . .

# Expose the application port
EXPOSE 5000

# Run the app
CMD ["python", "app.py"]
```

#### **requirements.txt**

```
flask
```

---

### ✅ 2. **Build and Run Docker Image**

```bash
docker build -t my-python-app .
docker run -d -p 5000:5000 my-python-app
```

---

### ✅ 3. **Docker Commands**

* List all containers:

  ```bash
  docker ps -a
  ```

* Remove all stopped containers:

  ```bash
  docker container prune
  ```

* Remove dangling (unused) images:

  ```bash
  docker image prune
  ```

---

### ✅ 4. **Passing Environment Variables**

```bash
docker run -e ENV=prod my-python-app
```

**Or use a `.env` file:**

```env
ENV=prod
```

```bash
docker run --env-file .env my-python-app
```

---

### ✅ 5. **Multi-stage Dockerfile (for React app)**

```Dockerfile
# Stage 1: Build
FROM node:16 as build
WORKDIR /app
COPY . .
RUN npm install && npm run build

# Stage 2: Serve
FROM nginx:alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```

---

### ✅ 6. **`docker-compose.yml` for web + redis + postgres**

```yaml
version: '3.8'

services:
  web:
    build: .
    ports:
      - "5000:5000"
    depends_on:
      - redis
      - db

  redis:
    image: redis:alpine

  db:
    image: postgres
    environment:
      POSTGRES_DB: mydb
      POSTGRES_USER: user
      POSTGRES_PASSWORD: pass
    volumes:
      - pgdata:/var/lib/postgresql/data

volumes:
  pgdata:
```

---

### ✅ 7. **Run container with volume**

```bash
docker volume create pgdata
docker run -d \
  -e POSTGRES_PASSWORD=pass \
  -v pgdata:/var/lib/postgresql/data \
  postgres
```

---

### ✅ 8. **Debugging a failing container**

* View logs:

  ```bash
  docker logs <container_id>
  ```

* Access container:

  ```bash
  docker exec -it <container_id> /bin/bash
  ```

* Inspect metadata:

  ```bash
  docker inspect <container_id>
  ```

---

### ✅ 9. **Run with restart policy**

```bash
docker run -d --restart unless-stopped myapp
```

---

### ✅ 10. **If secrets are baked into image**

* Remove the image:

  ```bash
  docker rmi <image_id>
  ```

* Use **`--build-arg`**, secrets manager (e.g., AWS Secrets Manager), or `.env` + `.dockerignore`

---

### ✅ 11. **Image Optimization Tips**

* Use Alpine:

  ```Dockerfile
  FROM python:3.9-alpine
  ```

* Remove cache:

  ```Dockerfile
  RUN pip install --no-cache-dir ...
  ```

* Use `.dockerignore` to exclude unnecessary files

---

### ✅ 12. **Docker Security Best Practices**

* Use a non-root user:

  ```Dockerfile
  RUN adduser --disabled-password myuser
  USER myuser
  ```

* Use minimal base images (e.g., `distroless`, `alpine`)

* Scan image:

  ```bash
  trivy image myapp
  ```

---

### ✅ 13. **Reduce Docker Image Size**

* Use `.dockerignore`
* Use multi-stage builds
* Strip unnecessary dependencies
* Combine RUN commands to reduce layers

---

### ✅ 14. **ENTRYPOINT vs CMD**

| Aspect      | ENTRYPOINT                  | CMD                        |
| ----------- | --------------------------- | -------------------------- |
| Overridable | Not easily overridden       | Easily overridden          |
| Use case    | Fixed command (e.g. binary) | Default args (e.g. script) |
| Example     | `ENTRYPOINT ["python"]`     | `CMD ["app.py"]`           |

**Combined Example:**

```Dockerfile
ENTRYPOINT ["python"]
CMD ["app.py"]
```

---

Let me know if you'd like these questions in **mock interview format** or need **project-based questions with answers**!
