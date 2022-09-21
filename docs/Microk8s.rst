Microk8s
=====

Microk8s is Canonical's Kubernetes. Easy to install via snap. Enterprise ready or can experiment locally. Crossplatform. 

.. code-block:: console

  ###Microk8s - Install###
  $ sudo snap install microk8s --classic --channel=1.24
  $ sudo usermod -a -G microk8s $USER
  $ sudo chown -f -R $USER ~/.kube 
  $ su - $USER

  ###Microk8s - Commands###
  $ alias kubectl='microk8s kubectl'
  $ microk8s status --wait-ready
  $ microk8s stop
  $ microk8s start
  $ microk8s kubectl get nodes
  $ microk8s kubectl get services
  $ microk8s kubectl get pods
  $ microk8s enable dns storage

  # Deploy Example:
  $ microk8s kubectl create deployment nginx --image=nginx


  ###References###
  https://microk8s.io/docs/getting-started
