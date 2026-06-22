---
title: "Setup Commands"
description: "Configure your server's settings and modules directly inside Discord."
icon: "screwdriver-wrench"
---

<Note>
  Administrators have access to over 20+ dedicated setup commands to totally configure the bot directly inside Discord. These commands override the defaults and write to your MongoDB database.
</Note>

---

## 🛠️ Essential Setups

| Command | Description |
| :--- | :--- |
| `[ /serverstats ]` | Maps interactive voice channels showing live member count, bots, boosts, and roles. |
| `[ /logging ]` | Creates a comprehensive audit log channel. Subcommands: `/logs search`. |
| `[ /auto-role ]` | Assigns an instant Discord role the moment a user joins the server. |
| `[ /welcome ]` | Configures the visual welcome poster and greeting channel. |
| `[ /leave ]` | Configures the farewell message and tracking channel. |
| `[ /join-ping ]` | Immediately ghosts-pings an active role or user alongside new member joins to capture attention. |

---

## 🛡️ Moderation & Enforcement Setups

| Command | Description |
| :--- | :--- |
| `[ /warnconfig ]` | Extremely powerful! Sets automatic punishments (timeout/ban) based on a threshold limit of warnings. |
| `[ /autoDelete ]` | Maps a channel to immediately delete specific types of messages (bot commands, links, bad words). |
| `[ /anti-ghost-ping ]` | Toggles the detection and public shaming of users who tag someone and immediately delete the message. |
| `[ /modmail ]` | Maps an internal modmail delivery system so server members can quietly DM the bot to reach staff. |
| `[ /verification ]` | Sets up a secure captcha/button wall that members must pass before seeing the main server channels. |

---

## 🎭 Interactive & Support Modules

| Command | Description |
| :--- | :--- |
| `[ /reaction-role menu ]` | Creates advanced dropdowns or button menus for assigning up to 25 self-roles dynamically. |
| `[ /ticket ]` | Builds a premium interactive ticket UI. Options for claims, transcripts, and multiple department categories. |
| `[ /suggestion ]` | Configures a clean channel where members submit formally formatted suggestions with live upvote tracking. |
| `[ /stickymsg ]` | Anchors an extremely important message dynamically to the bottom of the active chat channel. |
| `[ /leveling ]` | Configures XP multipliers, custom level-up messages, and toggles voice XP recording. |
| `[ /levelroles ]` | Links a Discord role to a specific level (e.g., reaching Level 50 auto-grants `@Veteran`). |

<Tip>
  Don't forget, most of these setup configurations can also be modified instantly using the **Web Dashboard interface**!
</Tip>
