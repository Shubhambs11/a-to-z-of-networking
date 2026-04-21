# Nginx as a Reverse Proxy

Nginx as a **Reverse Proxy** means it sits between clients (browsers/users) and your backend servers (like Node.js, Java, Python apps). Instead of users talking directly to your app, they talk to Nginx first.

---

## 🔁 What Nginx Reverse Proxy Provides

### 1. Load Balancing
Distributes incoming requests across multiple backend servers.

```
100 users → Nginx → splits to Server A, B, C
```

- Prevents overload on a single server

---

### 2. Improved Security
- Hides backend server details (IP, ports)
- Acts as a shield against attacks

> 👉 Users never directly access your application server

---

### 3. SSL/TLS Termination
- Handles HTTPS encryption/decryption
- Backend servers can run on HTTP (faster)

> 👉 Nginx manages certificates instead of your app

---

### 4. Caching
- Stores responses temporarily
- Reduces load on backend

> 👉 Faster response for repeated requests

---

### 5. Routing / Request Forwarding
Sends requests to different services based on URL.

```
/api     → backend server
/images  → static server
```

---

### 6. High Performance
- Handles thousands of connections efficiently
- Built on an **event-driven architecture**

---

### 7. Compression & Optimization
- Compresses responses using **Gzip**
- Reduces overall bandwidth usage

---

## 🧠 Simple Flow

```
Client → Nginx (Reverse Proxy) → Backend Server → Nginx → Client
```

---

## 🔧 Basic Example Config

```nginx
server {
    listen 80;

    location / {
        proxy_pass http://localhost:8080;
    }
}
```

> 👉 This forwards all traffic to your backend app running on port **8080**

---

## 🔧 Advanced Example Config (with SSL + Load Balancing)

```nginx
upstream backend_servers {
    server 192.168.1.10:8080;
    server 192.168.1.11:8080;
    server 192.168.1.12:8080;
}

server {
    listen 443 ssl;
    server_name yourdomain.com;

    ssl_certificate     /etc/nginx/ssl/cert.pem;
    ssl_certificate_key /etc/nginx/ssl/key.pem;

    location /api {
        proxy_pass http://backend_servers;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }

    location /images {
        root /var/www/static;
    }
}
```

---

## 📊 Quick Reference Table

| Feature              | Benefit                              |
|----------------------|--------------------------------------|
| Load Balancing       | Distributes traffic across servers   |
| Security             | Hides backend IPs and ports          |
| SSL/TLS Termination  | Centralized certificate management   |
| Caching              | Faster responses, less backend load  |
| Request Routing      | URL-based forwarding to services     |
| Compression (Gzip)   | Reduced bandwidth usage              |
| High Performance     | Handles thousands of concurrent connections |

---

## 🚀 In One Line

> **Nginx reverse proxy = performance + security + scalability layer in front of your backend**

---

## 📚 Further Reading

- [Nginx Official Docs](https://nginx.org/en/docs/)
- [Nginx Reverse Proxy Guide](https://docs.nginx.com/nginx/admin-guide/web-server/reverse-proxy/)
- [SSL/TLS Configuration](https://nginx.org/en/docs/http/configuring_https_servers.html)
