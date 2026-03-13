# 🦞 OpenClaw AI Bot — Telegram + HuggingFace Integration

<p align="center">
  <img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExNmMxZXBlb2Q2eGV4NjgydnUxbDk3NmtoYm85ZnZpZ2FwaWRrdjA5YyZlcD12MV9naWZzX3NlYXJjaCZjdD1n/TB2yb59rDtonIFNLy7/giphy.gif" width="600" alt="AI Bot Banner"/>
</p>

> A personal AI assistant running 24/7 on Telegram, powered by OpenClaw, HuggingFace, and OpenAI integrations — built and deployed on Windows.

---

## 📌 Project Overview

This project sets up a fully functional **AI agent on Telegram** using:

- **[OpenClaw](https://openclaw.ai)** — the AI agent framework that connects everything
- **[HuggingFace](https://huggingface.co)** — free AI model API (GLM-4.7-Flash)
- **[OpenAI Whisper](https://openai.com)** — audio transcription
- **[Telegram Bot API](https://core.telegram.org/bots)** — messaging interface
- **Windows Task Scheduler** — keeps the bot running 24/7

---
<div align="center">

[![Telegram](https://img.shields.io/badge/Telegram-2CA5E0?style=for-the-badge&logo=telegram&logoColor=white)](https://t.me/AKS_OPENCLAW_AI_BOT)
[![HuggingFace](https://img.shields.io/badge/HuggingFace-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)](https://huggingface.co)
[![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white)](https://openai.com)
[![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)](https://nodejs.org)
[![Windows](https://img.shields.io/badge/Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white)](https://microsoft.com)

</div>

## 🏗️ Architecture

```
You (Telegram) ──► Telegram Bot (@AKS_OPENCLAW_AI_BOT)
                          │
                          ▼
                   OpenClaw Gateway
                   (localhost:18789)
                          │
                          ▼
               HuggingFace AI Model
               (zai-org/GLM-4.7-Flash)
                          │
                          ▼
              Response sent back to Telegram
```

---

## ⚙️ Tech Stack

| Component | Tool | Purpose |
|-----------|------|---------|
| Agent Framework | OpenClaw v2026.3.8 | Core AI agent runtime |
| AI Model | HuggingFace GLM-4.7-Flash | Free LLM inference |
| Audio Transcription | OpenAI Whisper API | Voice message processing |
| Image Generation | OpenAI DALL-E | Image creation |
| Messaging | Telegram Bot API | User interface |
| Runtime | Node.js v22 on Windows | Server environment |
| Scheduler | Windows Task Scheduler | 24/7 uptime |

---

## 🚀 Setup Guide

### Prerequisites

- Windows 10/11
- Node.js v18+ (v22 recommended)
- Telegram account
- HuggingFace account (free)

### 1. Install OpenClaw

```powershell
# Run PowerShell as Administrator
irm https://openclaw.ai/install.ps1 | iex
```

### 2. Create Telegram Bot

1. Open Telegram → search `@BotFather`
2. Send `/newbot`
3. Follow prompts → copy the **bot token**

### 3. Configure OpenClaw

Edit `C:\Users\<YourName>\.openclaw\openclaw.json`:

```json
{
  "agents": {
    "defaults": {
      "model": {
        "primary": "huggingface/zai-org/GLM-4.7-Flash"
      }
    }
  },
  "tools": {
    "profile": "messaging"
  },
  "session": {
    "dmScope": "per-channel-peer"
  },
  "channels": {
    "telegram": {
      "enabled": true,
      "dmPolicy": "allowlist",
      "botToken": "YOUR_BOT_TOKEN",
      "allowFrom": ["YOUR_TELEGRAM_CHAT_ID"],
      "streaming": "partial"
    }
  }
}
```

### 4. Set HuggingFace API Key

```powershell
openclaw models set huggingface/zai-org/GLM-4.7-Flash
openclaw models auth paste-token --provider huggingface
# Paste your HuggingFace token when prompted
```

### 5. Set OpenAI API Key (for Whisper & Image Gen)

```powershell
openclaw models auth paste-token --provider openai
# Paste your OpenAI API key when prompted
```
### 6. Note
- Enter API_KEY in openclaw.json wherever said 
### 7. Start the Gateway

```powershell
openclaw gateway start
```

For 24/7 operation, the gateway runs as a **Windows Scheduled Task** automatically.

---

## 🔧 Key Commands

```powershell
openclaw gateway start       # Start the bot
openclaw gateway stop        # Stop the bot
openclaw logs --follow       # View live logs
openclaw models list         # See configured models
openclaw doctor              # Diagnose issues
```

---

## 🎯 Features

- ✅ **AI Chat** — Ask anything via Telegram
- ✅ **Web Search** — Real-time internet search
- ✅ **Session Memory** — Remembers conversation context
- ✅ **Audio Transcription** — Send voice messages, get text back
- ✅ **Image Generation** — Generate images via OpenAI
- ✅ **Skills Marketplace** — Install skills from clawhub.com
- ✅ **24/7 Uptime** — Runs as Windows background service
- 🔄 **LinkedIn Automation** — In progress via linkedin-automation skill

---

## 🛠️ Skills Installed

| Skill | Purpose |
|-------|---------|
| `openai-whisper-api` | Audio transcription |
| `openai-image-gen` | Image generation |
| `session-memory` | Conversation memory |
| `command-logger` | Command logging |

---

## 📁 Project Structure

```
C:\Users\<Name>\.openclaw\
├── openclaw.json              # Main config
├── agents\
│   └── main\
│       └── agent\
│           └── auth-profiles.json  # API keys store
├── workspace\                 # Agent workspace
└── canvas\                    # Dashboard assets
```

---

## 🔑 Environment Variables / API Keys Needed

| Service | Where to Get | Cost |
|---------|-------------|------|
| HuggingFace Token | huggingface.co/settings/tokens | Free |
| Telegram Bot Token | @BotFather on Telegram | Free |
| OpenAI API Key | platform.openai.com/api-keys | Free |

> ⚠️ **Never commit API keys to GitHub.** Use `.gitignore` or environment variables.

---

## 🐛 Troubleshooting

| Error | Fix |
|-------|-----|
| `Gateway not reachable` | Run `openclaw doctor` then `openclaw gateway start` |
| `Unknown model` | Run `openclaw models set <model-id>` and restart gateway |
| `422 status code` | Wrong tools profile — set `"profile": "messaging"` in config |
| `403 bot can't initiate` | User must message the bot first on Telegram |
| `API rate limit` | Switch provider or wait for daily reset |

---

## 📚 Resources

- [OpenClaw Documentation](https://openclaw.ai/docs)
- [HuggingFace Models](https://huggingface.co/models)
- [ClaWHub Skills Marketplace](https://clawhub.com)
- [Telegram Bot API](https://core.telegram.org/bots/api)

---

## 👤 Author

**Anubhav Kumar Srivastava**  
Built as a personal AI automation project — integrating free AI APIs with Telegram for 24/7 assistant functionality.

---

<p align="center">
  <img src="https://media.giphy.com/media/v1.Y2lkPWVjZjA1ZTQ3ZXV5ajk3dW9iMXJreDZicHllenl1OTBvdjR0cjg3ajd6ODM1aW53biZlcD12MV9naWZzX3NlYXJjaCZjdD1n/jojqsdjvhtBy6YB36f/giphy.gif" width="400" alt="Footer"/>
</p>

<p align="center">
  Made with 🦞 OpenClaw + ❤️ persistence
</p>
