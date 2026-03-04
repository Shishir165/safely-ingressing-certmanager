Safely Ingressing Kubernetes Applications

This project demonstrates how to securely expose Kubernetes applications using NGINX Ingress Controller, Cert-Manager, DuckDNS, and Let's Encrypt on an Azure Kubernetes Service (AKS) cluster.

The lab configures two domains:

HTTP (insecure) access

HTTPS (secure) access with an automatically issued TLS certificate from Let's Encrypt.

Architecture

Internet
↓
DuckDNS Domain
↓
Azure LoadBalancer (AKS)
↓
NGINX Ingress Controller
↓
Kubernetes Service
↓
NGINX Pod

Cert-Manager automates the TLS certificate issuance process using the ACME HTTP-01 challenge.

Domains Used
Domain	Protocol	Purpose
shishir-b.duckdns.org	HTTP	Insecure ingress example
shishir-a.duckdns.org	HTTPS	Secure ingress using Let's Encrypt
Technologies Used

Kubernetes

Azure Kubernetes Service (AKS)

NGINX Ingress Controller

Cert-Manager

Let's Encrypt

DuckDNS

YAML manifests

Project Structure
cert-manager-lab
│
├── manifests
│   ├── nginx-deployment.yaml
│   ├── nginx-service.yaml
│   ├── ingress-shishir-a.yaml
│   ├── ingress-shishir-b.yaml
│   └── letsencrypt-production.yaml
│
└── README.md
Deployment Steps
1. Deploy NGINX Application
kubectl apply -f manifests/nginx-deployment.yaml
kubectl apply -f manifests/nginx-service.yaml
2. Install Cert-Manager
kubectl apply -f https://github.com/cert-manager/cert-manager/releases/latest/download/cert-manager.yaml
3. Create Let's Encrypt ClusterIssuer
kubectl apply -f manifests/letsencrypt-production.yaml
4. Create Ingress Resources

HTTP (Insecure):

kubectl apply -f manifests/ingress-shishir-b.yaml

HTTPS (Secure):

kubectl apply -f manifests/ingress-shishir-a.yaml
5. Verify Resources

Check ingress:

kubectl get ingress

Check certificates:

kubectl get certificate

Expected result:

READY   True
Test the Application

HTTP (Insecure)

http://shishir-b.duckdns.org

HTTPS (Secure)

https://shishir-a.duckdns.org

The HTTPS site should display a valid TLS certificate issued by Let's Encrypt.

Key Learning Outcomes

Configure NGINX Ingress Controller in Kubernetes

Automate TLS certificates with Cert-Manager

Use Let's Encrypt ACME HTTP-01 challenges

Configure DuckDNS for external domain routing

Secure Kubernetes services using HTTPS

Author

Shishir Pariyar

DevOps / Cloud Engineering Learning Project