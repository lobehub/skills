# Knowledge Base Management

Manage knowledge bases, folders, documents, and files for your agents.

---

## kb list

List knowledge bases.

### Usage

```bash
lh kb list [options]
```

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `--json [fields]` | - | Output JSON |

### Examples

```bash
lh kb list
lh kb list --json
```

---

## kb view

View a knowledge base with recursive file listing.

### Usage

```bash
lh kb view <id> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `id` | Yes | Knowledge base ID |

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `--json [fields]` | - | Output JSON |

### Output

Displays the knowledge base details and a tree view of all folders and files.

---

## kb create

Create a knowledge base.

### Usage

```bash
lh kb create [options]
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `-n, --name <name>` | Yes | Knowledge base name |
| `-d, --description <desc>` | No | Description |
| `--avatar <url>` | No | Avatar URL |

### Examples

```bash
# Create with name only
lh kb create -n "Research Papers"

# Create with description and avatar
lh kb create -n "Product Docs" -d "Internal product documentation" --avatar https://example.com/icon.png
```

---

## kb edit

Update a knowledge base.

### Usage

```bash
lh kb edit <id> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `id` | Yes | Knowledge base ID |

### Options

| Option | Description |
| ------ | ----------- |
| `-n, --name <name>` | New name |
| `-d, --description <desc>` | New description |
| `--avatar <url>` | New avatar URL |

---

## kb delete

Delete a knowledge base.

### Usage

```bash
lh kb delete <id> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `id` | Yes | Knowledge base ID |

### Options

| Option | Description |
| ------ | ----------- |
| `--remove-files` | Also delete associated files |
| `--yes` | Skip confirmation prompt |

### Examples

```bash
# Delete knowledge base only
lh kb delete kb_abc123

# Delete with associated files
lh kb delete kb_abc123 --remove-files --yes
```

---

## kb upload

Upload a file to a knowledge base.

### Usage

```bash
lh kb upload <knowledgeBaseId> <filePath> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `knowledgeBaseId` | Yes | Knowledge base ID |
| `filePath` | Yes | Local file path |

### Options

| Option | Description |
| ------ | ----------- |
| `--parent <parentId>` | Parent folder ID |

### Behavior

1. Computes SHA-256 hash of the file
2. Checks if file already exists (deduplication)
3. Uploads to S3 via presigned URL
4. Creates file record in knowledge base

### Examples

```bash
# Upload to root
lh kb upload kb_abc123 ./document.pdf

# Upload to a folder
lh kb upload kb_abc123 ./report.docx --parent folder_xyz
```

---

## kb mkdir

Create a folder in a knowledge base.

### Usage

```bash
lh kb mkdir <knowledgeBaseId> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `knowledgeBaseId` | Yes | Knowledge base ID |

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `-n, --name <name>` | Yes | Folder name |
| `--parent <parentId>` | No | Parent folder ID |

### Examples

```bash
# Create folder at root
lh kb mkdir kb_abc123 -n "Research"

# Create subfolder
lh kb mkdir kb_abc123 -n "2024" --parent folder_research
```

---

## kb create-doc

Create a document in a knowledge base.

### Usage

```bash
lh kb create-doc <knowledgeBaseId> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `knowledgeBaseId` | Yes | Knowledge base ID |

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `-t, --title <title>` | Yes | Document title |
| `-c, --content <content>` | No | Document content (text) |
| `--parent <parentId>` | No | Parent folder ID |

### Examples

```bash
# Create empty document
lh kb create-doc kb_abc123 -t "Meeting Notes"

# Create with content
lh kb create-doc kb_abc123 -t "README" -c "# Welcome\n\nThis is the documentation."

# Create in a folder
lh kb create-doc kb_abc123 -t "Design Doc" --parent folder_xyz
```

---

## kb add-files

Add existing files to a knowledge base.

### Usage

```bash
lh kb add-files <knowledgeBaseId> --ids <ids...>
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `knowledgeBaseId` | Yes | Knowledge base ID |

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `--ids <ids...>` | Yes | File IDs to add |

### Examples

```bash
lh kb add-files kb_abc123 --ids file_1 file_2 file_3
```

---

## kb remove-files

Remove files from a knowledge base.

### Usage

```bash
lh kb remove-files <knowledgeBaseId> --ids <ids...> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--ids <ids...>` | File IDs to remove (required) |
| `--yes` | Skip confirmation prompt |

---

## kb move

Move a file or document to a different folder.

### Usage

```bash
lh kb move <id> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `id` | Yes | File or document ID |

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `--parent <parentId>` | - | Target folder ID (omit to move to root) |
| `--type <type>` | file | Item type: file or doc |

### Examples

```bash
# Move file to a folder
lh kb move file_abc123 --parent folder_xyz

# Move document to root
lh kb move doc_abc123 --type doc

# Move file to another folder
lh kb move file_abc123 --parent folder_new
```
