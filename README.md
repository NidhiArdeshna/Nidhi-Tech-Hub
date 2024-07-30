# DVWA Kubernetes Deployment and Attack Demo

## Setup

1. Install Minikube: [Minikube Installation Guide](https://minikube.sigs.k8s.io/docs/start/)
2. Start Minikube:
    ```sh
    minikube start
    ```
3. Deploy DVWA:
    ```sh
    kubectl apply -f dvwa-deployment.yaml
    ```
4. Access DVWA at `http://<minikube-ip>:30001`.

## Attack Vectors

### 1. SQL Injection
- Steps to perform SQL Injection can be found [here](./attack_vectors/sql_injection.md).

### 2. Cross-Site Scripting (XSS)
- Steps to perform XSS can be found [here](./attack_vectors/xss.md).

### 3. File Upload
- Steps to perform File Upload attack can be found [here](./attack_vectors/file_upload.md).

