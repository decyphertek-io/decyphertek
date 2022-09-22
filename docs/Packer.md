Packer
=====

Open Source cross cloud image builder. Run via Cli and build for multiple cloud platforms

Install
-------

    $ wget -O- https://apt.releases.hashicorp.com/gpg | gpg --dearmor | sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
    $ echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
    $ sudo apt update && sudo apt install packer

AWS Creds
---------

    $ export AWS_ACCESS_KEY_ID=”anaccesskey”
    $ export AWS_SECRET_ACCESS_KEY=”asecretkey”
    $ export AWS_DEFAULT_REGION=”us-east-1"

Example
-------
  
    $ vim packer-aws-quick-start.pkr.hcl 
    variable "access_key" {
      type    = string
      default = "${env("AWS_ACCESS_KEY_ID")}"
    }

    variable "secret_key" {
      type      = string
      default   = "${env("AWS_SECRET_ACCESS_KEY")}"
      sensitive = true
    }

    locals { timestamp = regex_replace(timestamp(), "[- TZ:]", "") }

    source "amazon-ebs" "quick-start" {
      access_key    = "${var.access_key}"
      ami_name      = "ami-name ${local.timestamp}"
      instance_type = "t2.micro"
      region        = "us-east-1"
      secret_key    = "${var.secret_key}"
      source_ami    = "ami-0000000"
      ssh_username  = "username"
    }

    build {
      sources = ["source.amazon-ebs.quick-start"]
    }

AWS Image
---------

    $ packer init .
    $ packer fmt .
    $ packer validate .
    $ packer build  packer-aws-quick-start.pkr.hcl


References
----------

https://github.com/hashicorp/packer
https://www.packer.io/
https://learn.hashicorp.com/tutorials/packer/aws-get-started-provision?in=packer/aws-get-started
https://marketplace.visualstudio.com/items?itemName=4ops.packer
https://www.packer.io/plugins/provisioners/ansible/ansible
https://tekanaid.com/posts/hashicorp-packer-terraform-and-ansible-to-set-up-jenkins/
