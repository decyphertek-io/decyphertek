Terraform
=====

Manage Cloud Infrastructure as code. 

Install - Ubuntu 20.04/18.04/16.04
---------------------------

    $ sudo apt-get update && sudo apt-get install -y gnupg software-properties-common
    $ wget -O- https://apt.releases.hashicorp.com/gpg | \
        gpg --dearmor | \
        sudo tee /usr/share/keyrings/hashicorp-archive-keyring.gpg
    $ gpg --no-default-keyring \
        --keyring /usr/share/keyrings/hashicorp-archive-keyring.gpg \
        --fingerprint
    # If you are running Ubuntu 20.04 or earlier, than run this. 
    $ echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] \
        https://apt.releases.hashicorp.com $(lsb_release -cs) main" | \
        sudo tee /etc/apt/sources.list.d/hashicorp.list
    $ sudo apt update && sudo apt install -y terraform
    $ terraform -help
    $ terraform -install-autocomplete

Install - Ubuntu 20.04
-----------------------

    $ sudo apt update
    $ sudo apt install  software-properties-common gnupg2 curl
    $ curl https://apt.releases.hashicorp.com/gpg | gpg --dearmor > hashicorp.gpg
    $ sudo install -o root -g root -m 644 hashicorp.gpg /etc/apt/trusted.gpg.d/
    $ sudo apt-add-repository "deb [arch=$(dpkg --print-architecture)] https://apt.releases.hashicorp.com focal main"
    $ sudo apt update && sudo apt install -y terraform

Build infrastructure - AWS
--------------------------

    # install aws cli and set environment variables
    $ sudo apt install python3-pip
    $ pip3 install awscli --upgrade --user
    $ export AWS_ACCESS_KEY_ID=
    $ export AWS_SECRET_ACCESS_KEY=
    # Each Terraform must have its own working directory
    $ mkdir learn-teraform-aws-instance
    $ cd learn-terraform-aws-instance
    $ vim main.tf
    terraform {
      required_providers {
        aws = {
          source  = "hashicorp/aws"
          version = "~> 4.16"
        }
      }

      required_version = ">= 1.2.0"
    }

    provider "aws" {
      region  = "us-west-2"
    }

    resource "aws_instance" "app_server" {
      ami = "ami-830c94e3"
      instance_type = "t2.micro"

      tags = {
        Name = "ExampleAppServerInstance"
      }
    }
    
    $ terraform init
    $ terraform fmt
    $ terraform validate
    $ terraform apply
    $ terraform show

Manually Manage
---------------

    $ terraform state list

Terraform + YAML
----------------

    # https://ascode.run/docs/
    $ wget https://github.com/mcuadros/ascode/releases/download/v1.3.0/ascode-v1.3.0-linux-amd64.tar.gz
    $ tar -xvzf ascode-v1.3.0-linux-amd64.tar.gz
    $ mv ascode /usr/local/bin/

References
----------

    https://www.terraform.io/
    https://learn.hashicorp.com/tutorials/terraform/aws-build?in=terraform/aws-get-started
    https://www.digitalocean.com/community/tutorials/how-to-use-ansible-with-terraform-for-configuration-management
    https://github.com/multycloud/multy