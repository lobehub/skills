# Authentication

Manage your LobeHub account authentication.

---

## login

Log in to LobeHub via browser using Device Code Flow.

### Usage

```bash
lh login [options]
```

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `--server <url>` | Official server | LobeHub server URL |

### Behavior

1. Initiates OAuth2 Device Code Flow
2. Opens your browser for authentication
3. Saves credentials locally for future sessions

### Examples

```bash
# Log in to official LobeHub
lh login

# Log in to a custom server
lh login --server https://my-lobehub-instance.com
```

---

## logout

Log out and remove stored credentials.

### Usage

```bash
lh logout
```

### Behavior

Removes all stored authentication credentials from your local machine.

---

## whoami

Display current user information.

### Usage

```bash
lh whoami [options]
```

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `--json [fields]` | - | Output JSON, optionally specify fields (comma-separated) |

### Output

```
User: john@example.com
ID: usr_abc123
Plan: Pro
```

### Examples

```bash
# Display user info
lh whoami

# Get JSON output
lh whoami --json

# Get specific fields
lh whoami --json id,email
```
