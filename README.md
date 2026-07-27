# Brayan Torres

**Platform engineer — GPU infrastructure and model serving on Kubernetes.** Madrid, Spain.

I run Roche's global Container-as-a-Service platform: GPU node pools on EKS, Triton and Ray Serve for production inference, and 100+ enterprise apps across regions on EKS and on-prem RKE2 — all under GxP regulatory constraints.

Kubestronaut (CKA, CKAD, CKS, KCNA, KCSA) · NVIDIA-Certified Associate, AI Infrastructure & Operations

## What I actually work on

**GPU-accelerated Kubernetes** — NVIDIA GPU Operator, device plugin, DCGM exporter. MIG partitioning and time-slicing to get real utilization out of shared node pools.

**Inference serving** — Triton Inference Server and Ray Serve on EKS, backing production model-serving for data science and research teams.

**Capacity and cost** — Karpenter tuning across GPU-backed NodePools: consolidation, disruption budgets, workload density. Throughput for high-compute ML jobs against reliability and GPU spend.

**The unglamorous half** — ingress and DNS, node lifecycle, image distribution, control-plane failures, and GPU driver/runtime mismatches.

**Platform delivery** — Terraform, ArgoCD, Prometheus/Grafana/Sysdig with SLO dashboards, Vault for secrets, Cilium as kube-proxy replacement for zero-trust networking.

## The stack I operate

**Platform & compute**

<p>
  <img src="https://skillicons.dev/icons?i=kubernetes,aws,gcp,docker,linux" alt="Kubernetes, AWS, GCP, Docker, Linux" height="42"/>
</p>
<p>
  <img src="https://img.shields.io/badge/RKE2-0075A8?style=flat-square" alt="RKE2"/>
  <img src="https://img.shields.io/badge/Karpenter-232F3E?style=flat-square" alt="Karpenter"/>
  <img src="https://img.shields.io/badge/Cilium-F8C517?style=flat-square" alt="Cilium"/>
</p>

**GPU & inference**

<p>
  <img src="https://img.shields.io/badge/NVIDIA%20GPU%20Operator-76B900?style=flat-square&logo=nvidia&logoColor=white" alt="NVIDIA GPU Operator"/>
  <img src="https://img.shields.io/badge/MIG%20%2F%20time--slicing-76B900?style=flat-square" alt="MIG and time-slicing"/>
  <img src="https://img.shields.io/badge/DCGM%20exporter-76B900?style=flat-square" alt="DCGM exporter"/>
  <img src="https://img.shields.io/badge/Triton%20Inference%20Server-76B900?style=flat-square" alt="Triton Inference Server"/>
  <img src="https://img.shields.io/badge/Ray%20Serve-028CF0?style=flat-square" alt="Ray Serve"/>
</p>

**Delivery & observability**

<p>
  <img src="https://skillicons.dev/icons?i=terraform,githubactions,prometheus,grafana" alt="Terraform, GitHub Actions, Prometheus, Grafana" height="42"/>
</p>
<p>
  <img src="https://img.shields.io/badge/ArgoCD-EF7B4D?style=flat-square&logo=argo&logoColor=white" alt="ArgoCD"/>
  <img src="https://img.shields.io/badge/Vault-FFEC6E?style=flat-square&logo=vault&logoColor=black" alt="Vault"/>
  <img src="https://img.shields.io/badge/Sysdig-00AEC7?style=flat-square" alt="Sysdig"/>
</p>

**Data & languages**

<p>
  <img src="https://skillicons.dev/icons?i=python,go,bash,postgres,redis" alt="Python, Go, Bash, PostgreSQL, Redis" height="42"/>
</p>
<p>
  <img src="https://img.shields.io/badge/Airflow-017CEE?style=flat-square&logo=apacheairflow&logoColor=white" alt="Apache Airflow"/>
</p>

## Experience

### **Platform Infrastructure Engineer (L6)** @ Roche · Aug 2024 – Present

Own the global CaaS platform end to end — EKS with GPU node pools, on-prem RKE2, 100+ enterprise apps across regions — from Terraform and ArgoCD through on-call.

Own cloud development for the product: any AWS service or integration the platform needs, from design and implementation through production operation.

Serve ML inference at scale with Triton and Ray Serve for data science and research teams.

Tune Karpenter across GPU-backed NodePools for consolidation, disruption budgets, and workload density.

Built the observability stack on Prometheus, Grafana, and Sysdig with SLO dashboards and alerting — **cut MTTR ~40%**.

