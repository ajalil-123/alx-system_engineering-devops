# Secured and Monitored Three-Server Web Infrastructure for www.foobar.com

## Overview
This infrastructure hosts `www.foobar.com` on **three servers**:
- **1 Load Balancer** (HAProxy) – Handles SSL termination and traffic distribution.
- **2 Application Servers** – Run the web server and application.
- **1 Database Server** – MySQL Primary for read/write operations.

It is designed to be **secured, serve encrypted traffic (HTTPS)**, and be **monitored** for performance and availability.

---

## Security Measures

### 1. Firewalls (3 Total)
- **Purpose:** Restrict access to only necessary ports/services.
- **Setup:**
  - **Firewall 1:** Protects the Load Balancer – Only allows HTTP(S) traffic from the public.
  - **Firewall 2:** Protects Application Servers – Only allows connections from the Load Balancer.
  - **Firewall 3:** Protects the Database Server – Only allows connections from Application Servers.
- **Why Added:** Prevents unauthorized access and limits attack surface.

### 2. SSL Certificate
- **Purpose:** Encrypts all data exchanged between clients and the server.
- **Why HTTPS:** 
  - Protects user data from interception or tampering.
  - Improves trust with users and search engine ranking.
- **Placement:** Installed at the Load Balancer to enable HTTPS for `www.foobar.com`.

---

## Monitoring Setup

### 1. Monitoring Clients (3 Total)
- Installed on each server (Load Balancer + 2 App Servers).
- **Purpose:** Collect system metrics (CPU, RAM, disk usage), application logs, and web traffic data.

### 2. Data Collection
- Monitoring agents forward logs and metrics to a centralized monitoring service (e.g., Sumo Logic, Datadog, or Prometheus).
- Enables real-time alerting, historical analysis, and performance tracking.

### 3. Monitoring Web Server QPS (Queries Per Second)
- Use the monitoring tool to track the **rate of incoming HTTP requests**.
- Configure a custom metric or dashboard to measure QPS and trigger alerts if it exceeds thresholds.

---

## Infrastructure Issues

### 1. SSL Termination at Load Balancer
- **Problem:** Traffic between the Load Balancer and Application Servers is unencrypted.
- **Risk:** Internal network traffic could be intercepted if the internal network is compromised.
- **Mitigation:** Use **end-to-end SSL** so traffic remains encrypted from client → load balancer → application server.

### 2. Single MySQL Write Node
- **Problem:** If the Primary database fails, no write operations can be performed.
- **Mitigation:** Implement database clustering or failover mechanisms (e.g., MySQL Group Replication, Galera Cluster).

### 3. All Servers Have Same Components (Database + Web + App)
- **Problem:** 
  - Increases the attack surface (a breach compromises all services).
  - Makes scaling difficult (you can’t scale database independently from the application).
- **Mitigation:** Use a **tiered architecture** where each server type is dedicated to a single role.

---

## Conclusion
This design ensures the infrastructure is **secure, encrypted, and monitored**, but still has potential bottlenecks and security considerations that can be addressed through:
- End-to-end encryption.
- Redundant database writes.
- Role separation across servers.

