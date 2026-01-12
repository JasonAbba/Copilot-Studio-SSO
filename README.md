# 🚀 Copilot Studio SSO Web Chat (MSAL + Direct Line)

This project demonstrates how to embed **Microsoft Copilot Studio** into a modern web UI with **Azure AD (Entra ID) Single Sign-On (SSO)** using **MSAL.js** and **Bot Framework Web Chat**.

It is designed to be deployed as a **static website (GitHub Pages)** and provides a clean, enterprise-ready chat experience with secure authentication.

---

## ✨ Features

* 🔐 Azure AD / Entra ID Authentication using MSAL.js
* 🤖 Copilot Studio bot integration via Direct Line
* 🔄 Silent token exchange (OAuth SSO) with Copilot Studio
* 🎨 Modern, enterprise UI styled with CSS
* 👤 User initials avatar and personalized greeting
* 🚪 Sign-out support
* 🌐 GitHub Pages ready

---

## 🧩 Architecture Overview

```text
Browser
  │
  ├─ MSAL.js (Azure AD Login)
  │      └─ Access Token (access_as_user)
  │
  ├─ Direct Line Token Endpoint
  │
  └─ Bot Framework Web Chat
          └─ Copilot Studio Bot
                 └─ OAuth Token Exchange
```

---

## 📁 Project Structure

```text
/
├── index.html        # Main application (HTML + CSS + JS)
└── README.md         # Documentation (this file)
```

---

## 🔧 Configuration

All configuration lives inside the `<script>` section of **index.html**.

---

## 1️⃣ Azure AD (Entra ID) App Registration – Web App

Used for authenticating users.

```javascript
clientId: "YOUR-CLIENT-ID",
authority: "https://login.microsoftonline.com/YOUR-TENANT-ID",
redirectUri: "https://<username>.github.io/<repo-name>/",
postLogoutRedirectUri: "https://<username>.github.io/<repo-name>/"
```

### Required settings in Azure Portal

* **Platform**: Single-page application (SPA)
* **Redirect URI**: Your GitHub Pages URL

### API Permissions

* `User.Read`
* Custom scope: `access_as_user`

---

## 2️⃣ Copilot Studio Authentication App

Used for token exchange between Web Chat and Copilot Studio.

```text
scope: api://<COPILOT-AUTH-APP-ID>/access_as_user
```

This must match:

* The OAuth connection in Copilot Studio
* The scope exposed by your Azure AD app

---

## 3️⃣ Direct Line Token Endpoint

Generated from Copilot Studio.

```text
tokenEndpoint: https://<environment>.api.powerplatform.com/...
```

This endpoint is used to securely generate a Direct Line token.

---

## 🔐 How Authentication Works

1. User loads the page
2. MSAL checks for an existing login
3. If not logged in → redirect to Azure AD
4. After login:

   * User name is displayed
   * Access token is silently acquired
   * Copilot Studio requests OAuth card
   * Token is automatically exchanged
   * User is signed into Copilot without prompts

---

## 💬 Copilot Studio SSO Flow

* OAuth card is intercepted
* `signin/tokenExchange` is sent automatically
* OAuth card never appears to the user
* True seamless SSO experience

---

## 🎨 UI Customization

The chat UI is customized using `styleOptions`:

* Rounded chat bubbles
* Microsoft Fluent colors
* User & bot avatars with initials
* Clean send box with hidden upload button

You can easily tweak colors, fonts, spacing, and avatars.

---

## 🚀 Deployment (GitHub Pages)

1. Push `index.html` and `README.md` to your repository
2. Go to **Settings → Pages**
3. Select:

   * **Source**: `main`
   * **Folder**: `/root`
4. Save

Your app will be available at:

```text
https://<username>.github.io/<repo-name>/
```

---

## 🧪 Local Testing

Because MSAL requires HTTPS:

* Use GitHub Pages
* Or a local HTTPS server (e.g., `localhost` with SSL)

---

---|------|
| Infinite login loop | Redirect URI mismatch |
| OAuth card still shows | Scope mismatch |
| Token exchange fails | Wrong OAuth connection name |
| Blank page | GitHub Pages not enabled |

---

## 🔒 Security Notes

* Tokens are stored in `sessionStorage`
* No secrets are exposed in the frontend
* Direct Line token is short-lived
* Azure AD handles identity security

---

## 📌 Technologies Used

* MSAL.js
* Bot Framework Web Chat
* Copilot Studio
* Azure AD (Entra ID)
* GitHub Pages
