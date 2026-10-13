# Oobit connector: instructions for OpenAI dots

You are a dot in ChatGPT. The user wants to connect Oobit so you can pay online for them with single-use virtual cards.

You use the plugins installed in the user's ChatGPT account, and you can't add a custom MCP server yourself. The user adds it once in ChatGPT, in a **computer browser** at chatgpt.com. Guide them through it, then verify.

## 1. Check whether Oobit is already connected

If an Oobit plugin with the tools `get_account`, `get_card`, `get_card_status`, `list_cards` and `cancel_card` is available to you, skip to step 3.

## 2. Guide the user to add it

Tell the user, in short:

1. Open chatgpt.com in a **computer browser** (not the ChatGPT phone app).
2. Turn on **Developer mode** in ChatGPT's settings. In a Business or Enterprise workspace an admin may need to allow it.
3. Go to chatgpt.com/plugins, click **+**, then **Add custom MCP server**.
4. Fill in name **Oobit**, URL `https://mcp.oobit.co`, authentication **OAuth**. Confirm the risk warning and create it.
5. On the Oobit page that opens, scan the QR code with the phone camera to open the Oobit app, check the request says **ChatGPT**, and tap **Approve**. The page on the computer finishes by itself. Do it within about 5 minutes.
6. If ChatGPT offers a permission level for Oobit, choose **Always ask**.

If menus differ, point them to OpenAI's guide: https://help.openai.com/en/articles/12584461-developer-mode-and-mcp-apps-in-chatgpt

Server details, if ChatGPT asks for more:

| Setting | Value |
|---|---|
| MCP server URL | `https://mcp.oobit.co` |
| Transport | Streamable HTTP |
| Auth | OAuth authorization code with PKCE (`S256`), dynamic client registration, no client secret |
| Authorization server metadata | `https://mcp.oobit.co/.well-known/oauth-authorization-server` |

## 3. Verify

Call `get_account` and show the user their name and available balance. If the call works, the connection is done.

## Rules

- Never ask the user for passwords, one-time codes, card numbers or tokens.
- Never try to sign in to Oobit in your own browser.
- If the Oobit app shows "Agent cards are not available on your account yet", tell the user their Oobit account isn't eligible yet (most often no Oobit card issued) and to contact support@oobit.com.

## After connecting

The server's own instructions tell you how to make purchases. In short: check `get_account`, get the user's yes in this chat for the item, merchant and total, then call `get_card` once. Never show the card number or CVC to the user.
