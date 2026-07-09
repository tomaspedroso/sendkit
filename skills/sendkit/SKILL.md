---
name: sendkit
description: |
  Send Telegram messages from agents using the Sendkit MCP tool or CLI fallback.
  Use this skill whenever the user asks to send a Telegram message, mentions Sendkit,
  wants to interact with the Sendkit toolset, needs to verify Sendkit is configured
  and working, or asks about choosing between Sendkit MCP and CLI approaches.
  Also use it when the user says "send a message", "notify me on Telegram",
  "send an alert to Telegram", or any similar messaging request where Sendkit
  could be the tool to use.
---

Sendkit lets you send Telegram messages from the terminal or from an AI agent.
It provides two ways to send messages:

## Sending a message

### 1. Try the MCP tool first

If the Sendkit MCP server is configured in your MCP client, it exposes a `telegram` tool that takes two parameters:

- `chatId` — the Telegram chat ID to send to (string, required)
- `message` — the message text (string, required)

The MCP server reads `TELEGRAM_BOT_TOKEN` from its configured environment, so no extra auth is needed if the token is set.

### 2. Fall back to the CLI

If the MCP tool isn't available, use the Sendkit CLI:

```bash
sendkit telegram <chatId> <message>
```

The CLI reads the bot token from `~/.config/sendkit/config.json`. If it's not configured yet:

```bash
sendkit init --telegram-bot-token <token>
```

## Getting a bot token

To send Telegram messages, you need a Telegram bot token:

1. Open Telegram and search for [@BotFather](https://t.me/botfather)
2. Send `/newbot` and follow the prompts
3. Copy the token (looks like `123456789:ABCdefGHIjklmNOPqrstUVwxyz`)
4. Configure it using one of the methods below

## Configuration

| Method | How the token is set |
|--------|---------------------|
| **MCP** | Set the `TELEGRAM_BOT_TOKEN` environment variable in your MCP client's server configuration |
| **CLI** | Run `sendkit init --telegram-bot-token <token>` to save it to `~/.config/sendkit/config.json` |

## Verification

To confirm everything is working, send a test message to a known chat ID. If authentication fails, the token is likely missing or incorrect — check the configuration method above for your setup.
