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
    # Update all plugins
    $ steampipe plugin update --all
    # Dashboards , EX: https://hub.steampipe.io/mods/turbot/aws_compliance
    $ steampipe plugin update aws
    $ git clone https://github.com/turbot/steampipe-mod-aws-compliance
    $ cd steampipe-mod-aws-compliance
    $ steampipe dashboard <OR> steampipe check list <OR> steampipe check benchmark.{name_from_list}

Optional: Turbot
-----------------

Turbot utlizes Steampipe , except it provides SaaS option, instead of rolling your own. https://turbot.com/

References:
-----------

https://steampipe.io


