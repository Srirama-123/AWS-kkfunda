# AWS Application Load Balancer (ALB) - Detailed Explanation

## 1. What is an Application Load Balancer (ALB)?
An **Application Load Balancer (ALB)** is an AWS Elastic Load Balancer (ELB) that operates at **Layer 7 (Application Layer)** of the **OSI model**. It intelligently distributes incoming **HTTP/HTTPS traffic** to multiple backend servers based on content, such as URL paths, hostnames, HTTP headers, and request methods.

---

## 2. Why Use an ALB?
- **Improves high availability**: Automatically distributes traffic to healthy instances.
- **Enhances security**: Supports **AWS Web Application Firewall (WAF)**.
- **Enables routing decisions**: Routes requests based on **URL paths, hostnames, HTTP headers, query parameters, and request methods**.
- **Supports microservices and containers**: Works well with **Amazon ECS, EKS, and Fargate**.
- **Load balancing across multiple Availability Zones**.

---

## 3. Key Features of ALB
### A. Content-Based Routing (Path-Based & Host-Based Routing)
- **Path-Based Routing**: Routes traffic based on the URL path.
  - Example:
    - `example.com/api` → Backend API instances.
    - `example.com/images` → Image processing instances.

- **Host-Based Routing**: Routes traffic based on domain names.
  - Example:
    - `app.example.com` → Application servers.
    - `blog.example.com` → Blog servers.

### B. HTTP/HTTPS Support & SSL Termination
- ALB supports **HTTP and HTTPS** for secure connections.
- **SSL Termination** (offloads SSL decryption at the ALB level instead of backend instances).

### C. WebSocket Support
- ALB supports **WebSockets**, allowing real-time two-way communication (useful for chat applications, gaming, and real-time stock trading).

### D. Health Checks
- ALB continuously checks the health of backend instances.
- If an instance becomes unhealthy, ALB stops sending traffic to it.

### E. Sticky Sessions (Session Persistence)
- Ensures that users continue to interact with the same backend server for the duration of a session.
- Useful for applications that require user-specific data (e.g., shopping carts).

### F. Auto Scaling Integration
- Works with **Auto Scaling Groups** to dynamically add or remove backend instances based on traffic.

### G. Support for AWS Lambda
- ALB can route traffic to **AWS Lambda functions**, enabling serverless application deployment.

---

## 4. ALB Architecture
An ALB consists of the following components:

### A. Listeners
- A **listener** is a process that checks for connection requests on a configured **port** and **protocol** (e.g., HTTP 80, HTTPS 443).
- Rules can be defined on listeners to forward traffic based on conditions.

### B. Target Groups
- A **target group** defines a set of **EC2 instances, containers (ECS), Lambda functions, or IP addresses** where ALB directs traffic.
- Each target group has a **health check** to ensure traffic is sent to only healthy targets.

### C. Rules
- ALB supports **listener rules** that define conditions and target groups for routing traffic.
- Example Rule:
  - IF request URL **contains** `/api` → Forward to API target group.
  - IF request URL **contains** `/images` → Forward to Image Processing target group.

### D. Availability Zones
- ALB can distribute traffic across **multiple Availability Zones**, ensuring high availability.

---

## 5. How ALB Works?
1. **User sends an HTTP/HTTPS request** to the ALB’s DNS name.
2. The **ALB listener** receives the request.
3. The listener **evaluates listener rules**.
4. ALB **routes the request** to the appropriate target group based on the rules.
5. If a backend instance **fails health checks**, ALB **removes it** from rotation.
6. ALB maintains **session stickiness (if enabled)**.
7. The backend server processes the request and **sends the response** back to the user.

---

## 6. Use Cases of ALB
| Use Case | Example |
|----------|---------|
| **Web applications** | Load balancing across multiple web servers. |
| **Microservices architecture** | Routing traffic to different microservices based on URL paths. |
| **Containerized applications** | Load balancing across ECS or Kubernetes services. |
| **Serverless applications** | Directing HTTP requests to AWS Lambda functions. |
| **Multi-domain websites** | Using ALB for routing different subdomains. |

---

## 7. Hands-on: How to Create an ALB in AWS

### Step 1: Create an ALB
1. Open **AWS Management Console** → Go to **EC2**.
2. Click on **Load Balancers** → Click **Create Load Balancer**.
3. Select **Application Load Balancer**.
4. Enter:
   - **Name**: `my-alb`
   - **Scheme**: Choose `Internet-facing` or `Internal`.
   - **Listeners**: Choose `HTTP` or `HTTPS`.
   - **Availability Zones**: Select two or more.

### Step 2: Create a Target Group
1. Go to **Target Groups** → Click **Create Target Group**.
2. Select **Instances** or **IP addresses**.
3. Define:
   - **Protocol**: `HTTP`
   - **Port**: `80`
   - **Health Check Path**: `/index.html`
4. Register your EC2 instances.

### Step 3: Configure Listener Rules
1. Under the ALB settings, **edit listeners**.
2. Add rules for **path-based or host-based routing**.

### Step 4: Test ALB
- Copy the **ALB DNS Name** from AWS.
- Open it in a browser to verify that traffic is routing correctly.

---

## 8. ALB Pricing
- **Charged per hour** (based on ALB type and usage).
- **Charged per LCU (Load Balancer Capacity Unit)**, which includes:
  - Number of **new connections per second**.
  - Number of **active connections**.
  - Processed **requests**.
  - Processed **data**.

---

## 9. ALB vs. NLB vs. CLB
| Feature | ALB (Layer 7) | NLB (Layer 4) | CLB (Legacy) |
|---------|--------------|--------------|--------------|
| **Best for** | Web apps & APIs | High-speed TCP/UDP traffic | Legacy applications |
| **Routing** | Path-based, Host-based | TCP, Static IPs | Basic |
| **Latency** | Higher | Very low | Medium |
| **WebSockets** | ✅ Yes | ❌ No | ❌ No |
| **SSL Termination** | ✅ Yes | ❌ No | ✅ Yes |

---

## 10. Pros & Cons of ALB
✅ **Pros:**
- Advanced **routing features** (path-based, host-based, query parameters).
- **Works with AWS Lambda**, ECS, and EKS.
- Integrated **security** (AWS WAF, SSL termination).
- **Scalable and fault-tolerant**.

❌ **Cons:**
- Higher **latency** compared to NLB.
- More **expensive** than CLB.
- Doesn’t support **TCP/UDP-based applications** (use NLB for that).

---

## Conclusion
An **Application Load Balancer (ALB)** is a powerful, feature-rich load balancer designed for **modern web applications, microservices, and containerized workloads**. It provides **intelligent routing, security, and seamless scaling**, making it the best choice for **HTTP/HTTPS traffic**.
