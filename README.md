# microk8s-es-cluster
Example of how to deploy a simple ES Cluster in Microk8s

## How to set up Kubernetes cluster locally with Microk8s (Multipass)

### 1. Before getting started
- Download home-brew: /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
- Download multipass: https://multipass.run/
- Download microk8s: brew install ubuntu/microk8s/microk8s 
- Install microk8s: microk8s install

### 2. Getting started
- Start microk8s: `microk8s status --wait-ready`
    - Start microk8s add-ons: `microk8s enable dns ingress storage dashboard`
- Test microk8s kubernetes: 
    - `microk8s kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1`
    - `microk8s kubectl get pods`
    - Open kubernetes dashboard:
        - Run microk8s dashboard-proxy
        - Open the dashboard: (there will be a line in the console stating what is the dashboard address "Dashboard will be available at https://192.168.64.12:10443")
        - Copy the token from the console and use it to log in the kubernetes dashboard

### 3. Running busybox with privileged user
- Log-in the microk8s virtual machine and add the following configuration in the `/var/snap/microk8s/current/args/kube-apiserver`
    - `allow-privileged=true`
- Restart microk8s services in ubuntu
    - `sudo systemctl restart snap.microk8s.daemon-kubelet.service`
    - `sudo systemctl restart snap.microk8s.daemon-apiserver.service`


note: must set privileged user else elasticsearch pod wont work
