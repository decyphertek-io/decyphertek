Pulumi
=======

"Universal Infrastructure as Code. Every cloud, every language, every architecture, every builder."

Install
-------
```
# Linux ( See Docs - Mac & Windows install )
curl -fsSL https://get.pulumi.com | sh
export PATH=$PATH:$HOME/.pulumi/bin
# YAML - Support by default
# AWS Example ( Supports Azure , GCP , Etc. )
export AWS_ACCESS_KEY_ID=<YOUR_ACCESS_KEY_ID> 
export AWS_SECRET_ACCESS_KEY=<YOUR_SECRET_ACCESS_KEY>
mkdir pulumi && cd pulumi
# You can run Pulumi Locally and avoid the complex setup
pulumi login --local
# OR login to Pulumi if you have a complex team to manage
pulumi new aws-yaml
# Create a login, CLI is free , no worries.
# Create Project - Name . Description, and Stack / Config Saved.
pulumi up 
# Creates an S3 bucket , yes to approve. 
pulumi stack output bucketName
# Pulumi example adds index.html to s3 bucket, useless example.
# Destroy stack, if needed
pulumi destroy
```

Dashboard
----------
```
https://app.pulumi.com
# View Stacks 
> Login > Stacks
```
Integrations
------------
```
* Github
* Gitlab
* Jenkins 
* Spinnaker
* CircleCi
* Travis CI
* Azure Devops
* JetBrains TeamCity
* AWS Code Services
* Google Code Builder
* Kubernetes Operator
* Codefresh
* Octopus
```

References
----------
```
* https://www.pulumi.com/
* https://www.pulumi.com/docs/get-started/aws/begin/

```
