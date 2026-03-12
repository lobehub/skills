# Skills & Plugins

Manage agent skills and plugins.

---

# Skills

---

## skill list

List skills.

### Usage

```bash
lh skill list [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--source <source>` | Filter by source: builtin, market, user |
| `--json [fields]` | Output JSON |

### Examples

```bash
# List all skills
lh skill list

# List user-created skills
lh skill list --source user

# List marketplace skills
lh skill list --source market
```

---

## skill view

View skill details.

### Usage

```bash
lh skill view <id> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `id` | Yes | Skill ID |

### Options

| Option | Description |
| ------ | ----------- |
| `--json [fields]` | Output JSON |

---

## skill create

Create a user skill.

### Usage

```bash
lh skill create [options]
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `-n, --name <name>` | Yes | Skill name |
| `-d, --description <desc>` | Yes | Skill description |
| `-c, --content <content>` | Yes | Skill content (prompt) |
| `-i, --identifier <id>` | No | Custom identifier |

### Examples

```bash
lh skill create \
  -n "Code Reviewer" \
  -d "Reviews code for bugs and best practices" \
  -c "You are an expert code reviewer. When reviewing code, look for: 1) Bugs and errors 2) Performance issues 3) Security vulnerabilities 4) Code style"
```

---

## skill edit

Update a skill.

### Usage

```bash
lh skill edit <id> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `id` | Yes | Skill ID |

### Options

| Option | Description |
| ------ | ----------- |
| `-c, --content <content>` | New content |
| `-n, --name <name>` | New name (via manifest) |
| `-d, --description <desc>` | New description (via manifest) |

---

## skill delete

Delete a skill.

### Usage

```bash
lh skill delete <id> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--yes` | Skip confirmation prompt |

---

## skill search

Search skills.

### Usage

```bash
lh skill search <query> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `query` | Yes | Search query |

### Options

| Option | Description |
| ------ | ----------- |
| `--json [fields]` | Output JSON |

### Examples

```bash
lh skill search "code review"
lh skill search "pdf" --json
```

---

## skill install

Install a skill.

### Usage

```bash
lh skill install <source> [options]
lh skill i <source> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `source` | Yes | GitHub URL/shorthand, ZIP URL, or marketplace identifier |

### Options

| Option | Description |
| ------ | ----------- |
| `--branch <branch>` | Branch name (GitHub only) |

### Source Formats

- **GitHub shorthand:** `owner/repo`
- **GitHub URL:** `https://github.com/owner/repo`
- **ZIP URL:** `https://example.com/skill.zip`
- **Marketplace ID:** `skill-identifier`

### Examples

```bash
# Install from marketplace
lh skill install lobehub-pdf-tools

# Install from GitHub
lh skill install lobehub/pdf-skill
lh skill install https://github.com/lobehub/pdf-skill

# Install specific branch
lh skill install lobehub/pdf-skill --branch develop

# Install from ZIP
lh skill install https://example.com/my-skill.zip
```

---

## skill resources

List skill resource files.

### Usage

```bash
lh skill resources <id> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--json [fields]` | Output JSON |

---

## skill read-resource

Read a skill resource file.

### Usage

```bash
lh skill read-resource <id> <path>
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `id` | Yes | Skill ID |
| `path` | Yes | Resource file path |

---

# Plugins

---

## plugin list

List installed plugins.

### Usage

```bash
lh plugin list [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--json [fields]` | Output JSON |

---

## plugin create

Create a new plugin (without settings).

### Usage

```bash
lh plugin create [options]
```

### Options

| Option | Required | Default | Description |
| ------ | -------- | ------- | ----------- |
| `-i, --identifier <id>` | Yes | - | Plugin identifier |
| `--manifest <json>` | Yes | - | Plugin manifest JSON |
| `--type <type>` | No | plugin | Plugin type: plugin or customPlugin |
| `--custom-params <json>` | No | - | Custom parameters JSON |

---

## plugin install

Install a plugin.

### Usage

```bash
lh plugin install [options]
```

### Options

| Option | Required | Default | Description |
| ------ | -------- | ------- | ----------- |
| `-i, --identifier <id>` | Yes | - | Plugin identifier |
| `--manifest <json>` | Yes | - | Plugin manifest JSON |
| `--type <type>` | No | plugin | Plugin type: plugin or customPlugin |
| `--settings <json>` | No | - | Plugin settings JSON |

### Examples

```bash
lh plugin install \
  -i my-weather-plugin \
  --manifest '{"name": "Weather", "description": "Get weather info"}' \
  --settings '{"apiKey": "your-api-key"}'
```

---

## plugin uninstall

Uninstall a plugin.

### Usage

```bash
lh plugin uninstall <id> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--yes` | Skip confirmation prompt |

---

## plugin update

Update plugin settings or manifest.

### Usage

```bash
lh plugin update <id> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `id` | Yes | Plugin ID |

### Options

| Option | Description |
| ------ | ----------- |
| `--manifest <json>` | New manifest JSON |
| `--settings <json>` | New settings JSON |

### Examples

```bash
# Update settings
lh plugin update my-weather-plugin --settings '{"apiKey": "new-api-key"}'

# Update manifest
lh plugin update my-weather-plugin --manifest '{"name": "Weather Pro", "description": "Enhanced weather info"}'
```
