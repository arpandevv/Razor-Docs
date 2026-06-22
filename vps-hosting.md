---
title: "24/7 VPS Hosting (PM2)"
description: "Deploy Razor and its Web Dashboard to a Linux VPS and keep it running 24/7 using PM2."
icon: "server"
---

To keep **Razor** and its **Web Dashboard** online 24/7, you should host them on a Virtual Private Server (VPS) running Linux (e.g., Ubuntu). 

Using a production process manager like **PM2** ensures that if your bot crashes, it will automatically restart instantly, and if the VPS reboots, the bot and docs will spin up automatically.

---

## 1. ⚙️ Initial VPS Preparation

Connect to your VPS via SSH and run the following commands to update system dependencies and install the correct Node.js version.

### Step 1: Update Packages
```bash
sudo apt update && sudo apt upgrade -y
```

### Step 2: Install Node.js v24 (LTS)
Install Node.js utilizing the official NodeSource binaries:

```bash
# Fetch and setup NodeSource v24 repository
curl -fsSL https://deb.nodesource.com/setup_24.x | sudo -E bash -

# Install Node.js
sudo apt install -y nodejs
```

Verify your installation version:
```bash
node -v  # Should be v24.x.x
npm -v   # Should return the npm version
```

### Step 3: Install PM2 Globally
Install the PM2 process manager globally on the system:

```bash
sudo npm install pm2 -g
```

---

## 2. 📂 Project Deployment

1. Transfer your configured **Razor Bot Source Code** and **Razor Docs** folders to your VPS (either using SFTP/FileZilla or by pushing to a private GitHub repository and cloning it).
2. Navigate into the project folder on your VPS:
   ```bash
   cd /path/to/your/RazorBot
   ```
3. Compile all packages:
   ```bash
   npm install
   ```

---

## 3. 🚀 Daemonizing Processes with PM2

Instead of starting with `npm start` (which exits as soon as your SSH console session terminates), we will run the processes in the background using PM2.

### Starting the Razor Bot
Launch the bot loader script and name the process `razor-bot`:

```bash
pm2 start load.js --name "razor-bot"
```



PM2 will automatically read the ecosystem file and start the docs server on port `6488`.

---

## 4. 🔒 Persisting Across Reboots

If your VPS hosting provider does emergency maintenance and reboots your server, PM2 can automatically restore your running processes.

Run the startup generator command:
```bash
pm2 startup
```

PM2 will output a specific command containing env paths. **Copy and paste that command** back into your terminal and run it. 

Finally, save the active process list:
```bash
pm2 save
```

---

## 🛠️ Handy PM2 Commands

Use these commands to monitor and manage your bot and docs processes on the VPS:

| Command | Description |
| :--- | :--- |
| `pm2 status` | View a list of all active processes, their IDs, CPU usage, and memory consumption. |
| `pm2 logs razor-bot` | Open live console logs for the bot (great for debugging errors). |
| `pm2 logs razor-docs` | Open live console logs for the documentation site. |
| `pm2 restart razor-bot` | Reload the bot (use this whenever you update `config.js` or files). |
| `pm2 stop razor-bot` | Temporarily halt the bot process. |
| `pm2 delete razor-bot` | Fully remove the process from PM2's management list. |
