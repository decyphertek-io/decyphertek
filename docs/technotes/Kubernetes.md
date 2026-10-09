Kubernetes
==========

Kubernetes via k0s, a single binary that runs the whole cluster. Great for a single node &
easy to expand later. These notes cover K0s, Helm, & Headlamp ( web UI ).

K0s - Install
-------------
```
curl --proto '=https' --tlsv1.2 -sSf https://get.k0s.sh | sudo sh
sudo k0s install controller --single
sudo k0s start
sudo k0s status
sudo k0s kubectl get nodes

# Export the kubeconfig for helm, headlamp, etc ( k0s also embeds kubectl )
mkdir -p ~/.kube
sudo k0s kubeconfig admin > ~/.kube/config
chmod 600 ~/.kube/config
```
* `--single` sets up a controller + worker in one & cannot be extended later. Use `--enable-worker --no-taints` instead if you may add nodes.

Helm - Install
--------------
```
curl -fsSL https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
helm version
```

Headlamp - Install
------------------
Kubernetes web UI, deployed in-cluster with helm.
```
helm repo add headlamp https://kubernetes-sigs.github.io/headlamp/
helm repo update
helm install my-headlamp headlamp/headlamp --namespace kube-system

# Create an admin user & token to log in with
kubectl create serviceaccount headlamp-admin --namespace kube-system
kubectl create clusterrolebinding headlamp-admin --serviceaccount=kube-system:headlamp-admin --clusterrole=cluster-admin
kubectl create token headlamp-admin --namespace kube-system

# Open http://localhost:8080 & paste the token
kubectl port-forward -n kube-system svc/my-headlamp 8080:80
```

K0s - Commands
--------------
```
sudo k0s status
sudo k0s stop
sudo k0s start
sudo k0s kubectl get nodes -o wide
sudo k0s kubectl get pods -A
sudo k0s kubectl get svc -A
sudo k0s kubectl create deployment nginx --image=nginx
sudo k0s kubectl scale deployment nginx --replicas=2
sudo k0s kubectl delete deployment nginx

# Add another node: create a token on the controller, then on the new node
sudo k0s token create --role=worker
sudo k0s install worker --token-file /path/to/token
sudo k0s start

# Uninstall
sudo k0s stop
sudo k0s reset
reboot
```

References
----------
* https://k0sproject.io/
* https://docs.k0sproject.io/stable/install/
* https://helm.sh/docs/intro/install/
* https://github.com/kubernetes-sigs/headlamp/tree/main/charts/headlamp
