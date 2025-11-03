# Qr-Code-Generator

An app that converts a URL to a QR Code. 


# 📘 Overview

QR Code Generator is a full-stack web application that converts URLs into downloadable QR codes.
It demonstrates key DevOps practices such as containerization, infrastructure as code (IaC), continuous deployment, and cloud orchestration.

# Components

Frontend: Next.js web app where users submit URLs.

Backend (API): FastAPI service that generates and uploads QR codes to AWS S3.

Storage: AWS S3 bucket for storing generated QR images.



# Goal

To apply real-world DevOps principles — automating infrastructure setup, container orchestration, and deployment workflows using Docker, Terraform, and Kubernetes (EKS).

# ⚙️ Technologies Used

<img width="738" height="341" alt="image" src="https://github.com/user-attachments/assets/67e4abec-d408-4aac-97db-5e27b5f8bb9a" />


🧩 Application Structure
devops-qr-code/
│
├── api/                 → FastAPI backend  
├── front-end-nextjs/    → Next.js frontend  
├── infrastructure/      → Terraform & Kubernetes files  
└── README.md

# Architecture Workflow

This diagram visualizes how the frontend, backend, Dockerfiles, and cloud storage integrate in the DevOps pipeline:

<img width="1024" height="1024" alt="image" src="https://github.com/user-attachments/assets/4ccbeab6-7806-48f5-8c8c-8be68ffef58b" />


Flow Explanation



Frontend (NextJS) → Sends user-entered URLs to the backend.

Backend (FastAPI) → Generates QR codes and uploads them to AWS S3.

Cloud Bucket Storage (S3) → Stores generated QR codes securely.

Front-End & Back-End Dockerfiles → Package each app as a container.

Docker Hub → Hosts container images for deployment on EKS.



🧱 Running Locally
🔹 Backend (FastAPI)
git clone https://github.com/neyocloud/devops-qr-code.git
cd api
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt


Create a .env file and include:

AWS_ACCESS_KEY_ID=<your-access-key>
AWS_SECRET_ACCESS_KEY=<your-secret-key>
BUCKET_NAME=<your-s3-bucket-name>


Run the API:

uvicorn main:app --reload


➡️ Runs on http://localhost:8000

** 🔹 Frontend (Next.js) **
cd front-end-nextjs
npm install
npm run dev 


➡️ Runs on http://localhost:3000

☁️ Cloud Deployment
🏗️ Infrastructure (Terraform + EKS)

Terraform provisions:

VPC + Subnets

Internet Gateway + Route Tables

EKS Cluster + Node Groups

Commands:

terraform init
terraform validate
terraform apply


Update kubeconfig:

aws eks update-kubeconfig --name my-cluster-eks --region us-east-1 --profile devops

# 🚀 Deployment (Kubernetes)

# Frontend Deployment
<img width="1512" height="982" alt="image" src="https://github.com/user-attachments/assets/2b95a8c8-3abf-4388-afe3-ad056dcaed61" />


# Backend Deployment

<img width="1512" height="982" alt="image" src="https://github.com/user-attachments/assets/5eaf0f05-a914-44e0-9945-0ee5a466dd9c" />


# Challenges & Fixes


# Issue	Cause	Solution


Invalid AWS credentials	CLI not configured	Created IAM user and configured with aws configure
Terraform duplicate resources	Same resource names	Renamed subnets and unified provider block
Unsupported EKS version (1.27)	Deprecated by AWS	Updated to 1.30
ImagePullBackOff	Docker images missing	Rebuilt and pushed latest images
Frontend not connecting to backend	Wrong endpoint	Used Kubernetes DNS (qr-api-service:8000)



# ✅ Result

✔️ Infrastructure provisioned with Terraform


✔️ Containers deployed to AWS EKS


✔️ Frontend exposed via LoadBalancer


✔️ Backend connected to AWS S3


✔️ QR codes generated and downloadable successfully



# Cleanup
terraform destroy
kubectl delete all --all

# Key Learnings

Automated cloud deployment with Terraform and EKS

Containerized microservices using Docker

Kubernetes networking and LoadBalancer setup

Debugging CI/CD and AWS integration

Strengthened the DevOps principle: Automate Everything

# Conclusion

The QR Code Generator project highlights how DevOps transforms a simple app into a cloud-native, automated, and scalable system.
By integrating Docker, Terraform, and Kubernetes, the deployment process became:

✅ Fully Automated
✅ Easily Replicable
✅ Highly Scalable
✅ Cloud Cost-Efficient