Own platform security under pharma regulatory (GxP) constraints: Vault, Cilium, runtime hardening, SAST/SCA in CI.

### **Cloud Infrastructure Architect** @ Amazon Web Services · Nov 2021 – Jul 2024

Architected end-to-end solutions for enterprise customers — from discovery and design through production handover.

Led enterprise cloud migrations and cloud-native builds: data lakes and analytics platforms, microservice architectures, and application modernization.

Designed the full stack per engagement: network topology, storage, compute sizing, and security controls, mapped to each customer's workload profile and regulatory constraints.

Built CI/CD for greenfield and legacy applications, **cutting client time-to-market by 70%+**.

Senior technical advisor on escalations — architecture reviews and production troubleshooting across distributed systems, networking, and cost.

### **Business Manager, Cloud** @ TD Synnex · Feb 2021 – Nov 2021

Ran technical pre-sales and portfolio strategy for 100+ startups and SMEs on AWS and Azure — **grew pipeline $1M+**.

Built a partner enablement program that certified **30+ partners**.

##  Certifications

**Total Active Certifications: 25+** | 🎯 **Kubestronaut** | ☁️ **Multi-Cloud Expert** | 🔐 **Security Focused**

### AWS Certifications (9)
<details>
<summary>View All AWS Certifications</summary>

| Certification | Badge | Year |
|--------------|-------|------|
| **AWS Certified Machine Learning Engineer – Associate** | <img src="https://images.credly.com/size/80x80/images/f36cbbc1-c9f7-4b2c-b92b-f06c7fb8f0fd/image.png" width="60"/> | 2025 |
| **AWS Certified AI Practitioner** | <img src="https://images.credly.com/size/80x80/images/3e68e6e7-35ac-43e4-ab5f-e8a39e8c677b/image.png" width="60"/> | 2025 |
| **AWS Certified Data Engineer – Associate** | <img src="https://images.credly.com/size/80x80/images/f0d3fbb9-bfa7-4017-9989-7bde8eaf42b1/image.png" width="60"/> | 2024 |
| **AWS Certified DevOps Engineer – Professional** | <img src="https://images.credly.com/size/80x80/images/2d84e428-9078-49b6-a804-13c15383d0de/image.png" width="60"/> | 2022 |
| **AWS Certified SysOps Administrator – Associate** | <img src="https://images.credly.com/size/80x80/images/f0d3fbb9-bfa7-4017-9989-7bde8eaf42b1/image.png" width="60"/> | 2022 |
| **AWS Certified Developer – Associate** | <img src="https://images.credly.com/size/80x80/images/b9feab85-1a43-4f6c-99a5-631b88d5461b/image.png" width="60"/> | 2021 |
| **AWS Certified Solutions Architect – Associate** | <img src="https://images.credly.com/size/80x80/images/0e284c3f-5164-4b21-8660-0d84737941bc/image.png" width="60"/> | 2021 |
| **AWS Certified Cloud Practitioner** | <img src="https://images.credly.com/size/80x80/images/00634f82-b07f-4bbd-a6bb-53de397fc3a6/image.png" width="60"/> | 2021 |
| **Well-Architected Proficient** | <img src="https://images.credly.com/size/80x80/images/b870667f-00a3-48d7-b988-9c02b441b883/image.png" width="60"/> | 2022 |

</details>

### ⚓ Kubernetes & Cloud Native (6)
<details>
<summary>View All Kubernetes Certifications</summary>

| Certification | Badge | Year |
|--------------|-------|------|
| **Kubestronaut** (All 5 CNCF K8s Certs) | <img src="https://images.credly.com/size/80x80/images/cd6c6449-6814-4613-a2d3-13cf4ac5be4f/image.png" width="60"/> | 2024 |
| **CKS: Certified Kubernetes Security Specialist** | <img src="https://images.credly.com/size/80x80/images/9945dfcb-1cca-4529-841c-293d8c70c0e5/image.png" width="60"/> | 2024 |
| **CKA: Certified Kubernetes Administrator** | <img src="https://images.credly.com/size/80x80/images/8b8ed108-e77d-4396-ac59-2504583b9d54/cka_from_cncfsite__281_29.png" width="60"/> | 2023 |
| **CKAD: Certified Kubernetes Application Developer** | <img src="https://images.credly.com/size/80x80/images/f88d800c-5261-45c6-9515-0458e31c3e16/ckad_from_cncfsite.png" width="60"/> | 2023 |
| **KCSA: Kubernetes and Cloud Native Security Associate** | <img src="https://images.credly.com/size/80x80/images/a61b5e6d-68ce-4da0-a38b-eff69c45174d/image.png" width="60"/> | 2024 |
| **KCNA: Kubernetes and Cloud Native Associate** | <img src="https://images.credly.com/size/80x80/images/f28f1d88-428a-47f6-95b5-7da1dd6c1000/KCNA_badge.png" width="60"/> | 2024 |

