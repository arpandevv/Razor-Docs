---
title: "Addons Setup"
description: "Learn how to expand Razor Bot with powerful plugins including the Advanced Anti-Nuke and Playlist Manager addons."
icon: "puzzle-piece"
---

Razor supports optional addons to extend the bot's core functionality. This guide walks you through installing addons and setting up the premium **Advanced Anti-Nuke Addon** and the **Playlist Manager Addon**.

---

## 🛠️ Addon Installation Methods

There are two ways you can install addons to your Razor bot workspace. Choose the method that best fits your development preference.

<Steps>
  <Step title="Option 1: Drag & Drop the Whole Folder (Recommended)">
    This is the cleanest and easiest method. It keeps addon files modular and separated in a dedicated addons directory.
    
    1. Locate the downloaded addon folder (e.g., `Anti-Nuke Addon`).
    2. Drag and drop the **entire folder** into the `Addons/` directory located in the root of your main **Razor** bot files.
    
    ```text
    📦 Razor Bot
     ┣ 📂 Addons
     ┃ ┗ 📂 Anti-Nuke Addon  <-- Placed here!
     ┣ 📂 Commands
     ┣ 📂 Events
     ┗ ...
    ```
  </Step>

  <Step title="Option 2: Drag & Drop Folder Contents (Merge Directories)">
    This method integrates the addon files directly into the bot's core directories.
    
    1. Open the downloaded addon folder.
    2. Drag and drop the individual subfolders (`Commands`, `Dashboard`, `Events`, `Schemas`, `Systems`) directly into the root directory of your main **Razor** bot (`Razor v2.0.8`).
    3. If prompted, select **Merge** or **Replace** files to integrate them cleanly into the matching system paths.
  </Step>
</Steps>

---

## 🛡️ Addon 1: Advanced Anti-Nuke

The **Advanced Anti-Nuke Addon** protects your Discord servers against rogue administrators, compromised accounts, and malicious nukers with **13 dedicated protection modules**.

### ⚠️ Critical Fix Required (`index.js`)

<Warning>
  **Version Constraint**
  
  This manual patch is only required if you are running **Razor v2.0.6 or below**. For **Razor v2.0.7** and **Razor v2.0.8 Beta**, this safeguard is already natively integrated into your core codebase, and you can skip this step.
</Warning>

Because the new `antiNukeSystem.js` loads extremely early in the application lifecycle, you must update your core `index.js` file to prevent the bot from crashing during initialization if you are using an older version:

<Steps>
  <Step title="Locate Systems Loading Block">
    Open your main `index.js` file and search (`Ctrl + F`) for the following loop loading the bot systems:
    ```javascript
    for (const file of systemFiles) {
      const system = require(path.join(systemsPath, file));
      system(client);
      loadedSystemsCount++;
    }
    ```
  </Step>
  
  <Step title="Apply the Safeguard Patch">
    Replace the code block above with the updated version below. This adds a safeguard check to verify that the loaded file exports a function before executing it:
    ```javascript
    for (const file of systemFiles) {
      const system = require(path.join(systemsPath, file));
      if (typeof system === 'function') {
        system(client);
      }
      loadedSystemsCount++;
    }
    ```
  </Step>

  <Step title="Restart the Bot">
    Save the changes and restart the bot process via your terminal:
    ```bash
    node .
    ```
  </Step>
</Steps>

### ⚙️ Anti-Nuke Configuration & Usage

Once the addon is loaded, server owners can fully manage the protection configurations directly from Discord using the `/antinuke` command suite.

#### 🎮 Anti-Nuke Slash Commands

<CardGroup cols={2}>
  <Card title="System Setup" icon="sliders">
    Turn the system on and set your logging channel and action punishment (e.g., Ban, Kick, Quarantine, Timeout).
    ```text
    /antinuke setup log_channel:#security-logs punishment:Ban
    ```
  </Card>
  <Card title="Enable Protections" icon="shield-halved">
    Toggle specific modules. There are 13 protection modules available (e.g., Anti Channel Delete).
    ```text
    /antinuke enable protection:Anti Channel Delete
    ```
  </Card>
  <Card title="Configure Thresholds" icon="clock">
    Set how many actions trigger a punishment.
    ```text
    /antinuke threshold protection:Anti Channel Delete count:3 time_window:10
    ```
  </Card>
  <Card title="Whitelist System" icon="user-check">
    Whitelist trusted administrators, staff, or helper bots so they bypass limitations.
    ```text
    /antinuke whitelist add user_or_bot:@trusted_admin
    ```
  </Card>
</CardGroup>

<Tip>
  Use `/antinuke status` to get a beautiful, interactive visual grid listing all active protections, current threshold configurations, and whitelist status on your server!
</Tip>

