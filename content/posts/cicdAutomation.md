---
date: 2025-01-13
description: "Tier to get my feet wet with the devops world by using Jenkins and setting up CI/CD pipeline"
image: "/images/cicd/cicd.png"
lastmod: 2025-01-16
showTableOfContents: True
tags: ["DevOps", "Automation", "CI/CD", "Java", "Web Application", "Deployment"]
title: "Automating Java Web Application Deployment with CI/CD using GitHub and Jenkins"
type: "post"
---

At this stage, I don't have much experience with DevOps. My previous experience mainly involves using Docker to host multiple servers and setting up VPNs to play LAN games with my friends. Recently, I decided to dive deeper into DevOps by automating the deployment of a simple web application.

I designed a basic layout for an online library web application. Then, I created a development branch in GitHub and configured two `application.properties` files for different environments—one for development and one for production. After that, I pushed the code to GitHub and set up a local Jenkins instance on my machine to automate the deployment process. I deployed two instances of the web application, each corresponding to one of the branches.

For more detailed information, check out my [DevOps Beginner Project](/content/projects/devops-begning.md).
