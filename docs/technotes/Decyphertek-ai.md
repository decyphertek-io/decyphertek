# DecypherTek AI

Linux based decyphertek.ai chat. Modular stores: mcp ; agent ; app , to customize AI . 

## Features

- **AI Chat** - Generalized / Specialized AI chat.
- **Rag Chat** - Upload docs and inquire about them. 
- **App Store** - Python apps.
 **Agent Store** - Manage the AI personality.
- **MCP Servers** - Modular AI Skills.

## Quick Start
```
curl -fsSL https://raw.githubusercontent.com/decyphertek-io/decyphertek-ai/main/install.sh | sudo bash

* Setup > Create creds > add settings > AI Admin Chat . 

# Decyphertek AI working directory:
cd ~/.decyphertek-ai/

# Optional: Application desktop icon works with xfce. May need to edit.
vim /usr/share/applications/decyphertek-ai.desktop

# Debugging:
/opt/decyphertak.ai 
* This will run the app and show terminal output for debugging issues.
* Run this from chat to help debug.
sudo systemctl status mcp
sudo systemctl status agent
sudo systemctl status app
healthcheck-agent
```
