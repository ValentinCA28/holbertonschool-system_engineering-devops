# 0. Simple web stack

![Simple Web Stack - One server infrastructure](../assests/Simple%20Web%20Stack%20-%20One%20server%20infrastructure.png)

## Description

A one server web infrastructure hosting the website `www.foobar.com`, built
on a LAMP-style stack (Linux + Nginx + MySQL + application code).

### Request flow

1. The user types `www.foobar.com` in the browser, which asks the **DNS** to
   resolve the name.
2. The DNS returns the server **IP `8.8.8.8`**.
3. The browser sends an **HTTP request over TCP/IP** to the web server (Nginx).
4. Nginx forwards the dynamic request to the **application server** (PHP-FPM).
5. The application server **queries the MySQL database** when data is needed.
6. The server sends the **HTTP response** back to the user.

## Specifics to explain

- **What is a server**: a physical or virtual machine that runs programs and
  serves resources (here, the website) to clients over a network.
- **Role of the domain name**: a human-readable name (`foobar.com`) that maps to
  the server IP, so users don't have to remember `8.8.8.8`.
- **Type of DNS record for `www`**: since `www.foobar.com` points directly to the
  server IP `8.8.8.8`, the `www` record is an **A record** (an A record maps a
  name to an IPv4 address). A CNAME could not be used here because a CNAME points
  to another domain name, never directly to an IP.
- **Role of the web server (Nginx)**: receives HTTP requests, serves static
  files, and forwards dynamic requests to the application server.
- **Role of the application server (PHP-FPM)**: executes the application code
  (the code base) to generate dynamic content.
- **Role of the database (MySQL)**: stores and retrieves the website's data.
- **Communication with the user's computer**: the server communicates using the
  **TCP/IP** protocol (HTTP over TCP/IP).

## Issues with this infrastructure

- **SPOF (Single Point Of Failure)**: there is only one server. If it goes down,
  the whole website is unreachable.
- **Downtime during maintenance**: deploying new code or updating the web server
  requires restarting it, making the site temporarily unavailable.
- **Cannot scale**: a single server cannot handle a large increase in incoming
  traffic.
