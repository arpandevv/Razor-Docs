---
title: "Economy Commands"
description: "Engage your community with Razor's built-in virtual currency and shop systems."
icon: "coins"
---

<Note>
  Engage your community with Razor's massive internal economy system. Users can work, rob, beg, and buy configurable items from your custom server shop!
</Note>

---

## 💰 Core Economy

| Command | Description |
| :--- | :--- |
| `[ /economy balance ]` | Check your current generated wealth (Cash vs. Bank limits). |
| `[ /economy deposit ]` | Move cash securely into your bank so it cannot be robbed. |
| `[ /economy withdraw ]` | Take money out of the bank. |
| `[ /economy pay ]` | Transfer funds to another server member. |
| `[ /economy rob ]` | Attempt to steal cash from another user (Risk involved!). |

---

## 🛠️ Earning Currency

| Command | Description | Cooldown |
| :--- | :--- | :--- |
| `[ /work ]` | Perform a randomized job to earn a solid paycheck. | 1 Hour |
| `[ /daily ]` | Claim your guaranteed daily allowance. | 24 Hours |
| `[ /beg ]` | Ask the bot for spare change. High failure rate! | 5 Minutes |

---

## 🛍️ The Server Shop

Admin users can create infinite custom items utilizing the dynamic shop system. 

| Command | Description |
| :--- | :--- |
| `[ /shop ]` | Browse all available items currently stocked in the server marketplace. |
| `[ /inventory ]` | View the items you have successfully purchased. |
| `[ /buy ]` | Purchase an item using your cached balance. |

<Tip>
  Assigning an item type of `role` in the shop configuration means users will **automatically be granted that Discord Role** when they purchase the item!
</Tip>

---

## 🏆 Standings & Progression

| Command | Description |
| :--- | :--- |
| `[ /leaderboard ]` | View the richest members, or the highest XP holders in your server. |
| `[ /rank ]` | Generate a beautiful UI card displaying your current level and XP progression. |
| `[ /reset ]` | *(Admin Only)* Completely wipe the economy or XP database for the server. |
