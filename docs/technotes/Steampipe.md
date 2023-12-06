SteamPipe is an open source Cli tool. Query the cloud and Enterprise toolsets like a SQL DB and install useful dashboards. 

Linux Install:
--------------

    $ sudo /bin/sh -c "$(curl -fsSL https://raw.githubusercontent.com/turbot/steampipe/main/install.sh)"
    $ steampipe -v
    # Install a Plugin, EX:
    $ steampipe plugin install steampipe
    # Install AWS Plugin
    $ steampipe plugin install aws
    # AWS Plugin configuratiion  - https://hub.steampipe.io/plugins/turbot/aws
    # Make sure AWS CLI is installed and setup. https://aws.amazon.com/cli/

    [account_a]
    aws_access_key_id = AKIA4YFAKEKEYXTDS252
    aws_secret_access_key = SH42YMW5p3EThisIsNotRealzTiEUwXN8BOIOF5J8m
    region = us-west-2

    [account_b]
    aws_access_key_id = AKIA4YFAKEKEYJ7HS98F
    aws_secret_access_key = Apf938vDKd8ThisIsNotRealzTiEUwXj9nKLWP9mg4

    $ sudo vim ~/.steampipe/config/aws.spc

    connection "aws_account_a" {
      plugin  = "aws"
      profile = "account_a"
      regions = ["us-east-1", "us-west-2"]
    }

    connection "aws_account_b" {
      plugin  = "aws"
      profile = "account_b"
      regions = ["ap-southeast-1", "ap-southeast-2"]
    }

    # AWS Query example:

    select
      title,
      create_date,
      mfa_enabled
    from
      aws_iam_user

    # Update all plugins
    $ steampipe plugin update --all
    # Dashboards , EX: https://hub.steampipe.io/mods/turbot/aws_compliance
    $ steampipe plugin update aws
    $ git clone https://github.com/turbot/steampipe-mod-aws-compliance
    $ cd steampipe-mod-aws-compliance
    $ steampipe dashboard 
    # http://localhost:9194
    <OR> 
    $ steampipe check list
    $ steampipe check benchmark.{name_from_list}

Optional: Turbot
-----------------

Turbot utlizes Steampipe , except it provides SaaS option, instead of rolling your own. https://turbot.com/

References:
-----------

https://steampipe.io


