DevOps Project Report: Automated CI/CD Pipeline for a 2-Tier Flask Application on AWS
Author: Prashant Gohel Date: August 23, 2025

Table of Contents
Project Overview
Architecture Diagram
Step 1: AWS EC2 Instance Preparation
Step 2: Install Dependencies on EC2
Step 3: Jenkins Installation and Setup
Step 4: GitHub Repository Configuration
Dockerfile
docker-compose.yml
Jenkinsfile
Step 5: Jenkins Pipeline Creation and Execution
Conclusion
Infrastructure Diagram
Work flow Diagram
1. Project Overview
This document outlines the step-by-step process for deploying a 2-tier web application (Flask + MySQL) on an AWS EC2 instance. The deployment is containerized using Docker and Docker Compose. A full CI/CD pipeline is established using Jenkins to automate the build and deployment process whenever new code is pushed to a GitHub repository.

2. Architecture Diagram
+-----------------+      +----------------------+      +-----------------------------+
|   Developer     |----->|     GitHub Repo      |----->|        Jenkins Server       |
| (pushes code)   |      | (Source Code Mgmt)   |      |  (on AWS EC2)               |
+-----------------+      +----------------------+      |                             |
                                                       | 1. Clones Repo              |
                                                       | 2. Builds Docker Image      |
                                                       | 3. Runs Docker Compose      |
                                                       +--------------+--------------+
                                                                      |
                                                                      | Deploys
                                                                      v
                                                       +-----------------------------+
                                                       |      Application Server     |
                                                       |      (Same AWS EC2)         |
                                                       |                             |
                                                       | +-------------------------+ |
                                                       | | Docker Container: Flask | |
                                                       | +-------------------------+ |
                                                       |              |              |
                                                       |              v              |
                                                       | +-------------------------+ |
                                                       | | Docker Container: MySQL | |
                                                       | +-------------------------+ |
                                                       +-----------------------------+
3. Step 1: AWS EC2 Instance Preparation
Launch EC2 Instance:
Navigate to the AWS EC2 console.
Launch a new instance using the Ubuntu 22.04 LTS AMI.
Select the t2.micro instance type for free-tier eligibility.
Create and assign a new key pair for SSH access.
