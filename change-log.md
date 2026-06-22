---
title: "Change Logs"
description: "Review all release updates, bug fixes, and features added to Razor."
icon: "clock"
---

All notable changes to the **Razor** project will be documented in this file to keep you informed of our continuous improvements.

---

## v2.0.8 (Latest)

<Note>
  This update introduces advanced billing integration via Stripe, a fully featured Developer Admin Control Panel, automated warn decays, server statistics counters, and improved stability through Discord.js sharding.
</Note>

### ✦ Added
- **Developer Admin Panel** — Comprehensive `/admin` control room detailing system diagnostics (RAM usage, WebSocket ping, uptime) and providing remote command reloading.
- **User & Server Blacklists** — Hard blacklist management dashboard to ban users or force the bot to exit specific servers immediately.
- **Dynamic Command & Feature Locking** — Toggles in the admin dashboard to lock specific bot slash commands or dashboard views behind premium subscription plans.
- **Global Broadcast System** — Broadcast custom warning, information, or alert embeds to guild owners or specific system/chat channels directly from the dashboard.
- **Stripe Payments Integration** — Native Stripe checkout sessions and webhooks to automatically generate and grant premium subscription keys to users.
- **Sharded Loader (`load.js`)** — Implemented Discord.js `ShardingManager` for loading the bot stably and preventing startup timeouts on larger setups.
- **Warn Decay Scheduler** — Daily automated warning decay cron job to automatically remove warnings after a configured expiration window.
- **Server Stats Cron** — Optimized background stats counter updating voice channel names representing human members, online status, bot counts, etc., every 5 minutes.

### ◈ Changed
- **Unified Uppercase Environment Variables** — Standardized all config parameters in `.env` to strict uppercase format (e.g. `CLIENT_ID`, `CLIENT_SECRET`, `BOT_TOKEN`, `MONGODB_URL`, `DEVELOPER_ID`, `LICENSE_KEY`).
- **MongoStore Session Storage** — Express dashboard session manager rewritten to store active login sessions in the MongoDB Cluster for cluster-safe persistence.

---

## v2.0.6 (Legacy)

<Note>
  This is a major update focusing on stability, modularity, and introducing new feature systems like the Economy Shop and Web Dashboard extensions.
</Note>

### ✦ Added
- **Logging Search**: Added `/logs search` subcommand to dynamically search through server log history with filters (user, action, category) and pagination.
- **Warn Auto-Punishment**: Enforce automatic timeout, kick, or ban actions when users reach configured warning thresholds.
- **Warn Config**: Detailed `/warnconfig` command added to configure thresholds and decay settings.
- **Role Menus**: Advanced role menus featuring button and dropdown modes accessible via `/reaction-role menu`.
- **Server Stats**: New `/serverstats` command for voice channel counters (members, bots, boosts).
- **Economy Shop**: Full economy system with admin-configurable items, interactive user inventories, and auto-role granting.
- **Enhanced Giveaways**: Added stringent requirements like required roles, enforced voice channels, and booster bonuses.
- **Member Growth Analytics**: Real tracking system with daily database recording and stunning dashboard visualization.
- **Web Dashboard Expansion**: New standalone pages for Join-Ping, Leave handling, and Reaction Roles configuration.

### ◈ Changed
- **Backend Modularity**: Split the monolithic `routes.js` into 19 feature-specific files for unmatched speed.
- **Utilities Structure**: Consolidated the `Utils` folder into `Utilities` for better project organization.
- **Optimized Cooldowns**: Centralized all cooldown logic into a single `CooldownManager` instance to prevent memory leaks.
- **API Security**: Implemented strict rate limiting and global input sanitization across the Dashboard API.

---

## v1.0.1 (Legacy)

<Tip>
  This update introduced our very first interaction structures.
</Tip>

### ✦ Added
- **Economy System Framework**: Initial foundation for currency.
- **Commands**: Rolled out the core economy suite: `/beg`, `/daily`, `/deposit`, `/economy`, `/leaderboard`, `/rank`, `/reset`, `/withdrawl`.

---

## v1.0.0 (Legacy)

- **Initial Release**: The grand launch of the Razor All-in-One Discord Bot.
