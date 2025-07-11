# Amazon Prime Video Kubernetes Project 🎬

This repository contains the infrastructure as code (IaC) and CI/CD pipeline definitions for deploying and managing an application mimicking a service like Amazon Prime Video, leveraging AWS cloud infrastructure and automation tools. This project is a **forked repository**, where I've customized and enhanced the original codebase to fit specific deployment and monitoring requirements. While the project name suggests Kubernetes for the application, this repository specifically focuses on the foundational EC2-based monitoring server and the automated deployment processes.

---

## 🚀 Project Overview

This project automates the provisioning of core AWS infrastructure components using Terraform and orchestrates their deployment via a Jenkins CI/CD pipeline. The goal is to establish a robust and repeatable process for deploying cloud resources, with a specific focus on setting up a monitoring server that would support a larger application environment.

---

## 💡 Technologies Used

* **Cloud Provider:** Amazon Web Services (AWS) ☁️
    * EC2 (Elastic Compute Cloud)
    * Security Groups
    * IAM (Identity and Access Management)
* **Infrastructure as Code (IaC):** Terraform (v1.12.2) ⚙️
    * Manages AWS resource provisioning (EC2 instances, Security Groups).
* **CI/CD (Continuous Integration/Continuous Delivery):** Jenkins 🔄
    * Automates the entire deployment workflow from code commit to infrastructure provisioning.
    * Manages sensitive AWS credentials securely.
* **Version Control:** Git & GitHub 🐙
    * **Forked, customized, and managed source code** on GitHub, ensuring automated pipeline triggers upon code changes.

---

## 🏗️ Project Structure

The repository is organized to separate infrastructure definitions, CI/CD pipeline code, and other project assets:


To reflect that you forked the code, you can add a sentence or adjust the existing "Version Control Integration" point in the README.md file.

Here's how you can modify the "Project Overview" and "Version Control Integration" sections:

Markdown

# Amazon Prime Video Kubernetes Project 🎬

This repository contains the infrastructure as code (IaC) and CI/CD pipeline definitions for deploying and managing an application mimicking a service like Amazon Prime Video, leveraging AWS cloud infrastructure and automation tools. This project is a **forked repository**, where I've customized and enhanced the original codebase to fit specific deployment and monitoring requirements. While the project name suggests Kubernetes for the application, this repository specifically focuses on the foundational EC2-based monitoring server and the automated deployment processes.

---

## 🚀 Project Overview

This project automates the provisioning of core AWS infrastructure components using Terraform and orchestrates their deployment via a Jenkins CI/CD pipeline. The goal is to establish a robust and repeatable process for deploying cloud resources, with a specific focus on setting up a monitoring server that would support a larger application environment.

---

## 💡 Technologies Used

* **Cloud Provider:** Amazon Web Services (AWS) ☁️
    * EC2 (Elastic Compute Cloud)
    * Security Groups
    * IAM (Identity and Access Management)
* **Infrastructure as Code (IaC):** Terraform (v1.12.2) ⚙️
    * Manages AWS resource provisioning (EC2 instances, Security Groups).
* **CI/CD (Continuous Integration/Continuous Delivery):** Jenkins 🔄
    * Automates the entire deployment workflow from code commit to infrastructure provisioning.
    * Manages sensitive AWS credentials securely.
* **Version Control:** Git & GitHub 🐙
    * **Forked, customized, and managed source code** on GitHub (`https://github.com/mrinalini7788/amazon-prime-video-kubernetes.git`), ensuring automated pipeline triggers upon code changes.

---

## 🏗️ Project Structure

The repository is organized to separate infrastructure definitions, CI/CD pipeline code, and other project assets:

.
├── .git/                                # Git version control
├── App In kubernetes - Monitoring Project Document.pdf
├── Dockerfile                           # (Potentially for the application or Jenkins agent)
├── Jenkinsfile                          # Main Jenkins Pipeline definition
├── Jenkinsfile2-eks                     # (Alternative/EKS-specific Jenkinsfile)
├── Progress notes.txt
├── README.md                            # This file
├── kubernetes/                          # (Likely contains Kubernetes manifests for the application)
├── monitoring/                          # (Potentially monitoring-related configurations)
├── package-lock.json
├── package.json
├── progressnote
├── public/
├── scripts/
├── src/
└── terraform/                           # Contains Terraform configuration files
├── main.tf                          # Main resource definitions (e.g., EC2, Security Group)
├── variables.tf                     # Input variables for Terraform (e.g., instance_name, key_name)
├── output.tf                        # Output values from Terraform (e.g., public IP of instance)



