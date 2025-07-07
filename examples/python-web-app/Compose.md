Here are **detailed notes on Docker Compose**, including syntax, structure, and real-world examples:

---

# 🧩 **Docker Compose – Full Detailed Notes with Syntax**

---

## 📌 **What is Docker Compose?**

**Docker Compose** is a tool for defining and managing multi-container Docker applications using a YAML file (`docker-compose.yml`). It lets you:

* Run multiple containers as a single service stack.
* Define container services, networks, and volumes declaratively.
* Use simple `docker-compose` CLI commands to manage the whole app.

---

## 🧱 **Docker Compose File Structure (`docker-compose.yml`)**

```yaml
version: "3"
services:
  service_name:
    image: <image_name>
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "host_port:container_port"
    volumes:
      - host_path:container_path
    environment:
      - VAR1=value1
      - VAR2=value2
    networks:
      - mynetwork
    depends_on:
      - other_service
networks:
  mynetwork:
    driver: bridge
volumes:
  myvolume:
```

---

## 🧾 **Key Sections and Their Syntax**

---

### 🔹 `version`

Specifies the Compose file version. Common versions: `"3"`, `"3.8"` (recommended).

```yaml
version: "3.8"
```

---

### 🔹 `services`

Defines the container services to be run.

```yaml
services:
  web:
    image: nginx
```

---

### 🔹 `build`

Used when you want to build an image from a Dockerfile.

```yaml
build:
  context: .
  dockerfile: Dockerfile.dev
```

---

### 🔹 `image`

Use an existing image from Docker Hub or a custom-built image.

```yaml
image: mysql:5.7
```

---

### 🔹 `ports`

Maps container ports to the host.

```yaml
ports:
  - "8080:80"   # host:container
```

---

### 🔹 `volumes`

Mounts host paths or named volumes.

```yaml
volumes:
  - ./app:/usr/src/app
```

To declare named volumes:

```yaml
volumes:
  mydata:
```

---

### 🔹 `environment`

Sets environment variables inside containers.

```yaml
environment:
  - MYSQL_ROOT_PASSWORD=secret
  - MYSQL_DATABASE=exampledb
```

Or using object syntax:

```yaml
environment:
  MYSQL_ROOT_PASSWORD: secret
  MYSQL_DATABASE: exampledb
```

---

### 🔹 `depends_on`

Specifies service dependencies and startup order.

```yaml
depends_on:
  - db
```

**Note:** `depends_on` doesn’t wait for db to be ready—only for it to start. Use healthchecks for readiness.

---

### 🔹 `command`

Overrides the default command of the container.

```yaml
command: ["npm", "start"]
```

---

### 🔹 `restart`

Automatically restart containers under specific conditions.

```yaml
restart: always
# or: no | on-failure | unless-stopped
```

---

### 🔹 `networks`

Defines custom networks and connects services to them.

```yaml
networks:
  mynet:
    driver: bridge
```

Usage inside service:

```yaml
networks:
  - mynet
```

---

## 🔧 **Common Docker Compose Commands**

| Command                               | Description                            |
| ------------------------------------- | -------------------------------------- |
| `docker-compose up`                   | Starts services defined in the file    |
| `docker-compose up -d`                | Starts in detached mode                |
| `docker-compose down`                 | Stops and removes containers, networks |
| `docker-compose build`                | Builds images                          |
| `docker-compose stop`                 | Stops services                         |
| `docker-compose ps`                   | Shows running services                 |
| `docker-compose logs`                 | View logs                              |
| `docker-compose exec <service> <cmd>` | Run command in a running container     |

---

## 🧪 **Example 1: Nginx + PHP + MySQL Stack**

```yaml
version: "3.8"
services:
  web:
    image: nginx
    ports:
      - "80:80"
    volumes:
      - ./nginx.conf:/etc/nginx/nginx.conf
    depends_on:
      - php

  php:
    build: ./php
    volumes:
      - ./app:/var/www/html
    depends_on:
      - db

  db:
    image: mysql:5.7
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
      MYSQL_DATABASE: myapp

volumes:
  db_data:
```

---

## 🧪 **Example 2: Python Flask App + Redis**

### Folder Structure:

```
.
├── app.py
├── requirements.txt
└── docker-compose.yml
```

### `app.py`

```python
from flask import Flask
import redis

app = Flask(__name__)
r = redis.Redis(host='redis', port=6379)

@app.route('/')
def hello():
    r.incr('hits')
    return f"Hello! This page has been viewed {r.get('hits').decode()} times."
```

### `requirements.txt`

```
flask
redis
```

### `Dockerfile`

```dockerfile
FROM python:3.9
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["python", "app.py"]
```

### `docker-compose.yml`

```yaml
version: "3.8"
services:
  web:
    build: .
    ports:
      - "5000:5000"
    depends_on:
      - redis

  redis:
    image: redis:alpine
```

---

## 🛡️ **Tips & Best Practices**

* Use `.env` files for sensitive variables.
* Use `depends_on` + healthchecks to control service readiness.
* Use named volumes for persistent data.
* Keep services modular and well-defined.
* Separate development and production `docker-compose` files.

---

Would you like me to generate this into a **PDF/Markdown file** for download?

Also let me know if you want:

* Docker Compose + Kubernetes mapping.
* Advanced Compose features like **profiles**, **configs**, and **secrets**.
* **Real-world DevOps project** using Docker Compose.
