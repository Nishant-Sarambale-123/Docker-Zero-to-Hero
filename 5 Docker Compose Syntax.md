Here's the **complete syntax template for a `docker-compose.yml` file**, covering all key elements you might use when defining multi-container applications.

---

## 📄 **Docker Compose Syntax (Full Reference)**

```yaml
version: "3.8"  # Compose file format version

services:
  <service_name>:
    image: <image_name>  # OR
    build:
      context: .                  # Directory of Dockerfile
      dockerfile: Dockerfile      # Optional
      args:
        key: value

    container_name: <custom_name>
    
    command: <override_default_command>
    entrypoint: <override_entrypoint>
    
    ports:
      - "<host_port>:<container_port>"

    environment:
      - VAR1=value
      - VAR2=value
    env_file:
      - .env

    volumes:
      - ./host_path:/container_path
      - named_volume:/container_path

    depends_on:
      - <other_service>

    restart: "no" | always | on-failure | unless-stopped

    networks:
      - <network_name>

    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost"]
      interval: 30s
      timeout: 10s
      retries: 3

    logging:
      driver: "json-file"
      options:
        max-size: "10m"
        max-file: "3"

volumes:
  named_volume:

networks:
  <network_name>:
    driver: bridge
```

---

## ✅ Example: Node.js App + MongoDB

```yaml
version: "3.8"

services:
  app:
    build:
      context: .
      dockerfile: Dockerfile
    ports:
      - "3000:3000"
    environment:
      - MONGO_URL=mongodb://mongo:27017/mydb
    depends_on:
      - mongo

  mongo:
    image: mongo:6
    ports:
      - "27017:27017"
    volumes:
      - mongo_data:/data/db

volumes:
  mongo_data:
```

---

## 📌 Common Compose Commands

| Command                | Description                          |
| ---------------------- | ------------------------------------ |
| `docker-compose up`    | Start all services                   |
| `docker-compose up -d` | Start in background (detached)       |
| `docker-compose down`  | Stop and remove containers, networks |
| `docker-compose build` | Build images                         |
| `docker-compose logs`  | Show logs                            |
| `docker-compose ps`    | List running services                |

---

Let me know if you want a **language-specific compose file** (e.g., for Python + Redis, Java + PostgreSQL, etc.).
