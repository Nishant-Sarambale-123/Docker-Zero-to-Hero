## 🐳 `docker exec` — Detailed Explanation (Production + Interview)

![Image](https://lh5.googleusercontent.com/5Ac3cKvZLWwOwW5lL1djkY6Nvsbe8K5A-lt4t4awtSH-9_DLzGJpd-AYuTwKEIjOneQWdmYupzcyVfutv-9EZWsPyv6w5hehkGBy5R7skxeOV7KFpgv3rI4s4bmLduhP8XSGFpxvZyXmC6q3IkxVBg?utm_source=chatgpt.com)

![Image](https://i.sstatic.net/VpHql.png?utm_source=chatgpt.com)

![Image](https://www.docker.com/app/uploads/2021/11/docker-containerized-appliction-blue-border_2.png?utm_source=chatgpt.com)

---

## 🔹 What is `docker exec`?

`docker exec` **runs a NEW command or process inside an already running container** without disturbing the main application.

```bash
docker exec [OPTIONS] <container> <command>
```

✔ Safest way to debug containers
✔ Preferred in production
✔ Does NOT affect the main process (PID 1)

---

## 🔹 Why `docker exec` is IMPORTANT

* Opens a **new shell**
* Runs **temporary troubleshooting commands**
* Container continues running normally
* No risk of accidental container stop

---

## 🔹 Basic Usage

### ▶ Run a command inside container

```bash
docker exec mycontainer ls
```

---

### ▶ Interactive shell (MOST USED)

```bash
docker exec -it mycontainer /bin/bash
docker exec -it mycontainer /bin/sh
```

📌 Use `/bin/sh` for alpine images

---

## 🔹 Important Options (MUST KNOW)

| Option | Meaning           | Example              |
| ------ | ----------------- | -------------------- |
| `-i`   | Interactive       | stdin open           |
| `-t`   | Allocate tty      | terminal             |
| `-u`   | User              | run as specific user |
| `-e`   | Env variable      | pass env             |
| `-w`   | Working directory | change path          |

---

### ▶ Run as root

```bash
docker exec -it -u root mycontainer bash
```

---

### ▶ Set environment variable

```bash
docker exec -it -e ENV=prod mycontainer bash
```

---

### ▶ Change working directory

```bash
docker exec -it -w /app mycontainer bash
```

---

## 🔹 Real Production Use Cases

### ✅ 1️⃣ Debug application

```bash
docker exec -it app_container bash
ps aux
netstat -tulnp
env
```

---

### ✅ 2️⃣ Check logs inside container

```bash
docker exec app_container cat /var/log/app.log
```

---

### ✅ 3️⃣ Database troubleshooting

```bash
docker exec -it mysql_container mysql -u root -p
```

---

### ✅ 4️⃣ Network debugging

```bash
docker exec -it app_container ping google.com
docker exec -it app_container curl localhost:8080
```

---

### ✅ 5️⃣ File operations

```bash
docker exec app_container touch test.txt
docker exec app_container vi config.yml
```

---

## 🔹 How `docker exec` Works (Concept)

* Container already has **PID 1** running
* `docker exec` creates a **new process**
* This process shares:

  * Same namespaces
  * Same filesystem
  * Same network

📌 Once you exit shell → exec process ends, container continues.

---

## 🔹 `docker exec` vs `docker attach` (INTERVIEW FAVORITE)

| Feature             | docker exec | docker attach            |
| ------------------- | ----------- | ------------------------ |
| Creates new process | ✅ Yes       | ❌ No                     |
| Opens shell         | ✅ Yes       | ❌ Only if PID 1 is shell |
| Safe in production  | ✅ Yes       | ❌ Risky                  |
| Can stop container  | ❌ No        | ✅ Yes                    |
| Debugging           | Best        | Limited                  |

---

## 🔹 Common Errors & Fixes

### ❌ Error: Container not running

```text
Error: Container is not running
```

**Fix**

```bash
docker start <container>
```

---

### ❌ Error: `/bin/bash not found`

**Cause**

* Alpine image

**Fix**

```bash
docker exec -it container sh
```

---

### ❌ Permission denied

**Fix**

```bash
docker exec -it -u root container bash
```

---

## 🔹 Interview Questions & Answers

### ❓ What happens when you exit `docker exec` shell?

**Answer**

> Only the exec process exits. Container keeps running.

---

### ❓ Can `docker exec` restart container?

**Answer**

> No. It does not affect PID 1.

---

### ❓ Why is `docker exec` safer than attach?

**Answer**

> Because it creates a separate process and does not send signals to the main process.

---

## 🔹 Best Practices (VERY IMPORTANT)

✔ Use `exec` instead of `attach`
✔ Use `-it` for interactive shells
✔ Avoid installing tools inside prod containers
✔ Use exec for **temporary debugging only**

---

## 🔑 Key Takeaways

* `docker exec` = **production-safe debugging**
* Always prefer `/bin/sh` for alpine
* Exiting exec does NOT stop container
* Interview favorite topic 🚀

---

If you want next 👇
✅ `docker logs` deep dive
✅ Docker PID 1 & signal handling
✅ Exec vs Kubernetes `kubectl exec`

Just tell me 👍
