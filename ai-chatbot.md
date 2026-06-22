---
title: "AI Chatbot & Image Gen"
description: "Configure Google Gemini, OpenAI, or Anthropic models and set up automated AI chatting and image creation."
icon: "robot"
---

Razor features a built-in AI module powered by leading large language models (Google Gemini, OpenAI, and Anthropic). It supports two primary systems:
1. **AI Chatbot**: Real-time conversation threads via command or dedicated channel auto-replies.
2. **AI Image Generator**: Generate custom illustrations inside Discord using the `/imagine` command.

---

## 1. 🔑 Obtaining API Keys

To activate the AI functionalities, you must configure the Google Gemini API key.

### Step 1: Generate Google Gemini API Key
1. Visit [Google AI Studio](https://aistudio.google.com/).
2. Log in with your Google account.
3. Click the **Get API Key** button (top left).
4. Click **Create API Key** and select a project.
5. Copy the generated key.

### Step 2: Configure `config.js`
Open `config.js` in the root of your project, find the `APIs` section, and paste your Gemini key:

```javascript
  // APIs
  gemini_api: "PASTE_YOUR_GEMINI_API_KEY_HERE",   // Critical: For AI chat
```

---

## 2. 💬 Setting Up the AI Chatbot

Once the Gemini API key is configured, members can interact with the AI in two ways:

### Method A: Slash Commands
Users can execute the `/ai-config` command followed by their question. The bot will trigger a processing state and reply with the AI's response formatted in a clean embed.

---

## 3. 🎨 AI Image Generation (`/imagine`)

The `/imagine` command allows members to create custom artwork by typing descriptive text prompts:

```text
/imagine prompt:A futuristic cybernetic city under neon rain, detailed, 4k model:Rsn Labs
```

### Retrieving the Image Generation API Key:
Razor uses the **Rsn Labs** API to handle dynamic image generation. Follow these steps to obtain your free API key:

1. **Join the Discord Server** — Join the official [Rsn Labs Discord Server](https://discord.gg/tQtAdqe8).
2. **Locate Bot Commands Channel** — Head over to the [#bot-commands](https://discord.com/channels/1153324895883776002/1164593567600218132) channel.
3. **Register Account** — Run the slash command `/register` with your email and password:
   ```text
   /register email:your_email@example.com password:your_secure_password
   ```
4. **Generate Key** — Execute the slash command `/generate-key` to retrieve your private API key from the **Rsn Labs** bot.
5. **Configure `config.js`** — Copy the API key and paste it into the `imageGenAPI` field in your `config.js`:
   ```javascript
   // APIs
   imageGenAPI: "PASTE_YOUR_RSN_LABS_API_KEY_HERE",
   ```
