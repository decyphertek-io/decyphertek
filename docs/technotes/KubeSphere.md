KubeSphere
===========

"KubeSphere is a distributed operating system for cloud-native application management, using Kubernetes as its kernel. It provides a plug-and-play architecture, allowing third-party applications to be seamlessly integrated into its ecosystem."

Install
--------

    # Install Microk8s , Helm3 , First , then run. 
    kubectl apply -f https://github.com/kubesphere/ks-installer/releases/download/v3.3.2/kubesphere-installer.yaml
    kubectl apply -f https://github.com/kubesphere/ks-installer/releases/download/v3.3.2/cluster-configuration.yaml
    # Once logs stop , ctrl +c
    kubectl logs -n kubesphere-system $(kubectl get pod -n kubesphere-system -l 'app in (ks-install, ks-installer)' -o jsonpath='{.items[0].metadata.name}') -f
    kubectl get svc/ks-console -n kubesphere-system
    # Allow Inbound 30880 , host firewall and security group.  ( If using nginx , not required. ) 
    sudo ufw allow 30880/tcp 
    # Login 
    # http://ip-of-server:30880
    user:admin pass:P@88w0rd


References
----------

    https://kubesphere.io/docs/v3.3/quick-start/minimal-kubesphere-on-k8s/
