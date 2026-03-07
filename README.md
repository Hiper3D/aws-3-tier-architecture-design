# aws-3-tier-architecture-design
Highly Available 3-Tier Web Architecture on AWS ☁️

📌 Project Overview:
This project visualizes a secure, highly available, and fault-tolerant three-tier web application architecture on Amazon Web Services (AWS). It was designed as part of the hands-on architectural requirements for the AWS Cloud Support Associate professional certificate on Coursera.

The goal of this design is to demonstrate best practices in cloud networking, traffic distribution, and database redundancy by isolating resources across public and private subnets within a Virtual Private Cloud (VPC).

🏗️ Architecture Diagram:
(Upload your diagram image to your GitHub repo, then replace the link below with the actual image path)

⚙️ Core AWS Components:
Networking (Amazon VPC): A custom VPC spanning two Availability Zones (AZ A and AZ B) to ensure high availability and fault tolerance.

Public Web Tier: (Application Load Balancer): An ALB deployed in the public subnets acts as the single entry point. It receives incoming client traffic via an Internet Gateway (IGW) and distributes it evenly across healthy compute instances.

Private Compute Tier: (Amazon EC2): Application servers reside in isolated private subnets, ensuring they cannot be accessed directly from the public internet, thereby enhancing security.

Private Database Tier: (Amazon RDS): A Multi-AZ MySQL deployment situated in dedicated database subnets. It features a Primary instance for active queries and a Standby instance utilizing synchronous replication for automatic failover.

🚦 Traffic Flow:
Client to Backend:
When a client initiates a request from the internet to query data, the traffic enters the VPC through the Internet Gateway and is routed to the Application Load Balancer. The ALB evaluates the health of the compute layer and forwards the request to an available EC2 instance located securely in a private subnet. The EC2 instance processes the application logic and securely queries the Primary Amazon RDS database.

Database to Client:
After the Primary RDS database successfully processes the query, it returns the requested data back to the originating EC2 instance. The EC2 instance formats this data into a web response and sends it back to the ALB. The ELB then routes the final response out through the Internet Gateway and back over the internet to the client.

💡 Key Skills Demonstrated:
Cloud Infrastructure Design

Network Security & Isolation (Public vs. Private Subnets)

High Availability & Disaster Recovery (Multi-AZ Deployments)

Traffic Load Balancing
