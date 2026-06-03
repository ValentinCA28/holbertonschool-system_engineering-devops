# 2. Secured and monitored web infrastructure

![Secured and Monitored Web Infrastructure](../assests/Secured%20and%20Monitored%20Web%20Infrastructure.png)

## Description

The same three server infrastructure hosting `www.foobar.com`, now **secured**
(3 firewalls), serving **encrypted traffic** (SSL certificate / HTTPS), and
**monitored** (3 monitoring clients reporting to a monitoring platform).

## Why each additional element is added

- **3 firewalls**: one in front of the load balancer and one in front of each
  server, to control and filter network traffic and protect each part of the
  infrastructure from unauthorized access.
- **SSL certificate (HTTPS)**: to encrypt the traffic between the user and the
  infrastructure, so data exchanged with `www.foobar.com` cannot be read or
  tampered with.
- **3 monitoring clients**: one on each server (and the load balancer) to collect
  data and send it to a monitoring platform (e.g. Sumologic), so we can track the
  health and activity of the infrastructure.

## Specifics to explain

- **What firewalls are for**: a firewall is a security system that monitors and
  filters incoming and outgoing network traffic based on defined rules, blocking
  unwanted or malicious connections.
- **Why traffic is served over HTTPS**: HTTPS encrypts the traffic (via the SSL
  certificate), protecting users' data in transit from eavesdropping and
  man-in-the-middle attacks.
- **What monitoring is used for**: to observe the infrastructure — track uptime,
  performance, errors, and resource usage — so issues can be detected and fixed,
  ideally before they impact users.
- **How the monitoring tool collects data**: a **monitoring client (agent)** is
  installed on each server. It collects metrics and logs locally and sends them
  to the monitoring platform.
- **How to monitor the web server QPS** (Queries Per Second): configure the
  monitoring agent to read the web server's access logs (or expose Nginx
  metrics), count the number of requests per second, and send that metric to the
  monitoring platform where it can be visualized and alerted on.

## Issues with this infrastructure

- **Terminating SSL at the load balancer level**: traffic is decrypted at the
  load balancer, so between the load balancer and the servers the traffic travels
  **unencrypted** (clear text) inside the infrastructure, which is a security
  concern.
- **Only one MySQL server accepting writes**: the **Primary** node is the only
  one that can accept writes. If it goes down, the application can no longer write
  data — it is a single point of failure for writes.
- **Servers with all the same components**: every server runs the database, the
  web server, and the application server together. This makes them hard to scale
  independently and means a problem with one component affects the whole server.
