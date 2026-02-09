# AWS Load Balancers  – ALB vs NLB vs Classic ELB



##  What Is Elastic Load Balancing (ELB)?

Elastic Load Balancing is an AWS managed service that:
- Distributes incoming traffic across multiple targets
- Improves availability and fault tolerance
- Automatically scales with demand
- Performs health checks and traffic redirection

Targets can include:
- EC2 instances
- ECS tasks
- EKS pods
- Lambda functions

---

##  Types of AWS Load Balancers

| Load Balancer | Status | Primary Use |
|--------------|-------|-------------|
| Application Load Balancer (ALB) | Active | HTTP/HTTPS applications |
| Network Load Balancer (NLB) | Active | High‑performance TCP/UDP |
| Classic Load Balancer (ELB) | Legacy | Older EC2 workloads |

---

## 1️⃣ Application Load Balancer (ALB)

### OSI Layer
- **Layer 7 – Application Layer**

### How ALB Works (Request Flow)
Client → Listener (80/443) → Routing Rules → Target Group → Backend Target

### Routing Capabilities
- Path‑based routing (`/api`, `/login`)
- Host‑based routing (`api.example.com`)
- Header‑based routing
- Query string routing

### Target Groups
Supports:
- EC2 instances
- ECS tasks
- EKS pods (IP mode)
- Lambda functions

Each target group has:
- Independent health checks
- Custom routing rules

### Security Features
- AWS WAF integration
- SSL/TLS termination
- Security Groups
- Authentication (Cognito / OIDC)

### Advantages
- Intelligent routing
- Best for microservices
- Deep container integration
- Detailed request visibility

### Limitations
- HTTP/HTTPS only
- Slightly higher latency than NLB

### Common Use Cases
- REST APIs
- Web applications
- Microservices
- Kubernetes ingress

---

## 2️⃣ Network Load Balancer (NLB)

### OSI Layer
- **Layer 4 – Transport Layer**

### How NLB Works
Client → Static IP → Listener (TCP/UDP) → Target Group → Backend Target

### Key Capabilities
- Static IPv4/IPv6 addresses
- Preserves client source IP
- Millions of requests per second
- TCP, UDP, TLS support

### Performance
- Ultra‑low latency
- Handles sudden traffic spikes
- Ideal for real‑time systems

### Security Model
- No WAF support
- Security Groups applied to targets
- TLS pass‑through or termination

### Advantages
- Extremely fast
- Non‑HTTP protocol support
- Massive scalability

### Limitations
- No content‑based routing
- No HTTP inspection

### Common Use Cases
- Gaming servers
- VoIP systems
- IoT ingestion
- Databases behind TCP
- Financial trading systems

---

## 3️⃣ Classic Load Balancer (ELB – Legacy)

### OSI Layers
- Layer 4 (TCP)
- Limited Layer 7 (HTTP)

### Characteristics
- Older AWS load balancer
- Minimal routing logic
- No container‑native support

### Why It’s Deprecated
- No WAF
- No advanced routing
- Poor ECS/EKS integration
- Limited scalability features

 **Not recommended for new applications**

---

## 🧠 Layer 4 vs Layer 7 Comparison

| Feature | Layer 4 | Layer 7 |
|------|------|------|
| Routing Basis | IP & Port | HTTP Content |
| Visibility | Low | High |
| Speed | Very High | High |
| Example | NLB | ALB |
| Use Case | Performance | Intelligence |

---

##  Comparison Table

| Feature | ALB | NLB | Classic ELB |
|------|----|----|----|
| OSI Layer | 7 | 4 | 4 & 7 |
| Protocols | HTTP/HTTPS | TCP/UDP/TLS | HTTP, HTTPS, TCP |
| Static IP | No | Yes | No |
| Source IP | No | Yes | No |
| WAF Support | Yes | No | No |
| Container Support | Excellent | Partial | Poor |
| Latency | Low | Ultra‑Low | Moderate |
| Recommended | ✅ | ✅ | ❌ |

---

##  Architecture Design Recommendations

### Use ALB When:
- Application‑level routing is needed
- Running microservices or containers
- Security filtering via WAF is required

### Use NLB When:
- Ultra‑low latency is critical
- Non‑HTTP protocols are required
- Static IPs are mandatory

### Avoid Classic ELB When:
- Designing modern cloud architectures
- Working with ECS/EKS

---



##  Final Takeaway
AWS Load Balancers are **purpose‑built**, not interchangeable.

Choose:
- **ALB for intelligence**
- **NLB for speed**
- **Avoid Classic ELB for new workloads**

---

