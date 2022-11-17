AWS CLI
========

AWS CLI provides infrastructure as code methodology. 

Install
-------

     # Linux
     $ curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
     $ unzip awscliv2.zip
     # This saves aws creds under root user.
     # Beneficial if you have ansible installed via Linux at /etc/ansible/ 
     $ sudo ./aws/install
     $ sudo aws configure
     # Mac
     $ python3 -m pip install --user awscli

Basic Commands
--------------

    # List EC2 instances
    $ aws ec2 describe-instances --query 'Reservations[].Instances[].[State.Name, InstanceId, ImageId, InstanceType, PublicIpAddress, SubnetId, VpcId,Tags[?Key==`Name`]| [0].Value]' --output table
    # Manage Ec2 state
    $ aws ec2 start-instances --instance-ids i-0000000000000
    $ aws ec2 stop-instances --instance-ids i-0000000000000
    $ aws ec2 terminate-instances --instance-ids i-0000000000000
    # Create an AMI from an instance ID
    $ aws ec2 create-image \
    --instance-id i-1234567890abcdef0 \
    --name "My server" \
    --description "An AMI for my server"

References
----------

    https://docs.aws.amazon.com/cli/latest/