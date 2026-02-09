#  Introduction to AWS Services

##  AWS Services 

---

### 🔹 Amazon EC2 (Elastic Compute Cloud)

**Purpose:**  
Amazon EC2 provides **virtual servers (instances)** in the cloud to run applications.

**How it works:**

* Users choose an instance type (CPU, RAM, storage)
* Select an operating system (Linux/Windows)
* Launch instances inside a VPC
* Scale instances up/down based on demand

**Key Features:**

* Full control over OS and software
* Auto Scaling support
* Pay only for what you use

**Use Cases:**

* Web servers and application servers
* Backend APIs
* Development and testing environments

###  Security Best Practices
- Use **IAM roles** instead of access keys
- Restrict access using **Security Groups (least privilege)**
- Disable password login; use **SSH key-based access**
- Keep OS patched and updated
- Use **EBS encryption**
- Place instances in **private subnets** where possible
- Enable **CloudWatch + GuardDuty monitoring**

---

### 🔹 Amazon ECS (Elastic Container Service)

**Purpose:**  
ECS is a **container orchestration service** that runs Docker containers.

**How it works:**

* Containers are defined using task definitions
* Runs on EC2 or AWS Fargate
* Automatically manages container scheduling and scaling

**Key Features:**

* Deep AWS integration
* No need to manage container orchestration manually
* Supports microservices architecture

**Use Cases:**

* Containerized web applications
* CI/CD pipelines
* Microservices deployment

###  Security Best Practices
- Use **IAM task roles** (never hardcode credentials)
- Scan container images for vulnerabilities
- Run containers as **non-root users**
- Use **private ECR repositories**
- Apply **security groups per task (awsvpc mode)**
- Enable logging to CloudWatch

---

### 🔹 Amazon EKS (Elastic Kubernetes Service)

**Purpose:**  
EKS is a **managed Kubernetes service** that runs Kubernetes control plane on AWS.

**How it works:**

* AWS manages the Kubernetes master nodes
* Worker nodes run on EC2 or Fargate
* Integrates with IAM, VPC, and Load Balancers

**Key Features:**

* Highly scalable
* Kubernetes standard (cloud-agnostic)
* Automatic updates and patching

**Use Cases:**

* Large-scale container orchestration
* Multi-cloud Kubernetes environments
* Enterprise-grade microservices

###  Security Best Practices
- Use **IAM Roles for Service Accounts (IRSA)**
- Restrict Kubernetes API access
- Apply **Network Policies**
- Use **Pod Security Standards**
- Regularly patch worker nodes
- Enable **audit logs**
- Use **Secrets Manager** instead of plain secrets
---

### 🔹 Amazon VPC (Virtual Private Cloud)

**Purpose:**  
VPC provides a **logically isolated private network** inside AWS.

**How it works:**

* Define IP address ranges
* Create public and private subnets
* Configure route tables and gateways

**Key Features:**

* Network isolation
* Custom routing
* Secure communication

**Use Cases:**

* Hosting secure applications
* Hybrid cloud connectivity
* Network segmentation

###  Security Best Practices
- Use **private subnets** for backend resources
- Minimize use of public IPs
- Implement **NACL + Security Groups**
- Enable **VPC Flow Logs**
- Use **NAT Gateway** for outbound internet access
- Segment environments (prod, dev, test)

---

### 🔹 Security Groups

**Purpose:**  
Security Groups act as **virtual firewalls** for EC2 instances.

**How it works:**

* Allow inbound and outbound traffic using rules
* Rules are based on IP, protocol, and port
* Stateful firewall (responses are automatically allowed)

**Use Cases:**

* Restrict server access
* Protect application ports
* Enforce least-access networking

###  Security Best Practices
- Follow **least privilege**
- Avoid `0.0.0.0/0` unless required
- Separate security groups by role (web, app, DB)
- Regularly audit unused rules
- Never expose admin ports publicly (SSH, RDP)
---

### 🔹 Amazon Route 53

**Purpose:**  
Route 53 is a **scalable DNS (Domain Name System)** service.

**How it works:**