</details>

### ☁️ Microsoft Azure Certifications (9)
<details>
<summary>View All Azure Certifications</summary>

| Certification | Badge | Year |
|--------------|-------|------|
| **Azure Solutions Architect Expert** | <img src="https://images.credly.com/size/80x80/images/987adb7e-49be-4e24-b67e-55986bd3fe66/azure-solutions-architect-expert-600x600.png" width="60"/> | 2020 |
| **Azure AI Engineer Associate** | <img src="https://images.credly.com/size/80x80/images/61f56aa4-16fd-403c-90bc-1d90dba1fa99/image.png" width="60"/> | 2021 |
| **Azure Data Scientist Associate** | <img src="https://images.credly.com/size/80x80/images/5c8fca38-b0d2-49e5-9ad2-f3f8e79b327f/azure-data-scientist-associate-600x600.png" width="60"/> | 2021 |
| **Azure Security Engineer Associate** | <img src="https://images.credly.com/size/80x80/images/1ad16b6f-2c71-4a2e-ae74-ec69c4766039/azure-security-engineer-associate600x600.png" width="60"/> | 2020 |
| **Azure Data Fundamentals** | <img src="https://images.credly.com/size/80x80/images/70eb1e3f-d4de-4377-a062-b20fb29594ea/azure-data-fundamentals-600x600.png" width="60"/> | 2020 |
| **Azure AI Fundamentals** | <img src="https://images.credly.com/size/80x80/images/4136ced8-75d5-4afb-8677-40b6236e2672/azure-ai-fundamentals-600x600.png" width="60"/> | 2020 |
| **Azure Fundamentals** | <img src="https://images.credly.com/size/80x80/images/be8fcaeb-c769-4858-b567-ffaaa73ce8cf/image.png" width="60"/> | 2020 |
| **Power Platform App Maker Associate** | <img src="https://images.credly.com/size/80x80/images/1ad16b6f-2c71-4a2e-ae74-ec69c4766039/azure-security-engineer-associate600x600.png" width="60"/> | 2021 |
| **Power Platform Fundamentals** | <img src="https://images.credly.com/size/80x80/images/2a6251f2-737b-4bf6-9190-d77570cc76fc/CERT-Fundamentals-Power-Platform.png" width="60"/> | 2020 |

</details>

### 🏗️ Infrastructure as Code (1)
<details>
<summary>View IaC Certifications</summary>

| Certification | Badge | Year |
|--------------|-------|------|
| **HashiCorp Certified: Terraform Associate (003)** | <img src="https://images.credly.com/size/80x80/images/85b9cfc4-257a-4742-878c-4f7ab4a2631b/image.png" width="60"/> | 2024 |

</details>

---

<p align="center">
  <a href="https://www.credly.com/users/brayan-andres-torres-contreras">
    <img src="https://img.shields.io/badge/View_All_Certifications-FF6B00?style=for-the-badge&logo=credly&logoColor=white" alt="View All on Credly"/>
  </a>
</p>

## Education

**MSc Artificial Intelligence** — The University of Texas at Austin *(in progress)*
Deep Learning (PyTorch), NLP, Reinforcement Learning, Planning under Uncertainty.

**MSc Big Data & Data Engineering** — Universidad Complutense de Madrid · 9.3/10
Award-winning thesis: production RAG pipeline for pharmaceutical research on GCP — Airflow, Weaviate, Kubernetes — covering ingestion, model serving, and pipeline automation.

**BSc Electronic Engineering** — Universidad de los Andes, Colombia

## Currently

Benchmarking GPU sharing strategies (MIG vs. time-slicing) for mixed inference and training workloads, and writing up Kubernetes internals and incident post-mortems at [brayanto.dev](https://brayanto.dev/blog).

Mentor on the AWS Tech U program since 2023 — cloud architecture, infrastructure delivery, and debugging.

## Contact

[LinkedIn](https://www.linkedin.com/in/brayan-torres-re7a9839137/) · [brayanto.dev](https://brayanto.dev) · [Blog](https://brayanto.dev/blog) · [Credly](https://www.credly.com/users/brayan-andres-torres-contreras) · brayantcwork@gmail.com

