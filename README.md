# GitOps Demo App with Argo CD and Kubernetes

This project demonstrates how to implement **GitOps** using **Argo CD**, **Kubernetes (Minikube)**, and **GitHub**. The application is deployed and managed by syncing its state directly from a Git repository.

---

## 🚀 Objective

- Deploy an application to Kubernetes using Argo CD.
- Sync application state from Git automatically.
- Enable Auto-Sync, Auto-Prune, and Self-Heal to ensure the cluster stays aligned with Git.

---

## 📦 Tools Used

- **Minikube** – Local Kubernetes cluster.
- **Argo CD** – GitOps continuous delivery tool.
- **GitHub** – Source repository for application manifests.
- **kubectl / argocd CLI** – Command-line tools for interacting with the cluster and Argo CD.

---

## ✅ How It Works

1. Application manifests are stored in a GitHub repository.
2. Argo CD monitors the repository and applies changes to the cluster.
3. Changes pushed to Git are automatically applied (Auto-Sync).
4. Removed resources in Git are deleted from the cluster (Auto-Prune).
5. Drifted resources are fixed automatically (Self-Heal).

---

## ⚙ Setup Overview

1. Start Minikube and install Argo CD.
2. Access the Argo CD UI via port-forwarding.
3. Connect your GitHub repository containing the manifests.
4. Create an application in Argo CD pointing to your repository.
5. Enable Auto-Sync, Auto-Prune, and Self-Heal.
6. Verify that Git changes are reflected in the cluster.

---

## 📖 How to Verify the GitOps Workflow

### ✅ 1. Auto-Sync

- Edit the deployment manifest in Git by increasing replicas from 2 to 3.
- Push the changes.
- Argo CD automatically syncs the deployment and updates the cluster.

```bash
kubectl get deployment nginx-deployment
````

You should see the updated replica count.

---

### ✅ 2. Auto-Prune

* Delete the service manifest from Git.
* Push the changes.
* Argo CD automatically removes the service from the cluster.

```bash
kubectl get svc
```

The service should no longer exist.

---

### ✅ 3. Self-Heal

* Manually scale the deployment in the cluster.

```bash
kubectl scale deployment nginx-deployment --replicas=5
kubectl get deployment nginx-deployment
```

* Argo CD detects the drift and restores the original replica count defined in Git.

```bash
kubectl get deployment nginx-deployment
```

The replicas will be reverted to the correct number.

---

## 📸 Screenshots

### ✅ 1. Argo CD Dashboard

The application is synced and healthy with Auto-Sync, Prune, and Self-Heal enabled.

![Argo CD Dashboard showing nginx-app synced and healthy](screenshots/argocd-dashboard.png)

---

### ✅ 2. Sync Process

After updating replicas in Git, Argo CD automatically syncs the changes.

![Argo CD syncing the application after Git changes](screenshots/sync-process.png)

---

### ✅ 3. Self-Heal in Action

When the deployment is manually scaled, Argo CD detects the drift and reverts it to the correct state.

![Argo CD reverting a manual change to deployment replicas](screenshots/self-heal.png)

---

### ✅ 4. Final Working State

The deployment and service are running as expected after syncing.

![Argo CD showing synced and healthy state after updates](screenshots/final-state.png)

---

### ✅ 5. Application Webpage

The Nginx default webpage served by the deployed service confirms the application is accessible.

![Nginx webpage running on the cluster](screenshots/nginx-webpage.png)

---

## 📂 Deliverables

* GitHub repository containing deployment and service manifests.
* Argo CD screenshots showing the application’s status and features.
* Documentation explaining the setup, workflow, and verification steps.

---

## 📌 Final Notes

* This project sets up a **complete GitOps pipeline**, where the source of truth is Git.
* **Auto-Sync**, **Auto-Prune**, and **Self-Heal** ensure that the cluster always reflects the desired state.
* It can be easily extended to multi-environment setups and more complex workflows.



