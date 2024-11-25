
# ArgoCD Application Repository

This repository contains a sample application designed to demonstrate the deployment capabilities of [ArgoCD](https://argo-cd.readthedocs.io/), a declarative, GitOps continuous delivery tool for Kubernetes.

## Repository Structure

- `application.yaml`: Defines the ArgoCD Application resource, specifying the source repository, target namespace, and sync policies.

## Prerequisites

Before deploying this application, ensure you have the following:

- A running Kubernetes cluster.
- ArgoCD installed and configured in your cluster. ([Installation Guide](https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd))
- `kubectl` command-line tool configured to interact with your cluster.

## Deployment Instructions

1. **Install ArgoCD**: If ArgoCD is not already installed, follow the [official installation guide](https://argo-cd.readthedocs.io/en/stable/getting_started/#1-install-argo-cd).

2. **Apply the Application Manifest**: Deploy the application by applying the `application.yaml` manifest:

   ```bash
   kubectl apply -f application.yaml
   ```

3. **Access the ArgoCD Web UI**: To monitor the deployment, access the ArgoCD Web UI. Forward the ArgoCD server service to your local machine:

   ```bash
   kubectl port-forward svc/argocd-server -n argocd 8080:443
   ```

   Then, navigate to `https://localhost:8080` in your browser.

4. **Login to ArgoCD**: Retrieve the initial admin password:

   ```bash
   kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 --decode
   ```

   Use `admin` as the username and the decoded password to log in.

5. **Sync the Application**: In the ArgoCD Web UI, locate the newly created application and initiate a sync to deploy the resources to your cluster.
