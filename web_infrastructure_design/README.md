# Web Infrastructure Design

![Nginx](https://img.shields.io/badge/Web%20Server-Nginx-009639.svg?logo=nginx&logoColor=white)
![HAProxy](https://img.shields.io/badge/Load%20Balancer-HAProxy-106DA9.svg?logo=haproxy&logoColor=white)
![MySQL](https://img.shields.io/badge/Database-MySQL-4479A1.svg?logo=mysql&logoColor=white)
![HTTPS](https://img.shields.io/badge/Security-HTTPS%20%2F%20SSL-721412.svg?logo=letsencrypt&logoColor=white)
![Holberton](https://img.shields.io/badge/School-Holberton-red.svg)

> Conception d'infrastructures web, du simple serveur unique à une architecture distribuée, sécurisée, monitorée et scalée — illustrée par des diagrammes (whiteboarding).

---

## Objectifs d'apprentissage

- Concevoir une infrastructure web sur **un seul serveur** (LAMP stack)
- Distribuer la charge sur plusieurs serveurs avec un **load balancer**
- Comprendre les algorithmes de répartition et les setups **Active-Active / Active-Passive**
- Mettre en place un cluster de base de données **Primary-Replica (Master-Slave)**
- **Sécuriser** (firewalls, SSL/HTTPS) et **monitorer** une infrastructure
- **Scaler** une infrastructure en séparant les composants sur des serveurs dédiés
- Identifier les points faibles : **SPOF**, sécurité, scalabilité, monitoring

---

## Stack technique

| Outil | Rôle |
|-------|------|
| ![Nginx](https://img.shields.io/badge/Nginx-009639?logo=nginx&logoColor=white) | Serveur web : reçoit les requêtes HTTP et sert le contenu |
| ![HAProxy](https://img.shields.io/badge/HAProxy-106DA9?logo=haproxy&logoColor=white) | Load balancer : répartit le trafic entre les serveurs |
| ![PHP-FPM](https://img.shields.io/badge/PHP--FPM-777BB4?logo=php&logoColor=white) | Application server : exécute le code de l'application |
| ![MySQL](https://img.shields.io/badge/MySQL-4479A1?logo=mysql&logoColor=white) | Base de données : stockage des données (cluster Primary-Replica) |
| ![SSL](https://img.shields.io/badge/SSL%2FHTTPS-721412?logo=letsencrypt&logoColor=white) | Chiffrement du trafic entre l'utilisateur et l'infrastructure |

---

## Tâches

### 0. Simple web stack
> **Objectif** : Concevoir une infrastructure web à un seul serveur (LAMP) hébergeant `www.foobar.com`.

Un serveur unique avec Nginx, un application server (PHP-FPM), le code base et MySQL.
Couvre : rôle du serveur, du domaine, du record DNS, du web/app server, de la base, TCP/IP, et les issues (SPOF, downtime, scalabilité).

📄 [`0-simple_web_stack.md`](./0-simple_web_stack.md)

### 1. Distributed web infrastructure
> **Objectif** : Distribuer le site sur trois serveurs avec un load balancer HAProxy.

Ajout d'un load balancer (Round Robin) et d'un cluster MySQL Primary-Replica.
Couvre : Active-Active vs Active-Passive, fonctionnement du cluster, et les issues (SPOF, sécurité, monitoring).

📄 [`1-distributed_web_infrastructure.md`](./1-distributed_web_infrastructure.md)

### 2. Secured and monitored web infrastructure
> **Objectif** : Sécuriser, chiffrer et monitorer l'infrastructure à trois serveurs.

Ajout de 3 firewalls, d'un certificat SSL (HTTPS) et de 3 clients de monitoring.
Couvre : rôle des firewalls, HTTPS, monitoring, collecte de données, QPS, et les issues (SSL au LB, write unique MySQL, composants identiques).

📄 [`2-secured_and_monitored_web_infrastructure.md`](./2-secured_and_monitored_web_infrastructure.md)

### 3. Scale up
> **Objectif** : Scaler l'infrastructure en séparant les composants sur des serveurs dédiés.

Ajout d'un serveur et d'un second load balancer HAProxy en cluster, avec web server, application server et base de données chacun sur son propre serveur.
Couvre : raison de chaque ajout, et différence application server vs web server.

📄 [`3-scale_up.md`](./3-scale_up.md)

---

## Auteur

- **Valentin Planchon**

---

<div align="center">

![Holberton School](https://img.shields.io/badge/HOLBERTON%20SCHOOL-Web%20Infrastructure%20Design-white?style=for-the-badge&labelColor=c41e3a&color=36393f) <img src="../assests/holberton_logo.png" alt="Holberton Logo" width="34">

[Retour au projet principal](../)

</div>
