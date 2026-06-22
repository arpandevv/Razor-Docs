---
title: "Dashboard Setup Guide"
description: "Learn how to configure, run, and secure the Web Dashboard for Razor."
icon: "window-maximize"
---

<Note>
  The **Razor Web Dashboard** is a powerful plugin that provides a stunning, full-stack graphical interface to manage your bot and Discord server. Follow these precise steps to properly install and configure it with your source code.
</Note>

---

## 1. 📂 Codebase Integration

In **Razor v2.0.8 Beta**, the **Web Dashboard** is now natively integrated directly into the core source directory under the `Dashboard/` folder out-of-the-box. There is no need to manually copy or extract external zip folders unless you are updating or using a customized theme.

Your project directory structure looks like this:
```text
Razor Source Code/
├── Commands/
├── Dashboard/      <-- Natively included here!
│   ├── public/
│   ├── routes/
│   ├── views/
│   ├── server.js
│   └── .env.example
├── Events/
├── config.js
├── index.js
└── package.json
```

---

## 2. 🔑 Session & Payment Configs (.env)

The Web Dashboard uses Express sessions backed by **MongoDB** (sharing your core bot's `MONGODB_URL` connection string) and requires the **Discord Client Secret** for secure OAuth2 logins.

Ensure the following variables are defined in your root `.env` file:
```env
CLIENT_ID=YOUR_BOT_APPLICATION_ID
CLIENT_SECRET=YOUR_DISCORD_CLIENT_SECRET
MONGODB_URL=YOUR_MONGODB_ATLAS_CONNECTION_STRING
DEVELOPER_ID=YOUR_DISCORD_USER_ID
```

### Stripe Subscription Integration (Optional)

If you want to offer automated premium plans and subscription checkouts via your dashboard, follow the steps below to configure Stripe.

<Steps>
  <Step title="Retrieve your Stripe API Keys">
    1. Sign in to your [Stripe Dashboard](https://dashboard.stripe.com/).
    2. To test payments without real money, toggle **Test Mode** (located in the top-right corner of the dashboard).
    3. Navigate to **Developers** ➡️ **API Keys**.
    4. Copy your **Secret Key** (starts with `sk_test_` for testing, or `sk_live_` for production).
    5. In your project, locate the file `Dashboard/.env.example`, rename it to `Dashboard/.env`, and add your secret key:
       ```env
       STRIPE_SECRET_KEY=sk_test_YOUR_SECRET_KEY
       ```
  </Step>

  <Step title="Set Up Local Webhook Testing">
    To process payments and automatically provision premium status to servers/users, the Stripe billing system needs to communicate back with your application via webhooks.
    
    1. Download and install the [Stripe CLI](https://stripe.com/docs/stripe-cli) for your operating system.
    2. Open your terminal and log in to your Stripe account:
       ```bash
       stripe login
       ```
    3. Run the following command to forward webhook events to your local dashboard server:
       ```bash
       stripe listen --forward-to http://localhost:5500/api/premium/webhook
       ```
    4. Copy the webhook signing secret from the console output (starts with `whsec_...`).
    5. Add it to your `Dashboard/.env` file:
       ```env
       STRIPE_WEBHOOK_SECRET=whsec_YOUR_LOCAL_WEBHOOK_SECRET_HERE
       ```
    
    <Tip>
      Keep the terminal running `stripe listen` open while testing. This acts as a bridge forwarding Stripe's servers to your local machine!
    </Tip>
  </Step>

  <Step title="Transition to Production">
    Once you're ready to accept live payments:
    
    1. Toggle off **Test Mode** in your Stripe Dashboard.
    2. Copy your live **Secret Key** (`sk_live_...`) and place it in your production `Dashboard/.env`.
    3. Go to **Developers** ➡️ **Webhooks** in the Stripe Dashboard and click **Add Endpoint**.
    4. Set the **Endpoint URL** to your public production URL:
       ```text
       https://dashboard.yourdomain.com/api/premium/webhook
       ```
    5. Click **Select events** and choose `checkout.session.completed` (and any other events your app listens to, such as subscription events).
    6. Click **Add Endpoint** to save.
    7. Copy the new live signing secret (`whsec_...`) generated for this production webhook endpoint and update your production `Dashboard/.env`:
       ```env
       STRIPE_WEBHOOK_SECRET=whsec_YOUR_LIVE_WEBHOOK_SECRET_HERE
       ```
  </Step>
</Steps>

---

## 3. ⚙️ Configuring `config.js`

Now that the files are in place, you must tell the bot how to run the web server.

Open your `config.js` file and locate the **Dashboard Configuration** section. Update the variables as shown below:

```javascript
  // Dashboard Configuration //
  dashboard: {
    enabled: true,           // Set this to true to turn on the dashboard
    port: 5500,              // The port the web server will run on (default is 5500)
    domain: "http://localhost:5500", // The public URL of your dashboard
    sessionSecret: "razor-super-secret-key-change-this", // Change this to a random secure string!
  },
```

<Tip>
  **Hosting on a VPS?** Change the `domain` to your server's public IP address (e.g., `http://192.168.1.100:5500`) or your attached domain name (e.g., `https://dashboard.yourdomain.com`).
</Tip>

---

## 4. 🔑 Setting Up the Discord OAuth2 Callback

To allow users to log in to your dashboard securely via Discord, you absolutely must whitelist your callback URL in the [Discord Developer Portal](https://discord.com/developers/applications).

1. Select your Razor Bot application.
2. On the left sidebar, click **OAuth2** -> **General**.
3. Scroll down to the **Redirects** section.
4. Click **Add Redirect** and enter your domain followed by `/callback`.
   - *Example (Local):* `http://localhost:5500/callback`
   - *Example (Live Domain):* `https://dashboard.yourdomain.com/callback`
5. Click **Save Changes**.

---

## 5. 🚀 Launch the Dashboard

You're done! Now, simply run the bot as usual in your terminal:

```bash
npm start
```

Watch your console logs. You should see a success message indicating that the Razor Dashboard is locked, loaded, and running successfully on your specified port!

---

## 6. 🛡️ Developer Admin Panel

Razor v2.0.8 Beta ships with an advanced **Admin Dashboard** restricted solely to the developer. It is accessed by visiting the `/admin` path of your dashboard (e.g., `http://localhost:5500/admin`).

<Warning>
  **Authorization Check**
  
  To access the Admin Panel, you must log in with the Discord account matching the `DEVELOPER_ID` defined in your root `.env` file. Unauthorized users will receive a `403 Forbidden` response.
</Warning>

### Available Admin Sections:
- **Overview Panel (`/admin/overview`)** — Displays live metrics about the bot's health, including heap memory usage, system latency, connected guilds/channels count, client websocket ping, and bot process uptime.
- **User Management (`/admin/users`)** — Search, inspect, and manage Discord users. Allows developers to completely purge user metadata (warnings, leveling XP, balance cache, AFK, and blacklists) with a single click.
- **Server Overview (`/admin/servers`)** — View active guilds where the bot is joined, inspect member counts, owner details, generate instant invite links, or force the bot to leave specific servers remotely.
- **Blacklists Control (`/admin/blacklists`)** — Manage global blacklists. You can blacklist individual users or whole guilds with custom reasons. Blacklisted guilds are automatically left by the bot.
- **Global Broadcasts (`/admin/broadcast`)** — Broadcast critical announcements or alerts. Targets include DMing all server owners, posting to system channels, or finding the first chat channel.
- **Premium & Plan Management (`/admin/premium` / `/admin/premium-plans`)** — Create premium subscriptions dynamically, specify validity duration, and grant/revoke user/guild premium status.
- **Dynamic Command & Feature Locks (`/admin/premium-commands` / `/admin/premium-features`)** — Enforce premium subscription limits on specific Discord commands or dashboard page access.
- **Maintenance Toggle (`/admin/maintenance`)** — Enable a site-wide maintenance screen dynamically to block guild users from modifying dashboard settings during database migration or system updates.
