# One-Server Web Infrastructure – `www.foobar.com`

## Overview
This document describes a simple **one-server web infrastructure** setup hosting the website **www.foobar.com**.  
The infrastructure uses a **LAMP-like stack** (Linux, Nginx, MySQL, and application code) and is designed for basic hosting with minimal components.

---

##  Infrastructure Components

### 1. Server
- **Definition**: A physical or virtual machine that stores, processes, and delivers data to clients over a network.
- **In this setup**: Hosts the web server, application server, and database.

### 2. Domain Name
- **Role**: Translates a human-friendly name (**foobar.com**) into the server's IP address.
- **Example**: `www.foobar.com` → **8.8.8.8**

### 3. DNS Record
- **Type**: The `www` in `www.foobar.com` is typically an **A record** (maps domain name to IP) or a **CNAME record** (maps domain name to another domain).
- **Role**: Ensures that when users type the URL, the request is directed to the correct server.

### 4. Web Server (Nginx)
- **Role**: Handles HTTP requests, serves static files (HTML, CSS, JS), and forwards dynamic requests to the application server.

### 5. Application Server
- **Role**: Runs the application logic (e.g., PHP, Python, or Node.js) and processes dynamic content requests.

### 6. Application Files (Code Base)
- **Role**: Contains the website’s source code, templates, scripts, and business logic.

### 7. Database (MySQL)
- **Role**: Stores and retrieves structured data (e.g., user accounts, blog posts, transactions).

---

## Communication
- The **server** communicates with the user’s browser using the **HTTP protocol** over the internet.

---

## Limitations & Issues

1. **SPOF (Single Point of Failure)**
   - If the server goes down, the entire site becomes unavailable.

2. **Downtime During Maintenance**
   - Deploying new code or restarting the web server causes temporary outages.

3. **Scalability Limitations**
   - A single server cannot handle large traffic spikes effectively; performance degrades under heavy load.

---

##  Summary
While simple and cost-effective, this setup is vulnerable to downtime, scaling issues, and lacks redundancy.  
It’s suitable for small, low-traffic projects but requires upgrades for production-grade reliability.
