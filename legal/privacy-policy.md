---
title: "Privacy Policy"
description: "Privacy policy and data collection rules for Razor."
icon: "user-shield"
---

**Last Updated**: 06/22/2026

### 1. 📖 Introduction
This Privacy Policy outlines how Razor Development ("**we**," "**our**," or "**us**") collects, uses, discloses, and protects information collected from users ("you" or "your") of the Discord bot, **Razor** (the "Bot"). By using the Bot and its Web Dashboard, you strictly agree to the collection and use of information in accordance with this Privacy Policy.

---

### 2. 🗃️ Information We Collect

#### User Data
- **User ID:** We collect and securely store your Discord User ID to identify you within the bot's core functionalities (like Economy and Leveling).
- **Server ID:** We collect and store Server IDs where the bot is added to manage server-specific settings and Dashboard configurations.
- **Message Content:** We may *temporarily* collect message content strictly when commands are explicitly issued to the bot to process your immediate requests.

#### Dashboard Authentication & Sessions
- **Discord OAuth2 strategy:** Signing into the Web Dashboard requests `identify` and `guilds` scopes. This collects your Discord username, user ID, avatar URL, and the list of servers you manage to verify access.
- **Cookies & Session Tokens:** We use cookies to persist your dashboard login state. These session states are stored safely inside our MongoDB Cluster (`MongoStore`) for safe data caching.

#### Stripe Billing Info
- If you check out via the Web Dashboard, **Stripe** collects billing details, email, card information, and transaction histories. The bot database does not store raw credit card details, but receives and stores webhook events with plan metadata to toggle your premium status.

#### Command Logging
- All slash commands executed are logged to MongoDB, capturing the User ID, Server ID, command inputs, channel details, and execution timestamps for audit purposes.

---

### 3. 🎯 How We Use Your Information

<Info>
  **Core Utilization**
  
  We only process your data to keep Razor functional and secure.
</Info>

We use the information we collect for the following operational purposes:
1. To stably provide, operate, and maintain the Bot’s and Dashboard's functionalities.
2. To organically improve, personalize, and expand the Bot's features.
3. To understand and structurally analyze how you use the Bot.
4. To develop entirely new features, services, and functionalities.
5. To automatically communicate with you directly (or via the server) regarding vital updates.

---

### 4. 🤝 Data Sharing and Disclosure

<Check>
  **No Selling Data**
  
  We **do not sell, trade, or otherwise transfer** your personal information to third parties.
</Check>

Exemptions to this rule:
- **Service Providers:** We may share securely hashed information with incredibly trusted third-party service providers (like Stripe for billing and MongoDB Atlas for database hosting) who assist us in operating the Bot's backend.
- **Legal Requirements:** We may disclose your information if legally required to do so by a court of law or public authorities.

---

### 5. ⏳ Data Retention
We will strictly retain your information only for as long as functionally necessary to fulfill the purposes outlined in this Privacy Policy. We will purge tracking data continually.

### 6. 🛡️ Data Security
We take vast, enterprise-grade measures to protect the information we collect from unauthorized access, use, or disclosure. 

<Warning>
  **Security Disclaimer**
  
  However, no method of transmission over the Internet or method of electronic storage is 100% secure, and we cannot guarantee its absolute perfection.
</Warning>

### 7. ⚖️ Your Rights
You hold the ultimate right to access, update, or permanently delete your personal information. 
- You can request data purging. The bot developers can completely delete your server records (warnings, leveling XP, balance cache, AFK records, and blacklists) immediately from the developer admin interface.
- If you wish to forcefully exercise these rights, please contact our data team at **arpan2829@gmail.com** or open a support ticket.

### 8. 🚸 Children’s Privacy
The Bot is strictly not intended for use by anyone under the age of 13. We do not knowingly collect personal information from children under 13 under any circumstances.

### 9. 🔄 Changes to This Policy
We may update our Privacy Policy. We will notify major Discord servers of changes, but you are advised to verify this page periodically.

---

### 📩 Contact Us
If you have any questions or overarching concerns about this Privacy Policy, please email **arpan2829@gmail.com**.
