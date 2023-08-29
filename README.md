
# Argo CD 

ArgoCD is a Continuous Delivery (CD) tool that has gained popularity in DevOps for performing application delivery onto Kubernetes. It relies on a deployment method known as GitOps. GitOps is a mechanism that can pull the latest code and application configuration from the last known Git commit version and deploy it directly into Kubernetes resources. The wide adoption and popularity are because ArgoCD helps developers manage infrastructure and applications lifecycle in one platform.



## Table of content

- Prerequisites
- Install Argo CD CLI
- Install Argo CD UI to the cluster
- Access Argo CD API Server
- Login to Argo CD in UI
- Deploy simple Application 
- Deploy Argo CD Application using UI interface


- Install Argo CD CLI

        curl -sSL -o argocd-linux-amd64 https://github.com/argoproj/argo-cd/releases/latest/download/argocd-linux-amd64 

        sudo install -m 555 argocd-linux-amd64 /usr/local/bin/argocd

        rm argocd-linux-amd64

We need to install Argo CD to our cluster to be able to deploy applications.

- Install Argo CD UI to the cluster

        kubectl create namespace argocd

        kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml


This will create a namespace within your cluster and Argo CD services and applications.



By default, Argo CD API server is not exposed to external IP for security reasons. For this tutorial, we will access the server using port forwarding. Kubectl port-forwarding is used to connect to the API server without exposing the service to outside. We will use the same method for our example application.

-  Access Argo CD API Server

        kubectl port-forward svc/argocd-server -n argocd --address 0.0.0.0  8081:443


This will expose Argo CD service to localhost:8080


- Login to Argo CD in console

Before we access the Argo CD UI, we need to get the admin password. Let's get the password.


        kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo

- Login Argo CD UI

Now, let's go to localhost:8080 to access the UI.
