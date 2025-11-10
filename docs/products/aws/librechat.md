LibreChat is an open-source AI chat platform that provides users with a versatile interface for engaging with various AI models. It is enhanced with MeiliSearch for efficient data retrieval and Ollama for advanced conversational capabilities. Additionally, it incorporates robust security features to ensure a safe and secure user experience. [AWS Marketplace: Librechat AI]()

Note:
-----
* Please wait 10-15 minutes for Librechat to be accesible.
* Ollama is off by default and requires a GPU. To activate ollama run the following from terminal:
```
sudo systemctl start ollama
# To make persistent on reboot also run:
sudo systemctl enable ollama
```

SSH Into the server:
--------------------
```
ssh adminotaur@ip-of-server
```

Access The Server:
-------------------------
* Login > https://ip-of-server
* Create a new user to login
* This will redirect to a register page
* Enter your information , then login.

Manage Librechat:
-----------------
* Manage librechat , Meilisearch , and Ollama:
```
# pm2-root manages librechat
sudo systemctl status pm2-root meilisearch ollama
# By default ollama is not running, since it requires a GPU to run efficiently.
# Ollama can be up and running with a simple command. 
sudo systemctl start ollama
sudo systemctl enable ollama
sudo systemctl status ollama
# These same commands can be applied to pm2-root & meilisearch.
```

Librechat configuration update:
-------------------------------
* Any configuration changes to .env or librechat.yaml requires pm2 update for nodejs.
* To simplify this I have an librechat update script, for example:
```
# Lets say you want to add a new Ollama model and its not showing in librechat. We can fix that.
sudo su
cd /root/LibreChat/
# EX: You install ollama codeqwen model 
ollama run codeqwen
# These steps also apply to any changes made in .env for example. 
vim librechat.yaml

  custom:
    - name: "Ollama"
      apiKey: "ollama"
      baseURL: "http://localhost:11434/v1/chat/completions" 
      models:
        default: [
          "llama3.2:1b",
          "codeqwen"
          ]
        fetch: true
      titleConvo: true
      titleModel: "current_model"
      summarize: false
      summaryModel: "current_model"
      forcePrompt: false
      modelDisplayLabel: "Ollama"

# This will stop pm2-root , which manages librechat and save the configuration changes. 
bash /opt/.librechat.yaml
# Wait a few minutes after the script finishes, you should see the changes in .env or librechat.yaml take effect. 
```

Security Features:
------------------
* Auditd - https://decyphertek.readthedocs.io/en/latest/technotes/Auditd/
* OSSEC HIDS - https://decyphertek.readthedocs.io/en/latest/technotes/OSSEC/
* UFW - https://decyphertek.readthedocs.io/en/latest/technotes/UFW/
* Rsyslog - https://www.rsyslog.com/doc/index.html
* Automated Updates - Crontab runs at reboot and at 3am every morning.
* Security Reports:
```
# Daily Security report
sudo cat /var/log/decyphertek/security_report*
```

References:
-----------
* https://www.librechat.ai/
* https://ollama.com/library
* https://www.meilisearch.com/
