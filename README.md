# Copilot-Studio-SSO

Custom web canvas for Microsoft Copilot Studio with seamless SSO via MSAL.js. Authenticates users via Microsoft Entra ID to enable secure, personalized conversations and Dataverse integration without repetitive login prompts. Optimized for secure, identity-aware sales agent deployments.

## 🚀 Overview
This project provides a production-ready boilerplate for hosting a Copilot Studio agent on a custom website (such as GitHub Pages). It solves the "double login" problem by using a Token Exchange flow—once the user logs into your website, the agent automatically recognizes them.



## ✨ Features
- **Silent Authentication**: Uses MSAL.js 2.0+ for secure, popup-based or redirect login.
- **Dynamic Token Exchange**: Intercepts OAuth cards to provide a seamless "no-click" bot login.
- **Dataverse Integration**: Passes user context to Copilot Studio, ensuring the agent respects Row-Level Security (RLS) for sales data.
- **Auto-Start**: Triggers the 'Greeting' system topic automatically upon successful connection.
- **Customizable UI**: Fully themed header and chat canvas using Bot Framework Web Chat.

## 🛠️ Configuration
To get this running, update the constants in the `index.html` file:

```javascript
const clientId = "YOUR_AZURE_APP_CLIENT_ID";
const tenantId = "YOUR_TENANT_ID";
const tokenEndpoint = "YOUR_COPILOT_STUDIO_TOKEN_ENDPOINT";
