## MyApp-Ansible ##

## Overview
MyApp-Ansible is a sample Java web application project demonstrating a full CI/CD pipeline using Jenkins, Docker, and Ansible for deployment to Tomcat.

This project shows how to:
- Build a Java web application (.war) using Maven.
- Dockerize the application and push the image to a registry.
- Deploy the Dockerized application to target servers using Ansible.
- Optionally, deploy the .war directly to a system Tomcat installation.
- This repo is structured to showcase DevOps best practices, infrastructure as code, and automation skills, making it ideal for portfolio purposes.

## Repo Structure
myapp-ansible/
├── app/
│ ├── src/ # Java source code (Hello World web app)
│ ├── Dockerfile # Docker image definition for the app
│ └── pom.xml # Maven build file
├── roles/
│ ├── docker-host/ # Role to install Docker on target servers
│ └── tomcat/ # Role to install and configure system Tomcat
├── inventories/
│ └── production # Inventory of production servers
├── playbooks/
│ ├── provision.yml # Provision servers with Docker/Tomcat
│ └── deploy-docker.yml # Deploy app Docker container to servers
├── ansible.cfg # Ansible configuration file
└── README.md

----

## Features
- Jenkins Integration: Build and package Java application automatically.
- Docker: Containerize the application with Tomcat pre-installed.
- Ansible: Automate server provisioning and deployment of Docker containers or WAR files.
- Tomcat Deployment: Option to deploy either Dockerized Tomcat or system Tomcat.
- Idempotent Infrastructure: Re-running playbooks ensures consistent environments.

## SETUP
1. Provision Target Servers : ansible-playbook playbooks/provision.yml --private-key ~/.ssh/id_rsa
2. Build the Application: 
cd app
mvn clean package

3. Docker Build & Push
docker build -t registry.example.com/myapp:latest .
docker push registry.example.com/myapp:latest

4. Deploy via Ansible
ansible-playbook playbooks/deploy-docker.yml \
  --private-key ~/.ssh/id_rsa \
  -e "image=registry.example.com/myapp:latest"

 Optional: Use deploy-war.yml if deploying .war directly to a system Tomcat. 

5. Access the App
- Docker deployment: http://<server_ip>:8080/myapp/
- WAR deployment: http://<server_ip>:8080/myapp/

------
## Folder Details:
- app/src/ — Minimal Java web app with a HelloWorld servlet.
- roles/docker-host — Installs Docker on servers.
- roles/tomcat — Installs and configures Tomcat (if not using Docker).
- inventories/production — Lists your target servers and variables.
- playbooks/provision.yml — Sets up servers with necessary packages.
- playbooks/deploy-docker.yml — Pulls Docker image and runs the app container.
- ansible.cfg — Configures Ansible defaults.

Just so you all know: 
This project is designed as a portfolio demonstration. In production, consider:
- Using versioned tags for Docker images.
- Implementing blue/green deployments or rolling updates.
- Securing credentials via Jenkins or Ansible Vault.
- Adding monitoring and logging.

----
## Author
- Kimberly Nnamadim, DevOps & CX Enthusiast 
GitHub: [[github.com/knnamadim](https://github.com/knnamadim)]
