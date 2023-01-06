OpenAI
======

Open Source Artificial Intelligence. 

QuickStart
----------

    $ sudo apt update && sudo apt upgrade -y
    $ sudo su -c "curl -fsSL https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add -"
    $ curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - 
    $ sudo apt-get install -y nodejs 
    $ git clone https://github.com/openai/openai-quickstart-node.git
    # Get API key
    # https://beta.openai.com/signup
    $ npm install
    $ npm run dev
    # http://localhost:3000/

References
-----------

    https://beta.openai.com/docs/quickstart/build-your-application