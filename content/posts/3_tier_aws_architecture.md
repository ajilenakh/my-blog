---
date: 2025-01-21
description: "This blog chronicles my journey as I work on deploying a Java application using AWS's 3-Tier Architecture. It includes daily progress updates, challenges faced, and solutions implemented throughout the project. The goal is to create a scalable and secure architecture, utilizing AWS EC2 instances, RDS, and Elastic Load Balancers to manage different layers of the application."
image: "/images/AWS_3-Tier_Architecture/thumbnail.png"
lastmod: 2025-01-22
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