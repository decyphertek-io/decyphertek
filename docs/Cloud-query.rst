Cloud Query
=====

     Cloud Query is a simple CLI tool that can query your cloud infrastrucure as a database to ensure compliance.  

.. code-block:: console

  ###CloudQuery - Install####
  $ curl -L https://github.com/cloudquery/cloudquery/releases/latest/download/cloudquery_linux_x86_64 -o cloudquery 
  $ chmod a+x cloudquery 
  $ cloudquery init aws 
  # cloudquery init aws gcp  
  # This will generate a config containing aws and gcp providers 
  # cloudquery init --help # Show all possible auto generated configs and flags 
  $ docker run --name cloudquery_postgres -p 5432:5432 -e POSTGRES_PASSWORD=pass -d postgres 
  # Environment Variables 
  $ export AWS_ACCESS_KEY_ID={Your AWS Access Key ID} 
  $ export AWS_SECRET_ACCESS_KEY={Your AWS secret access key} 
  $ export AWS_SESSION_TOKEN={Your AWS session token} 
  # Connect to DB 
  $ psql "postgres://postgres:pass@localhost:5432/postgres?sslmode=disable" 
  # Example Query 
  $ SELECT * FROM aws_elbv2_load_balancers WHERE scheme = 'internet-facing'; 
  # Execute A Policy, CIS 
  $ cloudquery policy run aws//cis_v1.2.0 

  ###References### 
  https://www.cloudquery.io/ 
  https://github.com/cloudquery/cloudquery 
  https://docs.cloudquery.io/docs/getting-started/getting-started-with-aws/ 
