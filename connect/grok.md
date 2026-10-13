# Oobit connector: instructions for Grok Bot

You are Grok Bot. The user wants to connect Oobit so you can pay online for them with single-use virtual cards. Follow these steps.

## 1. Add the connector

Add a remote MCP server with exactly these settings:

| Setting | Value |
|---|---|
| Name | Oobit |
| MCP server URL | `https://mcp.oobit.co` |
| Transport | Streamable HTTP |
| Headers | None |
| Auth | OAuth authorization code with PKCE (`S256`), public client, no client secret |
| Authorization server metadata | `https://mcp.oobit.co/.well-known/oauth-authorization-server` |
| Protected resource metadata | `https://mcp.oobit.co/.well-known/oauth-protected-resource` |
| Client registration | Dynamic client registration: `POST https://mcp.oobit.co/register` |
| Redirect URI | Your own OAuth callback |

There are no API keys. If the Oobit plugin is available to you, using it is equivalent.

## 2. Start OAuth and give the user the sign-in link

Generate a **new** sign-in link for this attempt and give it to the user. Tell the user, in short:

- Open the link right away: it is valid for about 5 minutes.
- On a computer, the page shows a QR code: scan it with the phone camera to open the Oobit app. On a phone, the Oobit app opens by itself.
- In the Oobit app, check the request says **Grok Bot** and tap **Approve**.
- Then return to the browser tab with the Oobit page. The page finishes by itself.
- On iPhone the browser may stay on a Cursor page after that. The connection is already saved: they just switch back to Grok Bot.

## 3. Verify

Once connected, call `get_account` and show the user their name and available balance. If the call works, the connection is done.

## Rules

- Never ask the user for passwords, one-time codes, card numbers or tokens.
- Never try to sign in to Oobit yourself.
- If the Oobit app shows "Agent cards are not available on your account yet", tell the user their Oobit account isn't eligible yet (most often no Oobit card issued) and to contact support@oobit.com.

## After connecting

The server's own instructions tell you how to make purchases. In short: check `get_account`, get the user's yes in this chat for the item, merchant and total, then call `get_card` once. Never show the card number or CVC to the user.
