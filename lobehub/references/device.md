# Device & Connection

Connect devices to the LobeHub gateway for remote tool execution.

---

## connect

Connect to the device gateway and listen for tool calls.

### Usage

```bash
lh connect [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--token <jwt>` | JWT access token |
| `--gateway <url>` | Device gateway URL |
| `--device-id <id>` | Device ID (auto-generated if not provided) |
| `-v, --verbose` | Enable verbose logging |
| `-d, --daemon` | Run as background daemon process |

### Behavior

Establishes a WebSocket connection to the device gateway. When agents need to execute local tools, commands are sent through this connection.

### Examples

```bash
# Connect in foreground
lh connect

# Connect with verbose logging
lh connect -v

# Run as daemon
lh connect -d
```

---

## connect stop

Stop the background daemon process.

### Usage

```bash
lh connect stop
```

---

## connect status

Show background daemon status.

### Usage

```bash
lh connect status
```

### Output

Shows whether the daemon is running, the process ID, and connection status.

---

## connect logs

Tail the daemon log file.

### Usage

```bash
lh connect logs [options]
```

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `-n, --lines <count>` | 50 | Number of log lines to show |
| `-f, --follow` | - | Follow log output in real-time |

### Examples

```bash
# Show last 50 lines
lh connect logs

# Show last 100 lines
lh connect logs -n 100

# Follow logs in real-time
lh connect logs -f
```

---

## connect restart

Restart the background daemon process.

### Usage

```bash
lh connect restart
```

---

## status

Check if gateway connection can be established.

### Usage

```bash
lh status [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--token <jwt>` | JWT access token |
| `--service-token <token>` | Service token (requires --user-id) |
| `--user-id <id>` | User ID (required with --service-token) |
| `--gateway <url>` | Device gateway URL |
| `--timeout <ms>` | Connection timeout in ms (default: 10000) |
| `-v, --verbose` | Enable verbose logging |

### Examples

```bash
# Quick status check
lh status

# With custom timeout
lh status --timeout 5000

# Using service token
lh status --service-token "svc_token" --user-id "user_123"
```

---

## device list

List all online devices.

### Usage

```bash
lh device list [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--json [fields]` | Output JSON |

---

## device info

Show system info of a specific device.

### Usage

```bash
lh device info <deviceId> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `deviceId` | Yes | Device ID |

### Options

| Option | Description |
| ------ | ----------- |
| `--json [fields]` | Output JSON |

---

## device status

Show device connection overview.

### Usage

```bash
lh device status [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--json` | Output JSON |

---

## Typical Workflow

### Set Up Device Connection

1. Log in to your account:

```bash
lh login
```

2. Start the connection daemon:

```bash
lh connect -d
```

3. Check the status:

```bash
lh connect status
```

4. View logs if needed:

```bash
lh connect logs -f
```

5. When done, stop the daemon:

```bash
lh connect stop
```

### Monitor Devices

```bash
# List all online devices
lh device list

# Get info about a specific device
lh device info device_abc123

# Check overall device status
lh device status
```
