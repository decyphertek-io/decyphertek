AWS CLI
========

AWS CLI provides infrastructure as code methodology. 

Install
-------

     # Linux
     curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
     unzip awscliv2.zip
     # This saves aws creds under root user.
     # Beneficial if you have ansible installed via Linux at /etc/ansible/ 
     sudo ./aws/install
     sudo aws configure
     # Mac
     python3 -m pip install --user awscli

EC2 Commands
--------------

    # configure AWS - May need to use sudo if installed via sudo 
    aws configure
    # List EC2 instances
    aws ec2 describe-instances --query 'Reservations[].Instances[].[State.Name, InstanceId, ImageId, InstanceType, PublicIpAddress, SubnetId, VpcId,Tags[?Key==`Name`]| [0].Value]' 
    # List Vpcs
    aws ec2 describe-vpcs
    # List Subnets
    aws ec2 describe-subnets
    # List Security Groups
    aws ec2 describe-security-groups --query "SecurityGroups[*].{Name:GroupName,ID:GroupId}"
    aws ec2 describe-security-group-rules --filter Name="group-id",Values="sg-1234567890abcdef0"
    # Add an inbound rule to security group (cidr range optional)
    aws ec2 authorize-security-group-ingress \
    --group-id sg-1234567890abcdef0 \
    --protocol tcp \
    --port 22 \
    --cidr 203.0.113.0/24
    # Manage Ec2 state
    aws ec2 start-instances --instance-ids i-1234567890abcdef
    aws ec2 stop-instances --instance-ids i-1234567890abcdef
    aws ec2 terminate-instances --instance-ids i-1234567890abcdef
    # Create an AMI from an instance ID
    aws ec2 create-image \
    --instance-id i-1234567890abcdef0 \
    --name "My server" \
    --description "An AMI for my server"
    # Get account number
    aws sts get-caller-identity --query "Account"
    # List AMI owned by account #
    aws ec2 describe-images --owners 123123123123 --query 'Images[].[ImageId,Name]' | grep "-"

ECS Commands:
-------------

    aws ecs list-clusters
    aws ecs describe-clusters --clusters your_cluster_name_or_arn
    aws ecs list-services --cluster your_cluster_name_or_arn
    aws ecs describe-services --cluster your_cluster_name_or_arn --services your_service_name
    aws ecs list-tasks --cluster your_cluster_name_or_arn
    aws ecs describe-tasks --cluster your_cluster_name_or_arn --tasks your_task_id
    aws ecs list-container-instances --cluster your_cluster_name_or_arn
    aws ecs describe-container-instances --cluster your_cluster_name_or_arn --container-instances your_container_instance_id

Docker compose to ECS
---------------------

    This has been depracated. Not sure why, no longer works. 

References
----------

    https://docs.aws.amazon.com/cli/latest/
    https://awscli.amazonaws.com/v2/documentation/api/latest/reference/ec2/index.html
