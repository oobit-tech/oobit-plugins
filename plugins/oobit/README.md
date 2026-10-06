# Oobit for Cursor and Grok Bot

Lets your agent pay online for you with single-use Oobit virtual cards.

## Before you start

You need:

- An Oobit account, verified and in good standing. Get the Oobit app at [oobit.com](https://www.oobit.com).
- An Oobit card already issued on that account.
- Funds in your Oobit app account. Purchases are paid from your in-app balance, not from an external wallet.

Without these, Oobit won't let you connect your agent.

## Install

Add **Oobit** from the Plugins page in Cursor or Grok Bot, then click **Authorize** and sign in to your Oobit account. There are no API keys to paste.

## How it works

1. The agent checks your available balance and card limits.
2. It tells you the item, the merchant and the total, and waits for your yes in the chat.
3. After you confirm, it gets a single-use card for that amount. The card expires one hour later.
4. It uses the card once, at that merchant. If the purchase is abandoned, it cancels the card and the held funds are released.

| Tool | What it does |
|---|---|
| `get_account` | Your name, available balance and card limits |
| `get_card` | Creates a single-use card for one confirmed purchase |
| `get_card_status` | Whether a card was used, canceled or expired |
| `list_cards` | Your cards, newest first |
| `cancel_card` | Cancels an unused card and releases the funds |

## Security

- Sign-in is OAuth 2.1 with PKCE. The connector never sees your Oobit password, and the OAuth tokens stay on Cursor's connector backend.
- Each card works for one purchase, for at most the confirmed amount, and expires one hour after it is created.
- Card numbers are sent encrypted end to end between Oobit and the connector and are never written to logs.
- You can revoke the connection at any time from your Oobit account. Revoked connections stop working immediately.

## Support

support@oobit.com
