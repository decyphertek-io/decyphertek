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
    # Example
    $ helm search repo jenkins

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
    

References
----------

    https://microk8s.io/docs/getting-started
