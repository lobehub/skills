# Files & Documents

Manage files and documents.

---

## file list

List files.

### Usage

```bash
lh file list [options]
```

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `--kb-id <id>` | - | Filter by knowledge base ID |
| `-L, --limit <n>` | 30 | Maximum number of items |
| `--json [fields]` | - | Output JSON |

### Examples

```bash
# List all files
lh file list

# Filter by knowledge base
lh file list --kb-id kb_abc123

# Limit results
lh file list -L 10 --json
```

---

## file view

View file details.

### Usage

```bash
lh file view <id> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `id` | Yes | File ID |

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `--json [fields]` | - | Output JSON |

---

## file upload

Upload a file by URL.

### Usage

```bash
lh file upload <url> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `url` | Yes | File URL |

### Options

| Option | Description |
| ------ | ----------- |
| `--hash <hash>` | File hash for deduplication check |
| `--name <name>` | File name |
| `--type <type>` | File MIME type |
| `--size <size>` | File size in bytes |
| `--parent-id <id>` | Parent folder ID |
| `--json [fields]` | Output JSON |

### Behavior

Checks hash first to avoid uploading duplicates. If a file with the same hash exists, returns the existing file.

### Examples

```bash
# Upload from URL
lh file upload https://example.com/document.pdf

# Upload with metadata
lh file upload https://example.com/image.png --name "logo.png" --type "image/png"
```

---

## file delete

Delete one or more files.

### Usage

```bash
lh file delete <ids...> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `ids` | Yes | File IDs to delete |

### Options

| Option | Description |
| ------ | ----------- |
| `--yes` | Skip confirmation prompt |

### Examples

```bash
# Delete single file
lh file delete file_abc123

# Delete multiple files
lh file delete file_1 file_2 file_3 --yes
```

---

## file edit

Update file info (e.g., move to folder).

### Usage

```bash
lh file edit <id> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `id` | Yes | File ID |

### Options

| Option | Description |
| ------ | ----------- |
| `--parent-id <id>` | Move file to a folder (use "null" to unset) |

---

## file kb-items

View knowledge base items associated with a file.

### Usage

```bash
lh file kb-items <id> [options]
```

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `-L, --limit <n>` | 30 | Maximum number of items |
| `--json [fields]` | - | Output JSON |

---

## file recent

List recently accessed files.

### Usage

```bash
lh file recent [options]
```

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `-L, --limit <n>` | 10 | Number of items |
| `--json [fields]` | - | Output JSON |

---

# Documents

---

## doc list

List documents.

### Usage

```bash
lh doc list [options]
```

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `-L, --limit <n>` | 30 | Maximum number of items |
| `--file-type <type>` | - | Filter by file type |
| `--source-type <type>` | - | Filter by source type (file, web, api, topic) |
| `--json [fields]` | - | Output JSON |

---

## doc view

View a document.

### Usage

```bash
lh doc view <id> [options]
```

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `--json [fields]` | - | Output JSON |

---

## doc create

Create a new document.

### Usage

```bash
lh doc create [options]
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `-t, --title <title>` | Yes | Document title |
| `-b, --body <content>` | No | Document content |
| `-F, --body-file <path>` | No | Read content from file |
| `--parent <id>` | No | Parent document or folder ID |
| `--slug <slug>` | No | Custom slug |
| `--kb <id>` | No | Knowledge base ID to associate with |
| `--file-type <type>` | No | File type (e.g., custom/document, custom/folder) |

### Examples

```bash
# Create with inline content
lh doc create -t "API Reference" -b "# API\n\nDocumentation here..."

# Create from file
lh doc create -t "README" -F ./README.md

# Create and associate with knowledge base
lh doc create -t "Design Doc" -F ./design.md --kb kb_abc123
```

---

## doc batch-create

Batch create documents from a JSON file.

### Usage

```bash
lh doc batch-create <file>
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `file` | Yes | JSON file with document definitions |

---

## doc edit

Edit a document.

### Usage

```bash
lh doc edit <id> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `-t, --title <title>` | New title |
| `-b, --body <content>` | New content |
| `-F, --body-file <path>` | Read new content from file |
| `--parent <id>` | Move to parent document (empty string for root) |
| `--file-type <type>` | Change file type |

---

## doc delete

Delete one or more documents.

### Usage

```bash
lh doc delete <ids...> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--yes` | Skip confirmation prompt |

---

## doc parse

Parse an uploaded file into a document.

### Usage

```bash
lh doc parse <fileId> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `fileId` | Yes | File ID to parse |

### Options

| Option | Description |
| ------ | ----------- |
| `--with-pages` | Preserve page structure |
| `--json [fields]` | Output JSON |

### Examples

```bash
# Parse a PDF
lh doc parse file_abc123

# Parse with page structure
lh doc parse file_abc123 --with-pages
```

---

## doc link-topic

Associate a document with a topic.

### Usage

```bash
lh doc link-topic <docId> <topicId>
```

---

## doc topic-docs

List documents associated with a topic.

### Usage

```bash
lh doc topic-docs <topicId> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--type <type>` | Filter by document type |
| `--json [fields]` | Output JSON |
