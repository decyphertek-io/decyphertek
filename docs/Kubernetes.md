Microk8s
=====

Microk8s is Canonical's Kubernetes. Easy to install via snap. Enterprise ready or can experiment locally. Crossplatform. 

Install
-------

    $ sudo snap install microk8s --classic 
    $ sudo usermod -a -G microk8s $USER
    $ sudo chown -f -R $USER ~/.kube 
    $ alias kubectl='microk8s kubectl'
    # Logout and back in
    $ microk8s enable dns storage helm3
    $ alias helm='microk8s helm3'
    $ helm repo add stable https://charts.helm.sh/stable
    # Example 1
    $ helm search repo jenkins
    # Example 2
    $ helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
    $ helm repo update
    $ helm install ingress-controller ingress-nginx/ingress-nginx
    $ helm ls
    $ kubectl get deployments

Commands
--------

    $ microk8s status --wait-ready
    $ microk8s stop
    $ microk8s start
    $ microk8s kubectl get nodes
    $ microk8s kubectl get services
    $ microk8s kubectl get pods
    
Deploy Example
---------------

    $ microk8s kubectl create deployment nginx --image=nginx

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

    $ wget https://github.com/vmware-tanzu/octant/releases/download/v0.25.1/octant_0.25.1_Linux-64bit.deb
    $ sudo dpkg -i octant_0.25.1_Linux-64bit.deb

References
----------

    https://microk8s.io/docs/getting-started
    https://devopscube.com/install-configure-helm-kubernetes/
