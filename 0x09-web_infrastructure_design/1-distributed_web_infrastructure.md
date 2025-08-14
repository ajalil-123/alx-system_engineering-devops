    # Three-Server Web Infrastructure for www.foobar.com
    
    ## Overview
    This infrastructure design consists of:
    
    - **2 Application Servers** (Nginx + Application Server on each)
    - **1 Load Balancer** (HAProxy)
    - **1 Database Server** (MySQL Primary)
    - **1 Database Replica** (MySQL Replica)
    - **Domain Name:** `www.foobar.com` → Load Balancer IP
    
    ---
    
    ## Why Each Component is Added
    
    ### 1. Load Balancer (HAProxy)
    - Distributes incoming traffic between multiple application servers.
    - Improves availability and scalability.
    - Prevents a single application server from becoming overloaded.
    
    ### 2. Second Application Server
    - Ensures service continuity if one application server fails.
    - Allows handling more concurrent traffic.
    
    ### 3. Database Replica
    - Offloads read operations from the Primary DB.
    - Improves read performance.
    - Provides redundancy in case the Primary fails.
    
    ---
    
    ## Load Balancer Configuration
    
    - **Distribution Algorithm:** **Round Robin**
      - Each new request is sent to the next server in order.
      - Example:
        - Request 1 → Server A
        - Request 2 → Server B
        - Request 3 → Server A
      - Simple and ensures equal load distribution.
    
    ---
    
    ## Active-Active vs Active-Passive Setup
    
    - **Our Setup:** **Active-Active** for the application servers.
      - Both servers handle traffic simultaneously.
    
    - **Difference:**
      - **Active-Active:** All servers work at the same time, sharing the load.
      - **Active-Passive:** One server is active, the other is on standby and only takes over if the active one fails.
    
    ---
    
    ## Database Primary-Replica (Master-Slave) Cluster
    
    ### How It Works
    - The **Primary** handles **all write operations** (`INSERT`, `UPDATE`, `DELETE`).
    - Changes are replicated to the **Replica** in near real-time.
    - The **Replica** handles **read-only queries** (`SELECT`) to reduce load on the Primary.
    
    ### Application Usage
    - **Primary Node:** Read + Write operations.
    - **Replica Node:** Read-only operations.
    
    ---
    
    ## Issues in This Infrastructure
    
    ### 1. SPOF (Single Point of Failure)
    - The Load Balancer is a SPOF. If it fails, the site is unreachable.
    - The Primary database is also a SPOF for writes.
    
    ### 2. Security Issues
    - No firewall means all ports are open, increasing attack risk.
    - No HTTPS means data can be intercepted during transmission.
    
    ### 3. No Monitoring
    - Without monitoring tools, failures or performance degradation might go unnoticed until users complain.
    
    ---
    
    ## Suggested Improvements
    - Add a **second load balancer** for high availability.
    - Implement **firewall rules** to restrict access.
    - Enable **HTTPS** to secure data transmission.
- Use **monitoring tools** like Prometheus, Grafana, or ELK Stack.