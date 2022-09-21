Keycloak
=====

Open Source Identity and Access Management that includes SSO, identity brokering, and user federation. 


Install
-------

     # Install OpenJDK  
     $ sudo apt install default-jre  
     # Download and Run Keycloak 
     $ wget https://github.com/keycloak/keycloak/releases/download/17.0.1/keycloak-17.0.1.zip 
     $ unzip keycloak-17.0.1.zip 
     $ cd keycloak-17.0.1 
     $ bin/kc.sh start-dev &  
     $ ssh -L 9999:localhost:8080 user@ip-of-server 
     # Create Admin user- http://localhost:9999/ 
     # AWS Security group allow inbound 8080  
     # Login: http://ip-of-server:8080 

     # Create a Realm 
     > Admin Console > Master > Create Realm 
     # Create A User 
     > Admin Console > Users > Add User > Fill in Data >  Save 
     # Enable SSL while communicating, doesn't actually encrypt the web page you access? 
     > Admin Console > Realm Setting > Login > Require SSL > ALL Requests >  
     # Secure your app 
     > Admin Console > Clients > FIll in data: > save 
     Client ID: myclient 
     Client Protocol: openid-connect 
     Root URL: https://www.keycloak.org/app/ 

     # Using Keycloak with Jupyterhub# 
     # Create Client ID 
     > Admin Console > Clients > Create > Fill out Form > Save 
     > ClientID > Settings > Access Type = Confidential 
     > ClientID > Settings > Valid Redirect URIs: 
     http://127.0.0.1:8001 
     http://127.0.0.1:8081/* 
     http://127.0.0.1:443/hub/home 
     http://127.0.0.1:443/*  
     > Admin Console > Clients > Client Name > Credentials Tab > Copy secret  
     # Add to jupyterhub_cofig.py 

     from oauthenticator.generic import GenericOAuthenticator 
     c.JupyterHub.authenticator_class = GenericOAuthenticator 
     c.GenericOAuthenticator.client_id = 'Jupyterhub' 
     c.GenericOAuthenticator.client_secret = 'client-secret' 
     c.GenericOAuthenticator.token_url = 'http://0.0.0.0:8080/auth/realms/keycloak-demo/protocol/openid-connect/token' 
     c.GenericOAuthenticator.userdata_url = 'http://0.0.0.0:8080/auth/realms/keycloak-demo/protocol/openid-connect/userinfo' 
     c.GenericOAuthenticator.userdata_params = {'state': 'state'} 
     c.GenericOAuthenticator.username_key = 'preferred_username' 
     c.GenericOAuthenticator.login_service = 'Keycloak' 
     c.GenericOAuthenticator.scope = ['openid', 'profile'] 
     c.JupyterHub.spawner_class = 'jupyterhub.spawner.SimpleLocalProcessSpawner' 

     # You may not have to export these variables, just add them to the config, this looks confusing.  
     export OAUTH2_AUTHORIZE_URL=http://<keycloak-host:port>/auth/realms/keycloak-demo/protocol/openid-connect/authexport OAUTH2_TOKEN_URL=http://<keycloak-  
     host:port/auth/realms/keycloak-demo/protocol/openid-connect/token 
 
     # The Previous instructions will point Jupyterhub to Keycloak, now need to connect Keycloak to Azure  
     > Azure AD > App Registrations > Name & Select single tenant account > save 
     > Azure AD > Select new app made > Configuation & secrets > get client secret  

     # Keycloak settings 
     # Should choose most secure, following instrucitons here.  
     > Admin Console > Identity Providers > Open ID Connect v 1.0 > Add names & save 
     Next > Import External IDP Config >  see the Import from URL field. 
     > Azure AD > App registration > See Endpoints. 

References
-----------

     https://linoxide.com/install-java-ubuntu-20-04/ 
     https://www.keycloak.org/getting-started/getting-started-zip 
     https://www.keycloak.org/docs/latest/server_admin/ 
     https://medium.com/keycloak/secure-jupyterlab-using-keycloak-56e60c369c5f 
     https://dev.to/andremoriya/keycloak-azure-active-directory-4cg4 
