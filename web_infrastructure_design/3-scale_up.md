# 3. Scale up

![Scale Up](../assests/Scale%20up.png)

## Description

The infrastructure is scaled up by **splitting each component onto its own
dedicated server** (web server, application server, database) and by adding a
**second load balancer** clustered with the first one.

## Why each additional element is added

- **Additional server**: lets us split the components so each one runs on its own
  dedicated server, instead of stacking web server, application server, and
  database on the same machine.
- **Second load balancer (HAProxy) in a cluster**: the two HAProxy nodes are
  configured as a **cluster (sync)** so that if one load balancer fails, the
  other takes over. This removes the load balancer single point of failure.
- **Dedicated web server (Nginx)**: handling HTTP requests and serving content on
  its own server lets it be scaled and tuned independently.
- **Dedicated application server (PHP-FPM)**: running the application code on its
  own server isolates the compute workload and lets it be scaled independently.
- **Dedicated database server (MySQL)**: putting the database on its own server
  gives it dedicated resources (CPU, RAM, disk) and lets it be scaled and secured
  on its own.

## Application server vs Web server

- The **web server (Nginx)** handles **HTTP requests**: it serves static files
  and forwards dynamic requests. It deals with the web/HTTP layer.
- The **application server (PHP-FPM)** **executes the application code** (the code
  base) to generate dynamic content, and talks to the database.

In short: the web server delivers content over HTTP, while the application server
runs the business logic that produces that content.
