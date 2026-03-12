# Search

Search across local resources or the web.

---

## search

Search for resources.

### Usage

```bash
lh search [options]
```

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `-q, --query <query>` | - | Search query (required) |
| `-w, --web` | - | Search the web instead of local resources |
| `-t, --type <type>` | - | Filter by type |
| `-L, --limit <n>` | 10 | Results per type |
| `-e, --engines <engines>` | - | Web search engines (comma-separated, requires --web) |
| `-c, --categories <categories>` | - | Web search categories (comma-separated, requires --web) |
| `-T, --time-range <range>` | - | Time range filter (requires --web) |
| `--json [fields]` | - | Output JSON |

### Resource Types

- `agent` - AI agents
- `topic` - Conversation topics
- `file` - Files
- `folder` - Folders
- `message` - Messages
- `page` - Pages
- `memory` - Memories
- `mcp` - MCP servers
- `plugin` - Plugins
- `communityAgent` - Community agents
- `knowledgeBase` - Knowledge bases

### Examples

```bash
# Search local resources
lh search -q "project report"

# Filter by type
lh search -q "meeting" -t topic

# Search multiple types
lh search -q "api" -t agent,file

# Limit results
lh search -q "code" -L 5

# Web search
lh search -q "react best practices" --web

# Web search with time range
lh search -q "latest news" --web -T week
```

---

## search view

View details of a search result.

### Usage

```bash
lh search view <target> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `target` | Yes | Resource ID or URL |

### Options

| Option | Description |
| ------ | ----------- |
| `-i, --impl <impls>` | Crawler implementations for web URLs |
| `--json [fields]` | Output JSON |

### Examples

```bash
# View a local resource
lh search view agent_abc123

# View a web result
lh search view https://example.com/article

# View with specific crawler
lh search view https://example.com/article -i jina
```

---

## Typical Workflow

### Find an Agent

```bash
# Search for agents related to code review
lh search -q "code review" -t agent

# View agent details
lh search view agent_abc123
```

### Find Relevant Files

```bash
# Search for files about a project
lh search -q "quarterly report" -t file,folder

# Limit to 5 results
lh search -q "meeting notes" -t file -L 5
```

### Research on the Web

```bash
# Search for documentation
lh search -q "react hooks tutorial" --web

# Search recent content only
lh search -q "AI news" --web -T day

# View a specific result
lh search view https://example.com/article --json
```
