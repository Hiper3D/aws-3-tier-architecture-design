# ☁️ Highly Available 3-Tier Web Architecture on AWS

![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-web-services&logoColor=white)
![Amazon EC2](https://img.shields.io/badge/Amazon%20EC2-FF9900?style=for-the-badge&logo=Amazon%20EC2&logoColor=white)
![Amazon RDS](https://img.shields.io/badge/Amazon%20RDS-527FFF?style=for-the-badge&logo=Amazon%20RDS&logoColor=white)
![Amazon VPC](https://img.shields.io/badge/Amazon%20VPC-8C4FFF?style=for-the-badge&logo=Amazon%20VPC&logoColor=white)

## 📌 Executive Overview
This repository documents the structural design of a secure, highly available, and fault-tolerant three-tier web application architecture provisioned on AWS (Amazon Web Services - a comprehensive cloud computing platform). Architected to fulfill the rigorous hands-on requirements of the AWS Cloud Support Associate professional certificate, this project demonstrates enterprise-grade cloud networking capabilities. 

The core objective is to showcase best practices in traffic distribution, network isolation, and database redundancy by strategically decoupling resources across public and private subnets within a custom VPC (Virtual Private Cloud - a secure, isolated private cloud hosted within a public cloud).

## 🏗️ Architecture Topology
*(Please reference `AWSDiagram.drawio.svg` in the repository files for the visual network topology).*

## ⚙️ Core Infrastructure Components

### 1. Network Foundation
* **Amazon VPC:** Engineered a custom VPC (Virtual Private Cloud - a secure, isolated private cloud hosted within a public cloud) spanning two distinct AZs (Availability Zones - isolated locations within data center regions from which public cloud services originate and operate) to guarantee high availability and robust fault tolerance.

### 2. Presentation Tier (Public Web)
* **Traffic Management:** Deployed an ALB (Application Load Balancer - a load balancing service for web applications operating at the application layer) within the public subnets to act as the single, secure ingress point. It receives external client requests via an IGW (Internet Gateway - a horizontally scaled, redundant, and highly available VPC component that allows communication between your VPC and the internet) and intelligently distributes the payload evenly across healthy compute instances.

### 3. Logic Tier (Private Compute)
* **Secure Compute:** Provisioned Amazon EC2 (Elastic Compute Cloud - a web service that provides secure, resizable compute capacity in the cloud) application servers within deeply isolated private subnets. This strict segregation ensures the application layer cannot be targeted directly from the public internet, drastically reducing the external attack surface.

### 4. Data Tier (Private Database)
* **High-Availability Storage:** Configured a Multi-AZ Amazon RDS (Relational Database Service - a distributed relational database service) MySQL deployment situated in dedicated, backend database subnets. The architecture features a Primary instance handling active queries and a Standby instance leveraging synchronous replication for seamless, automatic failover.

## 🚦 End-to-End Traffic Lifecycle

* **Ingress (Client to Backend):** When a client initiates a data query, the traffic enters the VPC (Virtual Private Cloud - a secure, isolated private cloud hosted within a public cloud) through the IGW (Internet Gateway - a horizontally scaled, redundant, and highly available VPC component that allows communication between your VPC and the internet) and is securely routed to the ALB (Application Load Balancer - a load balancing service for web applications operating at the application layer). The ALB evaluates the health of the logic layer and forwards the payload to an available EC2 (Elastic Compute Cloud - a web service that provides secure, resizable compute capacity in the cloud) instance. The instance processes the application logic and securely queries the primary data tier.
* **Egress (Database to Client):** Upon successful query execution, the Primary RDS (Relational Database Service - a distributed relational database service) instance returns the localized data to the originating EC2 instance. The server formats this into a web response and passes it back to the load balancer. Finally, the ELB (Elastic Load Balancing - automatically distributes incoming application traffic across multiple targets) routes the finalized response out through the internet gateway back to the user.

## 💡 Core Engineering Competencies
* **Cloud Infrastructure Design:** Architecting scalable, decoupled enterprise environments.
* **Network Security & Isolation:** Strategic implementation of public vs. private subnets.
* **Disaster Recovery:** Ensuring high availability via Multi-AZ deployments and synchronous replication.
* **Traffic Optimization:** Advanced load balancing and secure gateway routing.
