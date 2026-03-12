# User & Account

Manage your user account and settings.

---

## user info

View user registration info.

### Usage

```bash
lh user info [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--json [fields]` | Output JSON |

---

## user settings

Update user settings.

### Usage

```bash
lh user settings --data <json>
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `--data <json>` | Yes | Settings data as JSON |

### Examples

```bash
lh user settings --data '{"theme": "dark", "language": "en"}'
```

---

## user preferences

Update user preferences.

### Usage

```bash
lh user preferences --data <json>
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `--data <json>` | Yes | Preferences data as JSON |

---

## user update-avatar

Update user avatar.

### Usage

```bash
lh user update-avatar <url>
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `url` | Yes | Avatar URL or Base64 data |

### Examples

```bash
# Update with URL
lh user update-avatar https://example.com/avatar.png

# Update with Base64
lh user update-avatar "data:image/png;base64,..."
```

---

## user update-name

Update user full name or username.

### Usage

```bash
lh user update-name [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--full-name <name>` | Update full name (max 64 chars) |
| `--username <name>` | Update username (alphanumeric + underscore) |

### Examples

```bash
# Update full name
lh user update-name --full-name "John Doe"

# Update username
lh user update-name --username "johndoe"

# Update both
lh user update-name --full-name "John Doe" --username "johndoe"
```

---

## usage

View usage statistics.

### Usage

```bash
lh usage [options]
```

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `--month <YYYY-MM>` | Current month | Month to query |
| `--daily` | - | Group by day |
| `--json [fields]` | - | Output JSON |

### Output

Displays:
- Token usage table (input/output tokens by model)
- Total costs
- Calendar heatmap for the past 12 months

### Examples

```bash
# View current month usage
lh usage

# View specific month
lh usage --month 2024-03

# View daily breakdown
lh usage --daily

# JSON output
lh usage --json
```
