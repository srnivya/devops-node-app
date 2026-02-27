     ** CI/CD Pipeline with Monitoring on AWS**
     
**📌 Project Description**

This project demonstrates an end-to-end DevOps pipeline using Jenkins, Docker, and AWS EC2 with monitoring using Prometheus and Grafana.
**
**🛠 Tech Stack**

          Node.js
          
          Docker
          
          Jenkins
          
          AWS EC2
          
          Docker Hub
          
          Prometheus
          
          Grafana

          Node Exporter

**⚙ Setup Instructions**

  1️⃣ Clone Repository
      git clone <repo-link>
      cd project
  2️⃣ Build Docker Image
      docker build -t app-name .
  3️⃣ Run Container
      docker run -d -p 3000:3000 app-name

**Access application at: http://15.206.123.182:3000**


**🔄 CI/CD Flow**

Code pushed to GitHub.

Jenkins triggered via webhook.

Docker image built.

Image pushed to Docker Hub.

EC2 pulls and deploys container.

Monitoring enabled via Prometheus and Grafana.

