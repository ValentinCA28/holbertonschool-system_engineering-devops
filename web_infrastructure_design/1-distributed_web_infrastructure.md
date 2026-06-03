# 1. Distributed web infrastructure

![Distributed Web Infrastructure - Three Servers](../assests/Distributed%20web%20infra.png)

## Description

A three server web infrastructure hosting `www.foobar.com`, with a load
balancer (HAProxy) distributing traffic across two servers. Each server runs a
web server (Nginx), an application server (PHP-FPM), the code base, and a MySQL
database configured as a Primary-Replica cluster.

## Why each additional element is added

- **Load balancer (HAProxy)**: distributes incoming traffic across the two
  servers, so no single server is overloaded and the site stays available if one
  server is busy.
- **2nd server**: adds redundancy and capacity. Traffic can be served by either
  server, avoiding the single point of failure of the one-server setup.
- **Database Primary-Replica cluster**: replicates data across both database
  nodes, so reads can be spread out and a copy of the data always exists.

## Load balancer specifics

- **Distribution algorithm**: **Round Robin**. The load balancer forwards each
  new request to the next server in the list, one after another, cycling back to
  the first once the end is reached. This spreads requests evenly across servers.
- **Active-Active vs Active-Passive**: this setup is **Active-Active** — both
  servers receive and process traffic at the same time.
  - **Active-Active**: all nodes are running and handling requests
    simultaneously.
  - **Active-Passive**: only one node (active) handles traffic, while the other
    (passive) stays on standby and takes over only if the active node fails.

## Database Primary-Replica (Master-Slave) cluster

- The **Primary** node accepts **write** operations and replicates every change
  to the Replica node.
- The **Replica** node receives a copy of the data and is used for **read**
  operations only.
- **Difference in regard to the application**: the application sends all
  **writes (and reads) to the Primary** node, while it can send **reads to the
  Replica** node. The Replica never receives writes directly from the
  application — it only gets its data from the Primary through replication.

## Issues with this infrastructure

- **SPOF (Single Point Of Failure)**: the **load balancer** is alone — if it
  goes down, the whole site becomes unreachable.
- **Security issues**: there is **no firewall** and **no HTTPS**, so traffic is
  not protected or encrypted.
- **No monitoring**: there is no tool to track the health, traffic, or
  performance of the infrastructure.
