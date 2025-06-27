# 🚀 DevOps EKS Portfolio

A battle-tested, enterprise-grade DevOps portfolio project, purpose-built to showcase best practices and real-world deployment pipelines in a modern cloud-native environment. Designed for engineers aspiring to master infrastructure as code, Kubernetes orchestration, and robust CI/CD workflows, this project reflects 20+ years of industry experience in scalable systems engineering.

---

## 📂 Repository: `devops-eks-portfolio`

This repository demonstrates the following advanced concepts:

- 🔧 Infrastructure provisioning using **Terraform** with reusable modules
- ⚙️ End-to-end CI/CD pipeline with **GitHub Actions** and multi-environment workflows
- 🐳 Containerization with **Docker** following OCI standards
- ☸️ Scalable deployments to **Kubernetes (EKS)** with service discovery and health checks
- 📈 Production-grade observability with **Prometheus**, **Grafana**, and alerting integrations
- 🔐 Secrets lifecycle management with **AWS SSM**, **Sealed Secrets**, and best practices
- 🧩 Optional integrations with **Ansible**, **Helm**, and **ArgoCD** for enhanced flexibility

---

## 🧱 Tech Stack Overview

| Category         | Tools & Services                     |
|------------------|--------------------------------------|
| Cloud Platform   | AWS (EKS, IAM, S3, SSM)              |
| IaC              | Terraform (Modular, version-locked)  |
| Containerization | Docker (Multi-stage, secure builds)  |
| Orchestration    | Kubernetes (EKS, autoscaling)        |
| CI/CD            | GitHub Actions, ECR, kubectl         |
| Monitoring       | Prometheus, Grafana, AlertManager    |
| Secrets Mgmt     | AWS SSM, Sealed Secrets, GitHub OIDC |
| Configuration    | Helm (templating), Ansible (provisioning) |

---

## 🧩 Project Structure

```bash
devops-eks-portfolio/
├── .github/
│   └── workflows/
│       └── ci-cd.yml             # Multi-stage CI/CD pipeline
├── terraform/
│   ├── modules/                  # Reusable modules (VPC, EKS, IAM)
│   ├── main.tf                   # Root configuration
│   └── variables.tf
├── k8s/
│   ├── deployment.yaml
│   ├── service.yaml
│   └── configmap.yaml
├── helm/
│   └── chart/                    # Optional Helm packaging
├── docker/
│   ├── Dockerfile                # Hardened image
│   └── .dockerignore
├── observability/
│   ├── prometheus-config.yaml
│   ├── grafana-dashboard.json
│   └── alertmanager.yaml
├── ansible/
│   └── site.yml
├── scripts/
│   └── deploy.sh
├── README.md
└── LICENSE
```

---

## 🛠️ Getting Started

### 🔐 Prerequisites

- AWS CLI + IAM credentials with EKS & SSM access
- Docker, kubectl, Terraform, and GitHub CLI installed
- Kubernetes 1.27+ compatible environment

### 1️⃣ Provision Infrastructure with Terraform

```bash
cd terraform
terraform init
terraform plan -out=tfplan
terraform apply tfplan
```

> This setup uses separate state files per environment and remote state in S3 with DynamoDB locking.

### 2️⃣ Configure `kubectl`

```bash
aws eks update-kubeconfig --name prod-eks-cluster --region us-east-1
```

### 3️⃣ Deploy Application

```bash
kubectl apply -f k8s/
```

---

## ⚙️ CI/CD Pipeline (GitHub Actions)

File: `.github/workflows/ci-cd.yml`

### Features:

- Push to `main` triggers full build-test-deploy cycle
- Docker image pushed to Amazon ECR with GitHub OIDC authentication
- Automated rolling deployments to EKS
- Branch protection, matrix builds, cache optimization

---

## 🔐 Secrets Management

This repo follows security-first design with multiple layers of secrets handling:

| Scope           | Strategy                      |
|----------------|-------------------------------|
| Terraform       | AWS SSM Parameter Store       |
| GitHub Actions  | GitHub OIDC + Encrypted Secrets |
| Kubernetes      | Bitnami Sealed Secrets        |

```bash
kubeseal < k8s/secret.yaml > k8s/sealed-secret.yaml
kubectl apply -f k8s/sealed-secret.yaml
```

---

## 📈 Monitoring & Observability

```bash
kubectl apply -f observability/prometheus-config.yaml
kubectl apply -f observability/grafana-dashboard.json
kubectl apply -f observability/alertmanager.yaml
```

### Access Grafana

```bash
kubectl port-forward svc/grafana 3000:3000
```

- Default credentials: `admin / admin`
- Change immediately in production

---

## 🚀 Optional Extensions

- 🔄 GitOps with ArgoCD or FluxCD
- 🔐 HashiCorp Vault integration
- 🧰 Jenkins or Tekton pipelines
- 🌍 Ingress with cert-manager + Let's Encrypt
- 📦 Helm umbrella charts for staging/prod

---

## 📘 References

- [Terraform EKS Module](https://registry.terraform.io/modules/terraform-aws-modules/eks/aws/latest)
- [Kubernetes Docs](https://kubernetes.io/docs/)
- [GitHub Actions](https://docs.github.com/en/actions)
- [Prometheus Operator](https://github.com/prometheus-operator/prometheus-operator)
- [Bitnami Sealed Secrets](https://github.com/bitnami-labs/sealed-secrets)

---

## 👨‍🏫 About the Author

**Raja Muhammad Awais**  
Principal DevOps Engineer | Cloud Architect | Open Source Contributor  
📧 smdevops24@gmail.com | 🌐 
🔗 [GitHub](https://github.com/RajaMuhammadAwais) | [LinkedIn](https://pk.linkedin.com/in/raja-muhammad-awais-turk)

---

## 📄 License

This repository is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---