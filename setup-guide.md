---
title: "Bot Setup Guide"
description: "Follow this comprehensive, step-by-step master guide to compile, configure, and launch Razor."
icon: "book-open"
---

Follow this comprehensive, step-by-step master guide to compile, configure, and launch your very own instance of Razor from the source code.

---

## 1. 📦 Prerequisites

<Note>
  Before you begin, verify that your environment meets these critical baseline requirements. **Do not skip these.**
</Note>

- **[Node.js v24 LTS (or higher)](https://nodejs.org/)** — Required runtime environment.
- **[Git / Source Control](https://git-scm.com/downloads/win)** — Highly recommended for code maintenance.
- **[Visual Studio Code](https://code.visualstudio.com/)** — Industry standard code editor.
- **[MongoDB Atlas](https://www.mongodb.com/cloud/atlas)** — Free cloud database cluster for storing bot data.
- **[Discord Developer Portal](https://discord.com/developers/applications)** — To generate your `Bot Token` and `Client ID`.

---

## 2. 📥 Environment Preparation

### Installing Node.js
1. Download the **LTS** (Long Term Support) installer from [nodejs.org](https://nodejs.org/).
2. Run the executable. When prompted, ensure that **"npm package manager"** is selected for installation.
3. Once completed, verify your installation by opening your terminal (or command prompt) and executing:
   ```bash
   node -v
   npm -v
   ```
   > Both commands should return version numbers.

### Extracting the Razor Source
1. Locate your downloaded **Razor Source Code** `.zip` file from your purchase.
2. Extract the archive contents into a dedicated project directory (e.g., `C:\RazorBot`).
3. Open this folder within **Visual Studio Code**.

---

## 3. ⚙️ Dependency Compilation

To build the bot's architecture, you must install the required Node.js packages.

Open an integrated terminal right inside Visual Studio Code (`Ctrl + ~` or `Terminal -> New Terminal`) and run:

```bash
npm install
```

<Warning>
  **Resolving Conflicts**
  
  If `npm` encounters peer dependency conflicts or permissions issues, forcefully resolve them by using:
  `npm install --force`
</Warning>

---

## 4. 📝 Core Configuration

Razor requires two primary configuration files to boot successfully.

### System Configuration (`config.js`)
Locate `config.js` in the root directory. This dictates global variables:
```javascript
module.exports = {
  status: "dnd",
  embedColor: "#fe394a",
  noPermsMessage: `You **do not** have the permission to do that!`,

  // Dashboard Configuration
  dashboard: {
    enabled: true,
    port: 5500,
    domain: "http://localhost:5500",
    sessionSecret: "razor-super-secret-key-change-this",
  },
  // Additional API, Lavalink, and Logging settings follow...
};
```

### Environment Variables (`.env`)
1. In the root directory, locate the file named `.env.example`.
2. Rename this file simply to `.env` (ensure there is no file extension like `.txt`).
3. Populate it with your sensitive credentials strictly:
```env
# BOT CONFIGURATION
CLIENT_ID=YOUR_BOT_APPLICATION_ID
CLIENT_SECRET=YOUR_DISCORD_CLIENT_SECRET
BOT_TOKEN=YOUR_SECURE_BOT_TOKEN
MONGODB_URL=mongodb+srv://user:pass@cluster.mongodb.net/?retryWrites=true&w=majority

# DEVELOPER SETTINGS
DEVELOPER_ID=YOUR_DISCORD_USER_ID

# LICENSE SETTINGS
LICENSE_KEY=YOUR_RAZOR_LICENSE_KEY
```

<Warning>
  **Security Alert**
  
  Never share your `.env` file or commit it to a public GitHub repository.
</Warning>

---

## 5. 🚀 Launch Sequence

With dependencies installed and configurations saved, you are ready for ignition.

Run the launch command directly in your terminal:
```bash
npm start
```

This launches the sharding system loader (`load.js`), which initializes the Discord.js `ShardingManager` and boots the core code (`index.js`) safely within separate shards for maximum speed and stability.

Watch the terminal. Once you see the successful initialization logs, **Razor is online**.