#### 📦 13 Protection Modules Covered

<AccordionGroup>
  <Accordion title="Structure Protections" icon="folder-tree">
    - **Anti Channel Delete/Create** — Blocks rogue channel deletions and spawns.
    - **Role Delete/Create** — Prevents mass deleting or creating roles to bypass hierarchy.
    - **Emoji Delete** — Shields custom server emojis from deletion.
  </Accordion>
  <Accordion title="Member & Moderation Protections" icon="user-shield">
    - **Bans & Kicks Tracking** — Halts rapid bans/kicks performed by compromised staff accounts.
    - **Pruning Prevention** — Intercepts and stops member list pruning actions.
    - **Unapproved Bot Adds** — Immediately bans/kicks any unverified bots added without approval.
  </Accordion>
  <Accordion title="Webhook & Spam Protections" icon="bolt">
    - **Webhook Create/Delete** — Prevents rogue webhooks from being created to bypass channel security.
    - **@Everyone/@Here Mention Spam** — Automatically silences and punishes users spamming global mentions.
    - **Guild Updates** — Reverts unapproved server name, description, banner, or vanity URL changes.
  </Accordion>
</AccordionGroup>

---

## 🎵 Addon 2: Playlist Manager

The **Playlist Addon** allows users to create, delete, share, and manage custom music playlists stored directly in your MongoDB database, loading them dynamically into the voice queue.

### 🛠️ Installation Instructions

Choose one of the two installation methods below:

<Tabs>
  <Tab title="Option 1: Drag & Drop (Recommended & Easiest)">
    Drag and drop the entire `Playlist Addon` folder inside the `Addons/` folder of your **Razor** bot root directory.
    
    ```text
    📦 Razor Bot
     ┣ 📂 Addons
     ┃ ┗ 📂 Playlist Addon  <-- Placed here!
     ┣ 📂 Commands
     ┣ 📂 Events
     ┗ ...
    ```
    
    <Note>
      This is the easiest approach because the addon code natively looks for the database schema in the `Addons/Playlist Addon/Schemas/` directory out-of-the-box.
    </Note>
  </Tab>

  <Tab title="Option 2: Merge Directories (Requires Path Modification)">
    1. Drag and drop the `Commands/Playlist` folder and the `Schemas/Playlist.js` file into their matching directories in the **Razor** root.
    2. Because the addon looks for its schema inside the `Addons/Playlist Addon` directory by default, you must update the database schema imports.
    3. Open `Commands/Playlist/playlist.js` and locate lines 3 and 6:
       ```javascript
       const db = require(path.join(process.cwd(), "Addons", "Playlist Addon", "Schemas", "Playlist.js"));
       // ...
       const Playlist = require(path.join(process.cwd(), "Addons", "Playlist Addon", "Schemas", "Playlist.js"));
       ```
    4. Replace both paths to point to the root schemas directory relatively:
       ```javascript
       const db = require("../../Schemas/Playlist.js");
       const Playlist = require("../../Schemas/Playlist.js");
       ```
  </Tab>
</Tabs>

### ⚙️ Playlist Usage & Commands

Once the addon is loaded, users can manage their private playlists using the `/playlist` slash command suite.

#### 🎮 Playlist Command Suite

<CardGroup cols={2}>
  <Card title="Playlist Creation" icon="plus">
    Create a new custom playlist (maximum of 10 playlists per user, names capped at 10 characters).
    ```text
    /playlist create name:myfavs
    ```
  </Card>
  <Card title="Save Current Track" icon="music">
    Save the song currently playing in the voice channel directly to your playlist.
    ```text
    /playlist addcurrent playlist_name:myfavs
    ```
  </Card>
  <Card title="Save Entire Queue" icon="list-music">
    Append all songs currently in the voice channel's queue to your custom playlist.
    ```text
    /playlist addqueue playlist_name:myfavs
    ```
  </Card>
  <Card title="Search & Add Tracks" icon="magnifying-glass">
    Search for a song title or URL and select one from the top 5 results to add.
    ```text
    /playlist addtrack playlist_name:myfavs track_name:Lofi Hip Hop
    ```
  </Card>
  <Card title="Load Playlist to Queue" icon="play">
    Join a voice channel and load all tracks from your custom playlist directly into the active queue.
    ```text
    /playlist load playlist_name:myfavs
    ```
  </Card>
  <Card title="Manage Playlists" icon="gear">
    Rename, inspect list of tracks (with interactive buttons for paginated navigation), remove individual tracks, or delete.
    ```text
    /playlist list
    /playlist info playlist_name:myfavs
    /playlist rename old_name:myfavs new_name:gaming
    /playlist removetrack playlist_name:gaming track_number:2
    /playlist delete name:gaming
    ```
  </Card>
</CardGroup>
