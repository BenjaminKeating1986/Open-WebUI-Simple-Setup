# 🚀 Open WebUI & TTS Deployment on Windows (Docker Guide)

This guide walks you through deploying **Open WebUI** and **Edge TTS** on Windows using Docker.  

---

## 🖥️ 1. Prerequisites
- Install **Docker Desktop for Windows**: [Download here](https://www.docker.com/products/docker-desktop)
- Ensure **WSL2 backend** is enabled
- Familiarity with using **Command Prompt / PowerShell**

---

## 🌐 2. Deploying Open WebUI

Run the following command in **Command Prompt** or **PowerShell**:

```bash
docker run -d -p 3023:8080 -v C:\Docker\WebUI2:/app/backend/data --name open-webui2 ghcr.io/open-webui/open-webui:main
```

### Notes:
- `3023` is the **external port** for accessing Open WebUI → change this if needed.  
- `8080` must **remain unchanged** (internal container port).  
- `C:\Docker\WebUI2` is where persistent data is stored. You can modify that path.  

After running the command, open your browser and go to:  
👉 **http://localhost:3023**

---

## 🔊 3. Deploying Edge TTS (Text-to-Speech)

### Step 1. Create a folder  
For example: `C:\Docker\EdgeTTS`

### Step 2. Create a `.env` file inside that folder with the following values:

```
API_KEY=pass123
PORT=5050
DEFAULT_VOICE=en-US-AvaNeural
DEFAULT_RESPONSE_FORMAT=mp3
DEFAULT_SPEED=1.0
DEFAULT_LANGUAGE=en-US
REQUIRE_API_KEY=True
REMOVE_FILTER=False
EXPAND_API=True
DETAILED_ERROR_LOGGING=True
```

Modify values as needed (e.g., change default voice, port, or API key).

---

### Step 3. Deploy the container  
Navigate to the folder in **Command Prompt**:

```bash
cd C:\Docker\EdgeTTS
```

Then run:

```bash
docker run -d -p 5050:5050 --env-file .env --name edge-tts travisvn/openai-edge-tts:latest
```

### Notes:
- Edge TTS is now running on **port 5050**.  
- This is an **API-only** service, but it is OpenAI-compatible.  

👉 Test voices here: [https://tts.travisvn.com](https://tts.travisvn.com)

---

## 🔍 4. Search Engine Setup  

For connecting and configuring the search engine module, please follow this detailed video guide:  
🎥 [YouTube Setup Video](https://www.youtube.com/watch?v=O5b9FvHYjqc)

---
