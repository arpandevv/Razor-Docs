---
title: "Moderation Commands"
description: "Enterprise-grade tools to secure and manage your server."
icon: "gavel"
---

<Note>
  Razor's moderation suite provides enterprise-grade tools to secure your server. All these commands require specific administrative or moderation Discord permissions to execute.
</Note>

---

## 🚫 Primary Enforcement

| Command | Description | Required Permission |
| :--- | :--- | :--- |
| `[ /ban ]` | Permanently bans a user from the server with an optional reason. | `Ban Members` |
| `[ /unban ]` | Revokes a ban using the user's ID. | `Ban Members` |
| `[ /mass-unban ]` | Instantly unbans every currently banned user. | `Administrator` |
| `[ /kick ]` | Removes a user from the server. They can rejoin if they have a new invite. | `Kick Members` |
| `[ /kickall ]` | Kicks all members holding a specific role. | `Administrator` |

---

## ⏳ Temporary Actions

| Command | Description | Required Permission |
| :--- | :--- | :--- |
| `[ /timeout ]` | Mutes a user from chatting or joining voice for a specified duration (e.g., `10m`, `1h`). | `Moderate Members` |
| `[ /untimeout ]` | Removes an active timeout from a user instantly. | `Moderate Members` |
| `[ /warn ]` | Issues a formal warning. Reaching the threshold triggers Auto-Punishment (kick/ban). | `Kick Members` |

---

## 🧹 Channel & Chat Management

| Command | Description | Required Permission |
| :--- | :--- | :--- |
| `[ /purge ]` | Deletes a bulk amount of messages (up to 100 at a time). | `Manage Messages` |
| `[ /lockdown ]` | Locks a channel, preventing standard members from sending messages. | `Manage Channels` |
| `[ /slowmode ]` | Sets the rate limit (slowmode) for the current channel. | `Manage Channels` |
| `[ /channel ]` | View detailed analytics and configuration data for the current channel. | `Manage Channels` |

---

## 🎭 Role Management

| Command | Description | Required Permission |
| :--- | :--- | :--- |
| `[ /role ]` | Quickly adds or removes a specific role from a target user. | `Manage Roles` |
| `[ /roleall ]` | Distributes a specific role to every single human member in the server. | `Administrator` |
| `[ /unroleall ]` | Strips a specific role from everyone who currently holds it. | `Administrator` |

<Warning>
  Commands like `/mass-unban` and `/roleall` are extremely powerful action scripts. Only use them when absolutely necessary.
</Warning>
