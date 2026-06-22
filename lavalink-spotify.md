---
title: "Lavalink & Spotify Setup"
description: "Connect your bot to Lavalink nodes and configure Spotify integration for high-fidelity music playback."
icon: "music"
---

Razor features a high-fidelity, sharded music system powered by **Lavalink** and **Kazagumo**. It supports searching, queueing, and playing music tracks from **Spotify**, YouTube, and Soundcloud.

To enable the music system, you must configure a working Lavalink node and provide Spotify API credentials.

---

## 1. 🎵 Lavalink Node Configuration

Lavalink is an external audio standalone provider that handles music voice connections, taking the CPU load off your main bot process.

### Configuration Fields
Open your `config.js` file and locate the `lavalink` object:

```javascript
  // Lavalink server configuration
  lavalink: {
    name: "Razor Node",
    url: "sg1-nodelink.nyxbot.app:3000", // Host address and port of the node
    auth: "nyxbot.app/support",         // Connection password/authorization
    secure: false,                      // Set to true if connection uses SSL (wss://)
  },
```

### Finding Lavalink Nodes
If the default node is offline, you have two options:
1. **Use Public Nodes**: You can find list of free, community-run public Lavalink nodes from sites like [lavalink.darrennathanael.com](https://lavalink.darrennathanael.com/) or Discord lists.
2. **Self-Host Lavalink**: Deploy your own private node on your VPS using Java and the Lavalink `.jar` server. This guarantees 100% uptime and no sharing of bandwidth.

---

## 2. 🔑 Spotify API Integration

Since Spotify doesn't allow direct audio streaming, Razor reads Spotify playlists, albums, or track metadata via the Spotify API, then dynamically searches and plays the matching audio stream.

Follow these steps to generate your Spotify developer credentials:

### Step 1: Create a Spotify Developer App
1. Go to the [Spotify Developer Dashboard](https://developer.spotify.com/dashboard).
2. Log in with your standard Spotify account.
3. Click the **Create App** button.
4. Fill in the application details:
   - **App Name**: `Razor Music Bot`
   - **App Description**: `Music metadata integration for Razor Bot.`
   - **Redirect URI**: `http://localhost:5500/callback` (you can put any valid URL here).
5. Accept the terms and click **Save**.

### Step 2: Retrieve Credentials
1. Inside your newly created app page, click on **Settings** (top right).
2. Look for the **Client ID** and click **Show client secret** to display the **Client Secret**.
3. Copy both values.

### Step 3: Insert into `config.js`
Open `config.js` and locate the API settings. Replace the empty strings with your credentials:

```javascript
  // APIs
  SpotifyClientID: "PASTE_YOUR_SPOTIFY_CLIENT_ID_HERE",
  SpotifyClientSecret: "PASTE_YOUR_SPOTIFY_CLIENT_SECRET_HERE",
```

---

## 3. 🚀 Verifying the Music System

Once you restart the bot, check your console boot logs. If the connection is successful, you will see the following confirmation log:

```text
[SUCCESS] Lavalink Razor Node: Ready!
```

If you see connection error logs, double-check your node port, host address, and authorization password in `config.js`.
