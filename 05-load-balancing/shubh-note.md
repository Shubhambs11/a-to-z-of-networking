SYN → "Let’s establish connection"
ACK → "I received your request"

## AWS load balancers

### 1. ALB – Application Load Balancer (Layer 7)

- Works at Layer 7 (HTTP/HTTPS)
- Understands URLs, headers, cookies

✅ Features
Path-based routing (/api, /login)
Host-based routing (app.example.com)
Supports microservices & containers (ECS, Kubernetes)
WebSocket & HTTP/2 support

📌 Use case
Web apps, REST APIs, microservices


2. NLB – Network Load Balancer (Layer 4)

- Works at Layer 4 (TCP/UDP)
- Does not understand HTTP, only routes traffic

✅ Features
Ultra high performance & low latency
Handles millions of requests/sec
Supports static IP / Elastic IP
Good for real-time systems

📌 Use case
Gaming, IoT, real-time apps, financial systems

3. ELB (Classic Load Balancer – CLB)

- Old generation (supports Layer 4 + Layer 7)
- Limited features compared to ALB/NLB

⚠️ Status
Legacy → Not recommended for new apps

📌 Use case
Only for old/legacy systems
