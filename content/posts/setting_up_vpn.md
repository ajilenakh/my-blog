---
date: 2025-01-28
# description: ""
# image: ""
lastmod: 2025-01-28
showTableOfContents: false
# tags: ["",]
title: "Setting Up a VPN on a Bastion Host with WireGuard"
type: "post"
---
# Why?

While building my 3-tier AWS architecture, I encountered a challenge related to accessing resources within my private VPC. Here's the setup:

I have two VPCs:

- Public VPC: This houses my Bastion host, which acts as the secure entry point to my network.
- Private VPC: This VPC is completely isolated, containing my Nginx servers, application servers, and databases—no public access at all. There’s only a single load balancer that routes traffic to the Nginx servers, and a NAT instance for internet access (still working on this, as I want to avoid the higher cost of a NAT gateway).

The problem is that, in the future, if I need to access services like Bitbucket, SonarQube, or any internal resources in the private VPC, I wouldn’t be able to do so easily. Since my private VPC resources don’t have public IPs and are completely isolated, direct access to them from my local machine or external network isn’t possible.

That’s when the idea clicked: **Why not turn my Bastion host into a VPN gateway?** This would allow me to securely access my private VPC from anywhere without exposing any resources directly to the public internet. Using a VPN, I can route my traffic through the Bastion host and access all my private resources—like Bitbucket and SonarQube—safely and securely.

# How to turn your ec2 instance into a vpn server?
