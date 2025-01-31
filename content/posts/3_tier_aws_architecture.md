---
date: 2025-01-21
description: "This blog chronicles my journey as I work on deploying a Java application using AWS's 3-Tier Architecture. It includes daily progress updates, challenges faced, and solutions implemented throughout the project. The goal is to create a scalable and secure architecture, utilizing AWS EC2 instances, RDS, and Elastic Load Balancers to manage different layers of the application."
image: "/images/AWS_3-Tier_Architecture/thumbnail.png"
lastmod: 2025-01-31
showTableOfContents: True
tags: ["AWS", "Java", "3-Tier Architecture", "EC2", "RDS", "Elastic Load Balancer", "Deployment", "Cloud Computing"]
title: "Deploying a Java Application on AWS 3-Tier Architecture"
type: "post"
---

# Introduction
In today's cloud-native ecosystem, deploying applications to the cloud is a common practice for ensuring scalability, security, and high availability. Amazon Web Services (AWS) offers a wide range of services that allow developers to deploy applications efficiently. One of the most popular architectural patterns used in cloud-based applications is the 3-tier architecture. In this blog post, I’ll walk you through the process of deploying a Java application on AWS using a 3-tier architecture setup.

# What is a 3-Tier Architecture?
A 3-tier architecture is a software design pattern that divides an application into three distinct layers:

- Presentation Tier (Frontend): The user interface (UI) where users interact with the application.
- Application Tier (Business Logic): The core of the application that processes user inputs, makes business decisions, and manages the application's logic.
- Data Tier (Database): The database layer that stores and retrieves data for the application.

The 3-tier architecture provides flexibility, maintainability, and scalability by isolating each component, allowing developers to focus on specific tasks and scale individual components as needed.
![AWS 3-Tier Architecture](/images/AWS_3-Tier_Architecture/diagram.png)

# Why Use AWS for 3-Tier Architecture?

AWS provides a robust cloud platform with a wide range of tools that are perfect for deploying a 3-tier architecture. Some of the key advantages of using AWS include:

- Scalability: AWS can automatically scale your resources based on traffic, ensuring that your application can handle increased loads efficiently.
- High Availability: AWS provides services like Elastic Load Balancing (ELB), Amazon RDS, and Auto Scaling to ensure your application remains available even under heavy traffic.
- Security: With AWS Identity and Access Management (IAM), AWS Shield, and other security features, you can secure your application and data at every layer.

---

## Progress 22jan2025:

### Prerequisites

- All the prerequisites are done:
  - Made an AWS Free Tier account
  - Created a repository with a Java application to store user login details
  - SonarQube account created
  - JFrog Cloud account created

### Pre-deployment

- Done creating a global AMI
- Installed AWS CLI, CloudWatch, and AWS SSM on that instance
- Done creating Golden AMIs for each separate tier (Nginx, Tomcat, Maven)

### Currently working on

- Learning about VPCs and deploying the VPCs

## Challenges faced:
Today, I faced an issue while trying to install Java on Amazon Linux 2023. Initially, I attempted to install Java using the usual commands, but I kept running into errors. After some troubleshooting, I realized that Amazon Linux 2023 doesn't support the typical java-11-openjdk installation.

Instead, I found that Amazon Corretto 21 is the recommended version. The correct command to install it is:
```bash
sudo dnf install java-11-amazon-corretto
```
After installing Java this way, everything worked as expected, and I was able to continue with my setup.

This was the only major problem that I face today

## Progress Update – 26th Jan 2025

I’m making some real progress with learning cloud architecture. It was a pretty complicated mess until yesterday, but now things are starting to click. I'm currently working on replicating: ![aws-3tier-achicture](/images/AWS_3-Tier_Architecture/aws-3-tier-architecture.png)and although there’s a lot to absorb, I’m starting to understand the key concepts bit by bit.

### Here’s where I’m at with the architecture:

- **VPC (Virtual Private Cloud):**  
  I’ve got a solid understanding of what a VPC is and how it fits into the larger AWS environment. It's essentially your private network in the cloud.

- **Availability Zones and Subnets:**
  I’ve learned how AWS divides regions into availability zones and how subnets are used within those zones to organize and secure network traffic.

- **NAT Gateways:**  
  Setting up NAT Gateways has been a key part of my learning. They allow instances in private subnets to access the internet without exposing them directly to the public.

- **Load Balancers:**  
  I’ve also gotten familiar with Load Balancers, which are crucial for distributing traffic across multiple EC2 instances to ensure high availability.

Right now, I’ve created the private subnets and laid down the foundation of the network, but I still need to dive into the following to complete the architecture:

- **Security Groups:**  
  These will help secure my instances and manage network traffic between them.

- **Auto Scaling:**  
  I need to learn how auto-scaling groups will help manage the scaling of my application based on demand.

- **Bastion Host:**  
  A bastion host will be important for securely accessing instances in the private subnets.

- **Transit Gateway:**  
  This will be essential for managing network traffic between VPCs and connecting to on-premise networks.

---

### CI Pipeline

Alongside this, I’ve also been learning about Continuous Integration (CI) pipelines. I plan to implement a CI pipeline with **Bitbucket**, **SonarQube**, and **JFrog Artifactory** to manage my build and deployment process. This is how I envision the workflow:

1. **Bitbucket** for version control and code repository.
2. **SonarQube** for static code analysis and ensuring code quality.
3. **JFrog Artifactory** to store and manage build artifacts (like JARs or WARs).
4. Finally, deploy those artifacts to an **EC2 instance** running my application.

Once I have everything set up and deployed, I’ll document the process in a detailed step-by-step guide to explain each part and how everything fits together. It’s all coming together, and I’m excited to put everything into action.

# Progress Update – 31st Jan 2025

Unfortunately, I’ve had to pause the project for now. I was very close to completing the AWS 3-Tier Architecture setup, with only a couple of tasks remaining: setting up the Nginx server and configuring the CI pipeline. However, while working through the deployment, I made a manual NAT gateway setup, as I realized that using AWS’s managed NAT Gateway service would incur additional costs. Unfortunately, I was completely unaware that simply setting up a VPC (Virtual Private Cloud) would also lead to unexpected charges.

This was a surprise, and given that I’m still learning, I need to take a step back and reassess my approach. The architecture was almost fully done—I had already set up VPCs, subnets, load balancers, and learned a lot about AWS services. The only tasks left were to implement the Nginx server to manage traffic and set up the CI pipeline for automating builds and deployments.

Although this setback has been disappointing, it’s also been a valuable learning experience. I’ve gained a deeper understanding of cloud infrastructure and how different AWS services interact. I plan to revisit the project in the future once I’m more familiar with cost management and can fully navigate the challenges involved.