## 🛠️ Setup & Deployment

### Prerequisites

* An AWS Account with programmatic access keys (Access Key ID and Secret Access Key).
* A running Jenkins server (e.g., accessible at `http://13.235.33.124:8080/`).
* Jenkins configured with AWS credentials (stored securely using Jenkins' Credentials Manager).
* Terraform (v1.12.2 or compatible) installed on the Jenkins agent.
* An EC2 Key Pair in your AWS account (e.g., named `primevideo`) for SSH access to deployed instances.

### Deployment Steps (via Jenkins)

1.  **Clone this Repository:** Ensure your Jenkins pipeline is configured to clone this GitHub repository (`https://github.com/mrinalini7788/amazon-prime-video-kubernetes.git`).
2.  **Configure Jenkins Credentials:**
    * In Jenkins, navigate to "Manage Jenkins" -> "Manage Credentials".
    * Add your AWS Access Key ID and Secret Access Key as a "Secret text" or "AWS Credentials" type. Ensure the ID matches what's referenced in the `Jenkinsfile` (e.g., `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY`).
3.  **Jenkinsfile Configuration:** The `Jenkinsfile` is configured to:
    * Checkout the `main` branch of this repository.
    * Run `terraform init`, `validate`, `plan`, and `apply` (or `destroy` based on a parameter).
    * Pass Terraform variables such as `key_name` (`primevideo`) and `instance_name` (`Monitoring_server`) via Jenkins environment variables.
4.  **Trigger the Pipeline:** Run the Jenkins pipeline job (e.g., `monitoringserver`) configured for this repository. You can select `apply` or `destroy` as a build parameter.

### Terraform Variables

The `terraform/variables.tf` defines key inputs:

* `instance_name`: The name tag for the EC2 instance (e.g., "Monitoring\_server").
* `key_name`: The name of the AWS EC2 Key Pair to associate with the instance (e.g., "primevideo").
    *(Note: `access_key` and `secret_key` variables in `variables.tf` are generally superseded by environment variables set in Jenkins for provider authentication and can often be removed or marked `sensitive` if explicitly needed for other modules.)*

---

## Troubleshooting & Learnings
•
DevSecOps Principles: Learned to integrate security tools and practices throughout the software development lifecycle, ensuring a "shift left" approach to security.
•
Project Management with Jira: Understood how Jira is used as a project management tool to assign tasks and track progress for application development.
•
Version Control with GitHub: Utilized GitHub as a distributed version control system for managing application source code.
•
Continuous Integration/Continuous Deployment (CI/CD) with Jenkins:
◦
Jenkins as a CI/CD Tool: Set up and configured Jenkins to automate the build, test, and deployment processes.
◦
Pipeline Creation: Created and managed three types of Jenkins pipelines: one for Continuous Integration (CI), one for Continuous Deployment (CD), and another for infrastructure setup (monitoring server).
◦
Declarative Pipelines: Gained experience in writing declarative Jenkins pipelines using Groovy language.
◦
Jenkins Architecture: Understood Jenkins Master-Slave (now Master-Node/Agent) concepts to handle increased workload and distribute builds.
◦
Plugin Management: Installed and utilized various Jenkins plugins (e.g., SonarQube Scanner, NodeJS, Docker, Kubernetes, Pipeline Stage View, Blue Ocean, Prometheus, Eclipse Temurin Installer, Extended Email Notification) to extend Jenkins' functionality.
◦
Credential Management: Configured and managed sensitive credentials (e.g., SonarQube token, Docker Hub credentials, AWS access keys, Gmail app password) securely within Jenkins' credential vault.
◦
Webhooks: Understood the use of webhooks for triggering Jenkins pipelines automatically upon code pushes to GitHub.
◦
Build Parameterization: Implemented parameterized builds in Jenkins to allow flexible execution of pipelines (e.g., apply or destroy for infrastructure).
◦
Troubleshooting Pipelines: Developed skills in identifying and resolving errors in Jenkins pipeline executions.
•
Static Application Security Testing (SAST) with SonarQube:
◦
Integrated SonarQube Community Edition into the CI pipeline to scan source code for vulnerabilities, hotspots, bugs, and code smells.
◦
Learned to configure SonarQube with Jenkins using authentication tokens and webhooks for quality gate checks.
◦
Understood how SonarQube reports are used to identify and prioritize code quality issues for developers.
•
Vulnerability Scanning with Aqua Trivy:
◦
Used Aqua Trivy Community Version to scan the application's file system for sensitive information (like API keys, access keys) and identify outdated packages or vulnerabilities.
◦
Also used Trivy to scan Docker images for vulnerabilities.
•
Containerization with Docker:
◦
Dockerfile Creation: Wrote Dockerfiles to define the application's environment and build Docker images.
◦
Image Management: Built Docker images, tagged them, and pushed them to Docker Hub for artifact storage.
◦
Container Deployment: Deployed the application as Docker containers for local testing.
◦
Understood Docker commands for managing images and containers (docker ps, docker images).
•
Cloud Computing with Amazon Web Services (AWS):
◦
EC2 Instances: Created and managed EC2 virtual machines (Ubuntu LTS) to host Jenkins, SonarQube, and monitoring tools.
◦
Security Groups: Configured AWS Security Groups to manage inbound and outbound network traffic by opening necessary ports (e.g., 8080 for Jenkins, 9000 for SonarQube, 3000 for Node.js/Grafana, 9090 for Prometheus, 9115 for Blackbox Exporter, SMTP ports).
◦
IAM Roles/Users: Created IAM users with specific policies to grant programmatic access for AWS CLI and Jenkins to interact with AWS services.
•
Container Orchestration with Kubernetes (AWS EKS):
◦
EKS Cluster Deployment: Deployed a managed Kubernetes cluster (EKS) on AWS for scalable and resilient application deployment.
◦
Kubernetes Architecture: Gained insights into Kubernetes master (control plane) and worker node architecture, including components like API server, scheduler, etcd, and controller manager.
◦
Pod Management: Deployed the application as pods within the Kubernetes cluster.
◦
Load Balancers: Exposed the application to the internet using AWS Load Balancers to provide stable access despite dynamic pod IPs.
◦
Auto-healing: Witnessed Kubernetes' auto-healing capabilities by intentionally deleting a pod and observing its automatic replacement.
◦
YAML Manifests: Understood how to define application deployments and services using Kubernetes YAML manifest files.
◦
kubectl and eksctl: Used kubectl for interacting with the Kubernetes cluster and eksctl for managing EKS clusters.
•
Infrastructure as Code (IaC) with Terraform:
◦
Used Terraform to define, provision, and manage AWS infrastructure (e.g., EC2 instances for monitoring servers) as code.
◦
Understood Terraform concepts like main.tf, variables.tf, outputs.tf, and terraform apply/destroy.
•
Monitoring with Prometheus and Grafana:
◦
Prometheus Setup: Deployed and configured Prometheus as a monitoring server to collect metrics.
◦
Grafana Dashboarding: Used Grafana to visualize Prometheus data by importing pre-built dashboards (e.g., for Jenkins, Blackbox Exporter) and creating custom visualizations.
◦
Exporters: Utilized Blackbox Exporter to monitor the availability and performance of external HTTP endpoints (application URL, domain). (Also understood the role of Node Exporter for server metrics, though not explicitly installed in detail).
◦
Configured Prometheus to scrape metrics from various targets including Blackbox Exporter, Jenkins, and the application's domain.
•
Networking and DNS:
◦
Understood concepts of ports (HTTP, HTTPS, Jenkins, SonarQube, Node.js, SMTP, Prometheus, Grafana, Blackbox Exporter).
◦
Configured DNS records (CNAME) using Cloudflare to map a custom subdomain (app.cloudaasim.com) to the application's load balancer for user-friendly access.
◦
Applied SSL/TLS certification to the custom domain for secure connections.
•
Scripting and Automation:
◦
Gained experience in shell scripting for automating repetitive tasks like installing multiple applications and setting permissions on Linux.
◦
Familiarity with basic Linux commands and best practices for server management (e.g., sudo apt update, git clone, chmod, netstat, nano editor).
•
Application Development Stack:
◦
Worked with applications built using Next.js and Node.js, understanding their dependencies and execution environment (npm install, port 3000).
•
Cost Management in Cloud:
◦
Learned the importance of destroying cloud resources after project completion to avoid unnecessary costs and even requesting a bill waiver from AWS

---

