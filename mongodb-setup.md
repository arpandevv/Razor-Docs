---
title: "MongoDB Atlas Setup"
description: "A step-by-step guide to creating a free database on MongoDB Atlas and retrieving your connection URL."
icon: "database"
---

To store bot data, guild configurations, economy records, and settings, Razor relies on a MongoDB database. Follow this guide to set up a free cloud database cluster and obtain your connection URL.

---

## 🚀 Setup Steps

<Steps>
  <Step title="Create a MongoDB Atlas Account">
    1. Go to the [MongoDB Atlas website](https://www.mongodb.com/cloud/atlas/register).
    2. Sign up for a free account using your email or register with Google/GitHub.
    3. Complete the brief onboarding questionnaire.
  </Step>

  <Step title="Deploy a Free Shared Cluster">
    1. Once logged in, click on **Create a Deployment** (or **Build a Database**).
    2. Choose the **M0** (Free) tier. This tier is completely free forever and provides up to 512MB of storage, which is more than enough for the bot.
    3. Select your preferred Cloud Provider (e.g., **AWS**) and a **Region** close to your hosting environment or geographical location.
    4. Set your cluster name (default is `Cluster0`) and click **Create**.
  </Step>

  <Step title="Configure Database Access (Credentials)">
    During the cluster creation process (or under **Security > Database Access** in the left sidebar):
    
    1. Set a **Username** (e.g., `razor-admin`).
    2. Generate or set a secure **Password**.
    
    <Warning>
      **Save Your Password!**
      
      Copy this password and store it somewhere safe. You will need to insert it directly into your `.env` file connection string later.
    </Warning>

    3. Ensure the user role is configured for **Read and write to any database** (Atlas admin).
    4. Click **Create Database User**.
  </Step>

  <Step title="Configure Network Access (Whitelist IP)">
    To allow your bot server (whether running locally or on a VPS) to communicate with MongoDB Atlas:
    
    1. Under the **Security > Network Access** tab in the left sidebar, click **Add IP Address**.
    2. Select **Allow Access from Anywhere** (this adds `0.0.0.0/0`).
    
    <Note>
      **Why Allow Access from Anywhere?**
      
      If you host the bot on your local PC or a dynamic cloud provider (like VPS, Heroku, etc.), your server's IP address will change frequently. Whitelisting `0.0.0.0/0` ensures your bot never loses database connection.
    </Note>

    3. Click **Confirm** and wait for the status to turn from *Pending* to *Active*.
  </Step>

  <Step title="Obtain Your Connection String">
    1. Navigate to the **Database** (or clusters) page in the left sidebar.
    2. Click the **Connect** button next to your cluster.
    3. Choose **Drivers** under the connection options.
    4. Choose **Node.js** as your driver and select the latest version.
    5. Copy the connection string template. It will look like this:
       ```text
       mongodb+srv://<db_username>:<db_password>@cluster0.abcde.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0
       ```
  </Step>

  <Step title="Configure Your Environment File">
    1. Open your bot's project folder in your editor (e.g., VS Code).
    2. Open your `.env` file (if you haven't created one, rename `.env.example` to `.env`).
    3. Paste your connection string into the `MONGODB_URL` variable.
    4. Replace `<db_username>` with your database user's username.
    5. Replace `<db_password>` with the password you saved in Step 3.
    6. Specify a database name (e.g. `razor`) right before the `?` query parameters.

    Here is an example of how your configured `.env` line should look:
    ```env
    MONGODB_URL=mongodb+srv://razor-admin:mySuperSecretPassword123@cluster0.abcde.mongodb.net/razor?retryWrites=true&w=majority&appName=Cluster0
    ```
  </Step>
</Steps>

---

## 🔍 Troubleshooting Connections

If your bot crashes or outputs database connection errors on startup, verify the following:

- **Special Characters in Passwords**: If your database password contains special characters like `@`, `:`, `/`, or `+`, you must URL-encode them (e.g., `@` becomes `%40`), or recreate the database user with only letters and numbers.
- **IP Access Whitelist**: Double check **Network Access** in MongoDB Atlas. If `0.0.0.0/0` is not active or has been deleted, the cluster will reject your bot's connection.
- **Accidental Brackets**: Do not keep `<` or `>` brackets around your password or username in the `.env` URL. 
  - ❌ Incorrect: `mongodb+srv://<razor-admin>:<password>@...`
  -  Correct: `mongodb+srv://razor-admin:password@...`
