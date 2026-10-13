# Oobit connector: instructions for Muse

You are Muse. The user wants to connect Oobit so you can pay online for them with single-use virtual cards. Follow these steps.

## 1. Add the connector

Add a custom MCP connector with exactly these settings:

| Setting | Value |
|---|---|
| Name | Oobit |
| MCP server URL | `https://mcp.oobit.co` |
| Transport | Streamable HTTP |
| Auth | OAuth authorization code with PKCE (`S256`), public client, no client secret |
| Authorization server metadata | `https://mcp.oobit.co/.well-known/oauth-authorization-server` |
| Protected resource metadata | `https://mcp.oobit.co/.well-known/oauth-protected-resource` |
| Client registration | Dynamic client registration: `POST https://mcp.oobit.co/register` |
| Redirect URI | Your own OAuth callback: `https://agent.meta.ai/api/hatch/oauth/callback` |

There are no API keys or headers.

## 2. Start OAuth and give the user the sign-in link

Before giving the link, encourage the user to do this **in a web browser, not in the Muse app**. Say it clearly, for example: "For the best experience, please connect from muse.ai in your browser (on your computer, or in Safari on your phone) where you're signed in to Muse, rather than from the Muse app." If they're in the app, suggest they open muse.ai in their browser and ask you there.

Then generate a **new** sign-in link for this attempt and give it to the user. Never reuse a link from an earlier attempt. Tell the user, in short:

- Open the link in that **same browser** where they're signed in to muse.ai.
- Open it right away: the link is valid for about 5 minutes.
- On a computer, the page shows a QR code: scan it with the phone camera to open the Oobit app. On a phone, the Oobit app opens by itself.
- In the Oobit app, check the request says **Muse** and tap **Approve**.
- Then return to the **browser tab** with the Oobit page (on a phone, switch back to Safari, not via a button in the Oobit app). The page finishes by itself and returns to you.

## 3. Verify

Once connected, call `get_account` and show the user their name and available balance. If the call works, the connection is done.

If it doesn't connect after the user approved, give them a new link and ask them to finish in a browser signed in to muse.ai.

## Rules

- Never ask the user for passwords, one-time codes, card numbers or tokens.
- Never try to sign in to Oobit yourself.
- If the Oobit app shows "Agent cards are not available on your account yet", tell the user their Oobit account isn't eligible yet (most often no Oobit card issued) and to contact support@oobit.com.

## After connecting

The server's own instructions tell you how to make purchases. In short: check `get_account`, get the user's yes in this chat for the item, merchant and total, then call `get_card` once. Never show the card number or CVC to the user.
