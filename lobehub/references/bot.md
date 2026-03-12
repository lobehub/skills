# Bot Integrations

Connect Discord, Slack, Telegram, Lark, and Feishu bots to your agents.

---

## Supported Platforms

| Platform | Webhook Routing | Required Credentials |
| -------- | --------------- | -------------------- |
| Discord | App ID | Bot Token, Public Key |
| Slack | App ID | Bot Token, Signing Secret |
| Telegram | App ID | Bot Token |
| Lark | App ID | Bot Token, App Secret |
| Feishu | App ID | Bot Token, App Secret |

---

## bot list

List bot integrations.

### Usage

```bash
lh bot list [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `-a, --agent <agentId>` | Filter by agent ID |
| `--platform <platform>` | Filter by platform |
| `--json [fields]` | Output JSON |

### Examples

```bash
# List all bots
lh bot list

# Filter by agent
lh bot list -a agent_abc123

# Filter by platform
lh bot list --platform discord
```

---

## bot view

View bot integration details.

### Usage

```bash
lh bot view <botId> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `botId` | Yes | Bot ID |

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `-a, --agent <agentId>` | Yes | Agent ID |
| `--json [fields]` | No | Output JSON |

---

## bot add

Add a bot integration to an agent.

### Usage

```bash
lh bot add [options]
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `-a, --agent <agentId>` | Yes | Agent ID |
| `--platform <platform>` | Yes | Platform (discord, slack, telegram, lark, feishu) |
| `--app-id <appId>` | Yes | Application ID for webhook routing |
| `--bot-token <token>` | No | Bot token |
| `--public-key <key>` | No | Public key (Discord) |
| `--signing-secret <secret>` | No | Signing secret (Slack) |
| `--app-secret <secret>` | No | App secret (Lark/Feishu) |

### Examples

#### Discord

```bash
lh bot add \
  -a agent_abc123 \
  --platform discord \
  --app-id 123456789 \
  --bot-token "your-bot-token" \
  --public-key "your-public-key"
```

#### Slack

```bash
lh bot add \
  -a agent_abc123 \
  --platform slack \
  --app-id A123456 \
  --bot-token "xoxb-your-bot-token" \
  --signing-secret "your-signing-secret"
```

#### Telegram

```bash
lh bot add \
  -a agent_abc123 \
  --platform telegram \
  --app-id your_bot_username \
  --bot-token "123456789:ABC-your-bot-token"
```

#### Lark / Feishu

```bash
lh bot add \
  -a agent_abc123 \
  --platform lark \
  --app-id cli_abc123 \
  --bot-token "your-bot-token" \
  --app-secret "your-app-secret"
```

---

## bot update

Update a bot integration.

### Usage

```bash
lh bot update <botId> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `botId` | Yes | Bot ID |

### Options

| Option | Description |
| ------ | ----------- |
| `--bot-token <token>` | New bot token |
| `--public-key <key>` | New public key |
| `--signing-secret <secret>` | New signing secret |
| `--app-secret <secret>` | New app secret |
| `--app-id <appId>` | New application ID |
| `--platform <platform>` | New platform |

---

## bot remove

Remove a bot integration.

### Usage

```bash
lh bot remove <botId> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--yes` | Skip confirmation prompt |

---

## bot enable

Enable a bot integration.

### Usage

```bash
lh bot enable <botId>
```

---

## bot disable

Disable a bot integration.

### Usage

```bash
lh bot disable <botId>
```

---

## bot connect

Connect and start a bot.

### Usage

```bash
lh bot connect <botId> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `botId` | Yes | Bot ID |

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `-a, --agent <agentId>` | Yes | Agent ID |

### Behavior

Establishes a connection to the bot platform and starts listening for messages. Messages are routed to the associated agent for processing.

---

## Typical Workflow

### Set Up a Discord Bot

1. Create a Discord application at https://discord.com/developers/applications
2. Get your Bot Token and Public Key from the Bot section
3. Add the bot to your agent:

```bash
lh bot add \
  -a agent_abc123 \
  --platform discord \
  --app-id 123456789 \
  --bot-token "your-bot-token" \
  --public-key "your-public-key"
```

4. Enable the bot:

```bash
lh bot enable bot_xyz789
```

5. Your agent will now respond to Discord messages!

### Set Up a Telegram Bot

1. Create a bot via @BotFather on Telegram
2. Get your bot token
3. Add the bot:

```bash
lh bot add \
  -a agent_abc123 \
  --platform telegram \
  --app-id your_bot_username \
  --bot-token "123456789:ABC-your-bot-token"
```

4. Enable the bot:

```bash
lh bot enable bot_xyz789
```
