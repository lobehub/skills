# Models & Providers

Manage AI models and providers.

---

# Models

---

## model list

List models for a provider.

### Usage

```bash
lh model list <providerId> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `providerId` | Yes | Provider ID (e.g., openai, anthropic) |

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `-L, --limit <n>` | 50 | Maximum number of items |
| `--enabled` | - | Only show enabled models |
| `--type <type>` | - | Filter by model type |
| `--json [fields]` | - | Output JSON |

### Model Types

- `chat` - Chat/completion models
- `embedding` - Embedding models
- `tts` - Text-to-speech models
- `stt` - Speech-to-text models
- `image` - Image generation models
- `video` - Video generation models
- `text2music` - Music generation models
- `realtime` - Real-time streaming models

### Examples

```bash
# List all OpenAI models
lh model list openai

# List only enabled chat models
lh model list openai --enabled --type chat

# JSON output
lh model list anthropic --json
```

---

## model view

View model details.

### Usage

```bash
lh model view <id> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--json [fields]` | Output JSON |

---

## model create

Create a new model.

### Usage

```bash
lh model create [options]
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `--id <id>` | Yes | Model ID |
| `--provider <providerId>` | Yes | Provider ID |
| `--display-name <name>` | No | Display name |
| `--type <type>` | No | Model type (default: chat) |

### Examples

```bash
lh model create --id gpt-4-custom --provider openai --display-name "GPT-4 Custom" --type chat
```

---

## model edit

Update model info.

### Usage

```bash
lh model edit <id> [options]
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `--provider <providerId>` | Yes | Provider ID |
| `--display-name <name>` | No | Display name |
| `--type <type>` | No | Model type |

---

## model toggle

Enable or disable a model.

### Usage

```bash
lh model toggle <id> [options]
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `--provider <providerId>` | Yes | Provider ID |
| `--enable` | No* | Enable the model |
| `--disable` | No* | Disable the model |

*One of `--enable` or `--disable` is required.

### Examples

```bash
# Enable a model
lh model toggle gpt-4o --provider openai --enable

# Disable a model
lh model toggle gpt-3.5-turbo --provider openai --disable
```

---

## model batch-toggle

Enable or disable multiple models at once.

### Usage

```bash
lh model batch-toggle <ids...> [options]
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `--provider <providerId>` | Yes | Provider ID |
| `--enable` | No* | Enable the models |
| `--disable` | No* | Disable the models |

### Examples

```bash
lh model batch-toggle gpt-4o gpt-4-turbo claude-3-opus --provider openai --enable
```

---

## model delete

Delete a model.

### Usage

```bash
lh model delete <id> [options]
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `--provider <providerId>` | Yes | Provider ID |
| `--yes` | No | Skip confirmation prompt |

---

## model clear

Clear models for a provider.

### Usage

```bash
lh model clear [options]
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `--provider <providerId>` | Yes | Provider ID |
| `--remote` | No | Only clear remote/fetched models |
| `--yes` | No | Skip confirmation prompt |

---

# Providers

---

## provider list

List AI providers.

### Usage

```bash
lh provider list [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--json [fields]` | Output JSON |

---

## provider view

View provider details.

### Usage

```bash
lh provider view <id> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--json [fields]` | Output JSON |

---

## provider create

Create a new AI provider.

### Usage

```bash
lh provider create [options]
```

### Options

| Option | Required | Default | Description |
| ------ | -------- | ------- | ----------- |
| `--id <id>` | Yes | - | Provider ID |
| `-n, --name <name>` | Yes | - | Provider name |
| `-s, --source <source>` | No | custom | Source type (builtin, custom) |
| `-d, --description <desc>` | No | - | Provider description |
| `--logo <logo>` | No | - | Provider logo URL |
| `--sdk-type <sdkType>` | No | - | SDK type |

### SDK Types

- `openai` - OpenAI-compatible API
- `anthropic` - Anthropic API
- `azure` - Azure OpenAI
- `bedrock` - AWS Bedrock
- `google` - Google AI
- `ollama` - Ollama local models

### Examples

```bash
lh provider create \
  --id my-openai \
  -n "My OpenAI" \
  -d "Custom OpenAI provider" \
  --sdk-type openai
```

---

## provider edit

Update provider info.

### Usage

```bash
lh provider edit <id> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `-n, --name <name>` | Provider name |
| `-d, --description <desc>` | Provider description |
| `--logo <logo>` | Provider logo URL |
| `--sdk-type <sdkType>` | SDK type |

---

## provider config

Configure provider settings (API key, base URL, etc.).

### Usage

```bash
lh provider config <id> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--api-key <key>` | Set API key |
| `--base-url <url>` | Set base URL |
| `--check-model <model>` | Set connectivity check model |
| `--enable-response-api` | Enable Response API mode (OpenAI) |
| `--disable-response-api` | Disable Response API mode |
| `--fetch-on-client` | Enable fetching models on client side |
| `--no-fetch-on-client` | Disable fetching models on client side |
| `--show` | Show current config |
| `--json [fields]` | Output JSON (with --show) |

### Examples

```bash
# Set API key
lh provider config openai --api-key sk-...

# Set base URL for custom endpoint
lh provider config my-openai --base-url https://api.my-server.com/v1

# View current config
lh provider config openai --show
```

---

## provider test

Test provider connectivity.

### Usage

```bash
lh provider test <id> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `-m, --model <model>` | Model to test with (defaults to provider checkModel) |
| `--json` | Output result as JSON |

### Examples

```bash
# Test with default model
lh provider test openai

# Test with specific model
lh provider test openai -m gpt-4o
```

---

## provider toggle

Enable or disable a provider.

### Usage

```bash
lh provider toggle <id> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--enable` | Enable the provider |
| `--disable` | Disable the provider |

---

## provider delete

Delete a provider.

### Usage

```bash
lh provider delete <id> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--yes` | Skip confirmation prompt |
