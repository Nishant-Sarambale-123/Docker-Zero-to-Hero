Here are **Docker troubleshooting commands** along with their **uses** to help you diagnose and resolve issues in Docker containers, images, volumes, and the daemon itself.

---

## 🔧 Docker Troubleshooting Commands with Uses

### 🔍 1. `docker ps`

* **Use**: Lists **running containers**.
* **Options**:

  * `docker ps -a` → Lists **all containers** (including stopped).
* **Example**:

  ```bash
  docker ps -a
  ```

---

### 🐳 2. `docker logs <container_id>`

* **Use**: Shows **logs** of a running or stopped container.
* **Example**:

  ```bash
  docker logs my_container
  ```

---

### 🔎 3. `docker inspect <container_or_image>`

* **Use**: Returns **detailed JSON output** about a container or image: network, volume mounts, environment variables, etc.
* **Example**:

  ```bash
  docker inspect my_container
  ```

---

### 📶 4. `docker exec -it <container_id> bash`

* **Use**: **Access a container shell** to run commands inside.
* **Alternative**: Use `sh` instead of `bash` if bash is not installed.
* **Example**:

  ```bash
  docker exec -it my_container bash
  ```

---

### 📡 5. `docker network inspect <network_name>`

* **Use**: View **network configuration** and connected containers.
* **Example**:

  ```bash
  docker network inspect bridge
  ```

---

### 🧹 6. `docker system df`

* **Use**: Shows **disk usage** by images, containers, and volumes.
* **Example**:

  ```bash
  docker system df
  ```

---

### 🚨 7. `docker events`

* **Use**: Stream **real-time Docker events**, useful for monitoring and debugging.
* **Example**:

  ```bash
  docker events
  ```

---

### 🛠️ 8. `docker info`

* **Use**: Shows **Docker daemon status**, number of containers/images, storage drivers, etc.
* **Example**:

  ```bash
  docker info
  ```

---

### 🧪 9. `docker run --rm -it alpine sh`

* **Use**: Runs a **test container** for quick troubleshooting with an Alpine image.
* **Example**:

  ```bash
  docker run --rm -it alpine sh
  ```

---

### 🧯 10. `docker-compose logs`

* **Use**: View **logs of services** defined in `docker-compose.yml`.
* **Example**:

  ```bash
  docker-compose logs
  ```

---

### ❌ 11. `docker container rm <id>` / `docker image rm <id>`

* **Use**: **Remove problematic containers/images**.
* **Options**:

  * Use `-f` to force remove.
* **Example**:

  ```bash
  docker container rm -f my_container
  ```

---

### 🔄 12. `docker restart <container_id>`

* **Use**: **Restart a container** that’s misbehaving or stuck.
* **Example**:

  ```bash
  docker restart my_container
  ```

---

### 🧹 13. `docker system prune`

* **Use**: Cleans up unused containers, images, volumes.
* **Warning**: Can delete valuable data.
* **Example**:

  ```bash
  docker system prune -a
  ```

---

### 🐞 14. `journalctl -u docker`

* **Use**: **Check Docker daemon logs** on Linux systems using `systemd`.
* **Example**:

  ```bash
  sudo journalctl -u docker
  ```

---

### 🔒 15. `docker volume inspect <volume_name>`

* **Use**: Troubleshoot **volume mount issues**.
* **Example**:

  ```bash
  docker volume inspect my_volume
  ```

---

## ✅ Bonus: Common Issues & Solutions

| Issue                      | Command                                                       | Action                       |
| -------------------------- | ------------------------------------------------------------- | ---------------------------- |
| Container won’t start      | `docker logs <container>`                                     | Check error logs             |
| Container keeps restarting | `docker inspect --format='{{.State.Restarting}}' <container>` | Find restart policy          |
| Port not exposed           | `docker ps` and `docker inspect`                              | Check published ports        |
| No space left              | `docker system df`, `docker system prune`                     | Clear space                  |
| Cannot exec into container | `docker inspect` → check status                               | Confirm container is running |

---

Would you like a **cheat sheet PDF** or **real-world troubleshooting examples** as well?