* Converts domain names to IP addresses
* Supports routing policies (simple, weighted, latency-based)
* Performs health checks

**Use Cases:**

* Domain management
* Traffic routing
* Failover and disaster recovery

###  Security Best Practices
- Enable **DNSSEC**
- Use **health checks** for failover
- Restrict access using IAM policies
- Monitor DNS changes via CloudTrail

---

### 🔹 Elastic Load Balancing (ELB)

**Purpose:**  
Distributes incoming traffic across multiple targets.

**Types:**

* Application Load Balancer (ALB)
* Network Load Balancer (NLB)

**Key Features:**

* High availability
* Health checks
* Fault tolerance

**Use Cases:**

* Web applications
* Microservices traffic distribution

###  Security Best Practices
- Use **HTTPS only**
- Terminate TLS at ALB
- Integrate **AWS WAF**
- Restrict backend access to load balancer only
- Enable access logs
---

### 🔹 Amazon S3 (Simple Storage Service)

**Purpose:**  
S3 is an **object storage service** for storing files and data.

**Key Features:**

* Extremely high durability (99.999999999%)
* Scalable and cost-effective
* Supports encryption and versioning

**Use Cases:**

* Static website hosting
* Log storage
* Backup and archival

###  Security Best Practices
- Block **public access** by default
- Enable **bucket encryption**
- Use **IAM policies over ACLs**
- Enable **versioning**
- Enable **server access logging**
- Monitor with GuardDuty (S3 protection)
---

### 🔹 AWS WAF (Web Application Firewall)

**Purpose:**  
Protects web applications from common attacks.

**How it works:**

* Filters HTTP/HTTPS requests
* Blocks SQL Injection, XSS, bots

**Use Cases:**

* Web security
* Compliance requirements
* SOC monitoring

###  Security Best Practices
- Enable **managed rule sets**
- Customize rules per application
- Use rate-limiting
- Monitor logs continuously
- Integrate with ALB or CloudFront
---

### 🔹 Amazon Athena

**Purpose:**  
Athena is a **serverless SQL query service**.

**How it works:**

* Queries data directly from S3
* No servers to manage
* Pay per query

**Use Cases:**

* Log analysis
* Security investigations
* Data analytics

###  Security Best Practices
- Restrict S3 access via IAM
- Encrypt query results
- Enable audit logging
- Use workgroups for access control
---

### 🔹 AWS IAM (Identity and Access Management)

**Purpose:**  
Controls **who can access AWS resources**.

**Key Concepts:**

* Users, Groups, Roles
* Policies (permissions)
* Least privilege principle

**Use Cases:**

* Secure access control
* Role-based access
* Compliance and auditing

###  Security Best Practices
- Enable **MFA for all users**
- Avoid root account usage
- Use **roles instead of long-term keys**
- Rotate credentials regularly
- Monitor with IAM Access Analyzer
- Apply least privilege always
---

### 🔹 AWS Lambda

**Purpose:**  
Serverless compute service that runs code without servers.

**How it works:**

* Triggered by events (S3 upload, API call, logs)
* Automatically scales
* Pay only for execution time

**Use Cases:**

* Automation
* Event-driven processing
* Security alert handling

###  Security Best Practices
- Use **least-privilege IAM roles**
- Limit function timeout and memory
- Never hardcode secrets
- Use **environment variable encryption**
- Enable logging and monitoring
---

##  Service Integration Overview

A typical AWS cloud architecture works as follows:

1. **Route 53** routes user traffic
2. **AWS WAF** filters malicious requests
3. **Load Balancer** distributes traffic
4. **EC2 / ECS / EKS** handle application logic
5. **IAM** controls permissions securely
6. **S3** stores static files and logs
7. **Athena** analyzes logs from S3
8. **Lambda** automates workflows and responses

---

##  Learning Outcomes

After completing this study, you will be able to:

* Explain AWS services clearly in exams and interviews
* Design basic AWS architectures
* Understand cloud security fundamentals
* Build a strong base for cloud and cybersecurity careers

---

##  Notes

This README and report are intended for **educational purposes** and **beginner-to-intermediate AWS learning**.