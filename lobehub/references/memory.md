# Memory Management

Manage user memories for personalization.

---

## Memory Categories

| Category | Description |
| -------- | ----------- |
| `identity` | Who you are - name, role, relationships |
| `activity` | What you do - tasks, projects, routines |
| `context` | Current situation - environment, tools, constraints |
| `experience` | Past events - accomplishments, learnings |
| `preference` | What you like - styles, preferences, habits |

---

## memory list

List memories by category.

### Usage

```bash
lh memory list [category] [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `category` | No | Memory category (identity, activity, context, experience, preference) |

### Options

| Option | Description |
| ------ | ----------- |
| `--json [fields]` | Output JSON |

### Examples

```bash
# List all memories
lh memory list

# List by category
lh memory list identity
lh memory list preference
```

---

## memory create

Create an identity memory entry.

### Usage

```bash
lh memory create [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--type <type>` | Memory type |
| `--role <role>` | Role |
| `--relationship <rel>` | Relationship |
| `-d, --description <desc>` | Description |
| `--labels <labels...>` | Extracted labels |

### Examples

```bash
lh memory create \
  --type "person" \
  --role "developer" \
  --description "I am a full-stack developer working on web applications" \
  --labels frontend backend javascript
```

---

## memory edit

Update a memory entry.

### Usage

```bash
lh memory edit <category> <id> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `category` | Yes | Memory category |
| `id` | Yes | Memory ID |

### Options

Options vary by category type. Common options:

| Option | Description |
| ------ | ----------- |
| `-d, --description <desc>` | Description |
| `--labels <labels...>` | Extracted labels |

---

## memory delete

Delete a memory entry.

### Usage

```bash
lh memory delete <category> <id> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `category` | Yes | Memory category |
| `id` | Yes | Memory ID |

### Options

| Option | Description |
| ------ | ----------- |
| `--yes` | Skip confirmation prompt |

### Examples

```bash
lh memory delete identity mem_abc123 --yes
```

---

## memory persona

View your memory persona summary.

### Usage

```bash
lh memory persona [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--json [fields]` | Output JSON |

### Output

Displays a summary of your persona based on all stored memories.

---

## memory extract

Extract memories from chat history.

### Usage

```bash
lh memory extract [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--from <date>` | Start date (ISO format) |
| `--to <date>` | End date (ISO format) |

### Behavior

Starts a background task that analyzes your chat history and extracts relevant memories into the appropriate categories.

### Examples

```bash
# Extract from all history
lh memory extract

# Extract from date range
lh memory extract --from 2024-01-01 --to 2024-03-31
```

---

## memory extract-status

Check memory extraction task status.

### Usage

```bash
lh memory extract-status [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--task-id <id>` | Specific task ID to check |
| `--json [fields]` | Output JSON |

---

## Typical Workflow

### Build Your Persona

1. Extract memories from existing conversations:

```bash
lh memory extract
```

2. Check extraction status:

```bash
lh memory extract-status
```

3. View your persona:

```bash
lh memory persona
```

4. Manually add important memories:

```bash
lh memory create \
  --type "preference" \
  --description "I prefer detailed explanations with code examples" \
  --labels technical detailed
```

5. Review and edit memories:

```bash
# List all memories
lh memory list

# Edit a specific memory
lh memory edit preference mem_abc123 -d "I prefer concise answers"

# Delete irrelevant memories
lh memory delete activity mem_xyz789 --yes
```
