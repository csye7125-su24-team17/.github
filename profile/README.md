# RAG and LLM-Based CVE Application hosted on Kubernetes 
[<img src="https://img.shields.io/badge/-AWS-FF9900?logo=amazonaws&logoColor=white&style=plastic" width="70" height="40" />](https://aws.amazon.com/)
[<img src="https://img.shields.io/badge/-Terraform-623CE4?logo=terraform&logoColor=white&style=plastic" width="150" height="40" />](https://www.terraform.io/)
[<img src="https://img.shields.io/badge/-Go-00ADD8?" width="0" height="40" />](https://go.dev/)
[<img src="https://img.shields.io/badge/-Jenkins-D24939?logo=jenkins&logoColor=white&style=plastic" width="120" height="40" />](https://www.jenkins.io/)
[<img src="https://img.shields.io/badge/-Docker-2496ED?logo=docker&logoColor=white&style=plastic" width="120" height="40" />](https://www.docker.com/)
[<img src="https://img.shields.io/badge/-Kubernetes-326CE5?logo=kubernetes&logoColor=white&style=plastic" width="190" height="40" />](https://kubernetes.io/)
[<img src="https://img.shields.io/badge/-Istio-466BB0?logo=istio&logoColor=white&style=plastic" width="100" height="40" />](https://istio.io/)
[<img src="https://img.shields.io/badge/-Prometheus-E6522C?logo=prometheus&logoColor=white&style=plastic" width="160" height="40" />](https://prometheus.io/)
[<img src="https://img.shields.io/badge/-Grafana-F46800?logo=grafana&logoColor=white&style=plastic" width="120" height="40" />](https://grafana.com/)
[<img src="https://img.shields.io/badge/-HuggingFace-FFAE1A?logo=huggingface&logoColor=white&style=plastic" width="170" height="40" />](https://huggingface.co/)
[<img src="https://img.shields.io/badge/-Pinecone-339933?logo=pinecone&logoColor=white&style=plastic" width="110" height="40" />](https://www.pinecone.io/)
[<img src="https://img.shields.io/badge/-LLaMA_3-7289DA?logo=ai&logoColor=white&style=plastic" width="100" height="40" />](https://ai.meta.com/llama/)

## Overview 



## Architecture  
![Architecture Diagram](https://raw.githubusercontent.com/csye7125-su24-team17/.github/main/profile/Architecture%20Diagram.png)

## Key Features 

- **Go-based CVE Processor and Consumer Application with Kafka**  
The core of our system is built around a Go-based CVE Processor that downloads, extracts, and processes JSON files from [CVEProject's Official GitHub Repository](https://github.com/CVEProject/cvelistV5/archive/refs/heads/main.zip), and then pushes it to a Kafka topic.

    Next, we have a Go-based CVE Consumer that retrieves those messages from Kafka and stores them in a PostgreSQL database. Before storing in Postgres, we have Flyway migration scripts to automatically create the necessary schema, tables, and views in PostgreSQL.

    We maintain Dockerfiles for the Flyway migration scripts, the CVE processor, and the CVE consumer applications. These Docker images are integrated into custom Helm charts that are deployed to an EKS Cluster, provisioned through Terraform. The PostgreSQL database is deployed using Bitnami's Helm chart. 
    
    Whenever we push code to these repositories on GitHub, Jenkins builds and publishes multi-architecture Docker images (supporting both arm and amd architectures) to our private Docker Hub repositories.
    
- **CI/CD Pipeline with Jenkins**  
The 