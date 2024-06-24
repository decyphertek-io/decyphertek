AutoGPT
========

AutoGPT utilizes openAI Chatgpt API and extends its capabilites.

Linux Install
-----------

    git clone -b stable https://github.com/Significant-Gravitas/Auto-GPT.git
    cd Auto-GPT
    mv .env.template .env
    vim .env
    OPENAPI Key = your api key
    sudo pip3 install -r requirements.txt
    sudo python3 -m autogpt 
    # Optional: Runs nonstop to solve the problem. 
    sudo python3 -m autogpt --continuous 
    # Optional: Text to speech. Still troubleshooting Elevenlabs TTS API . 
    sudo python3 -m autogpt --speak 

References
-----------

    https://github.com/Significant-Gravitas/Auto-GPT
    https://significant-gravitas.github.io/Auto-GPT/setup/