Gitpod
=====

     "Gitpod is an open-source developer platform for remote development. Accelerate your 
     teams developer experience, remote collaboration and security - to ship new products 
     faster and more securely."

.. code-block:: console

  ###Gitpod - Install###
  # Requirements:
  # Kubernetes Cluster
  # Cert-Manager installed on the cluster
  # DNS and TLS configured
  $ curl https://kots.io/install | bash
  $ kubectl kots install gitpod
  # Admin Console - http://localhost:8800
  # Follow Repo instructions, OAuth, etc. The Book. 


  ###References###
  https://www.gitpod.io/docs/self-hosted/latest/installing-gitpod