Kubernetes
==========

There is a few different ways to run Kubernetes, which can be viewed as a networking solution to containers. 
Setuping clusters and nodes via a yaml configuration can simplify infrastructure deployment. Some of the 
kubernetes options is AWS Eks , Microk8s , CoreOS , Rancher , Minikube , OpenShift, OKD, etc. 

Recomendation:
--------------
If you are running kubernetes locally, K3s & Headlamp are an easy way yo get up an running on Linux.

K3s
----
Rancher provides a lightwieght Kubernetes that is easy to install

    curl -sfL https://get.k3s.io | sh - 
    # Check for Ready node, takes ~30 seconds 
    sudo k3s kubectl get node 

AWS EKS
-------
Amazon provides a way to run Kubernetes locally then push to the cloud. ( Not updated since 2021 )

    sudo snap install eks --classic --edge

Deploy existing local kubernetes , what ever version, to AWS EKS

    https://blog.devops.dev/deploying-kubernetes-pods-configs-into-aws-eks-cluster-using-github-actions-ff6f5b8adf47

Microk8s
---------
Microk8s is Canonical's Kubernetes. Easy to install via snap. Enterprise ready or can experiment locally. Crossplatform. 

MicroK8s - Install
------------------
  
    $ sudo snap install microk8s --classic 
    $ sudo usermod -a -G microk8s $USER
    $ sudo chown -f -R $USER ~/.kube 
    $ sudo microk8s config > ~/.kube/config
    $ echo "alias kubectl='microk8s kubectl'" >> ~/.bashrc
    # Logout and back in
    $ microk8s enable dns storage helm3 ingress registry
    $ echo "alias helm='microk8s helm3'" >> ~/.bashrc
    # Logout and back in . 
    $ helm repo add stable https://charts.helm.sh/stable
    # Example 1
    $ helm search repo ingress-nginx
    # Example 2
    $ helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
    $ helm repo update
    $ helm install ingress-controller ingress-nginx/ingress-nginx
    $ helm ls
    $ kubectl get deployments

MicroK8s - Commands
------------------

    $ microk8s status --wait-ready
    $ microk8s stop
    $ microk8s start
    $ microk8s kubectl get nodes
    $ microk8s kubectl get services
    $ microk8s kubectl get pods
    
Microk8s - Deploy Example
------------------------

    $ microk8s kubectl create deployment nginx --image=nginx

Optional: Machine learning Projects:
-----------------------------------

    Install with a single command:
    You can install all Kubeflow official components (residing under apps) and all common services (residing under common) using the following command:
    Once, everything is installed successfully, you can access the Kubeflow Central Dashboard by logging in to your cluster.
    Congratulations! You can now start experimenting and running your end-to-end ML workflows with Kubeflow.

    $ git clone https://github.com/kubeflow/manifests.git
    $ cd manifests/apps/
    $ while ! kustomize build example | kubectl apply -f -; do echo "Retrying to apply resources"; sleep 10; done
    $ cd .. && cd common/
    $ while ! kustomize build example | kubectl apply -f -; do echo "Retrying to apply resources"; sleep 10; done

    https://www.kubeflow.org/
    https://www.kubeflow.org/docs/started/installing-kubeflow/

Optional: Headlamp
-------------------

    https://headlamp.dev/

Optional: Karpenter
-------------------

    https://karpenter.sh/

Optional: Kompose
------------------

    https://kompose.io/

Optional: Kubsphere
--------------------

    https://kubesphere.io/

Optional: Lens IDE
------------------

    # Desktop APP (Client Side) - Debian Package
    $ wget https://api.k8slens.dev/binaries/Lens-2022.11.101953-latest.amd64.deb
    $ sudo dpkg -i Lens-2022.11.101953-latest.amd64.deb
    # Create an account to use
    
Optional: K9
------------

    # Manage K8s via terminal - Install via Linuxbrew
    $ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
    $ brew install derailed/k9s/k9s

Optional: Ocatant
-----------------

    # Limitations , Yaml read only in gui. 
    $ wget https://github.com/vmware-tanzu/octant/releases/download/v0.25.1/octant_0.25.1_Linux-64bit.deb
    $ sudo dpkg -i octant_0.25.1_Linux-64bit.deb
    <OR>
    # Desktop App Mac / Linux
    $ brew install octant

Optional: KubeNav
----------------

    # One of the only currently available Android Kubernetes management apps. 
    https://play.google.com/store/apps/details?id=io.kubenav.kubenav&gl=US

Optional: Kubevious
--------------------

    # manage Kubernetes remotely form the desktop and get insights into security configurations.
    https://kubevious.io/open-source


References
----------

    https://microk8s.io/docs/getting-started
    https://devopscube.com/install-configure-helm-kubernetes/
    https://medium.com/dictcp/kubernetes-gui-clients-in-2020-kube-dashboard-lens-octant-and-kubenav-ce28df9bb0f0
