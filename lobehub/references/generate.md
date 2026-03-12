# Content Generation

Generate text, images, videos, and audio.

> **Note:** Image, video, and audio generation are asynchronous. Use `gen status` to check progress and `gen download` to retrieve results.

---

## gen text

Generate text.

### Usage

```bash
lh gen text [options]
```

### Examples

```bash
lh gen text --prompt "Write a haiku about coding"
```

---

## gen image

Generate images.

### Usage

```bash
lh gen image [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--prompt <text>` | Image generation prompt |
| `--model <model>` | Model to use (e.g., dall-e-3) |
| `--size <size>` | Image size |
| `--quality <quality>` | Image quality |
| `--style <style>` | Image style |

### Behavior

1. Submits the generation request
2. Returns a generation ID and task ID
3. Use `gen status` to check progress
4. Use `gen download` to retrieve the result

### Examples

```bash
# Generate an image
lh gen image --prompt "A sunset over mountains" --model dall-e-3

# With specific size
lh gen image --prompt "A cat wearing a hat" --size 1024x1024
```

---

## gen video

Generate videos.

### Usage

```bash
lh gen video [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--prompt <text>` | Video generation prompt |
| `--model <model>` | Model to use |
| `--duration <sec>` | Video duration |

### Behavior

Asynchronous - returns generation ID and task ID. Use `gen status` and `gen download`.

---

## gen tts

Generate text-to-speech audio.

### Usage

```bash
lh gen tts [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--text <text>` | Text to convert to speech |
| `--model <model>` | TTS model |
| `--voice <voice>` | Voice to use |

---

## gen asr

Automatic speech recognition (transcription).

### Usage

```bash
lh gen asr [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--file <path>` | Audio file to transcribe |
| `--model <model>` | ASR model |

---

## gen status

Check generation task status.

### Usage

```bash
lh gen status <generationId> <taskId> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `generationId` | Yes | Generation ID |
| `taskId` | Yes | Task ID |

### Options

| Option | Description |
| ------ | ----------- |
| `--json` | Output raw JSON |

### Output

Shows the current status of the generation task with color-coded results:
- **pending** - Task is queued
- **processing** - Task is being processed
- **completed** - Task finished successfully
- **failed** - Task failed

### Examples

```bash
lh gen status gen_abc123 task_xyz789
lh gen status gen_abc123 task_xyz789 --json
```

---

## gen download

Wait for generation to complete and download the result.

### Usage

```bash
lh gen download <generationId> <taskId> [options]
```

### Arguments

| Argument | Required | Description |
| -------- | -------- | ----------- |
| `generationId` | Yes | Generation ID |
| `taskId` | Yes | Task ID |

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `-o, --output <path>` | - | Output file path |
| `--interval <sec>` | 5 | Polling interval in seconds |
| `--timeout <sec>` | 300 | Timeout in seconds |

### Behavior

1. Polls the task status at the specified interval
2. Downloads the result when complete
3. Times out if task doesn't complete within the timeout period

### Examples

```bash
# Download to auto-named file
lh gen download gen_abc123 task_xyz789

# Download to specific path
lh gen download gen_abc123 task_xyz789 -o ./output/image.png

# Faster polling
lh gen download gen_abc123 task_xyz789 --interval 2 --timeout 600
```

---

## gen delete

Delete a generation record.

### Usage

```bash
lh gen delete <generationId> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--yes` | Skip confirmation prompt |

---

## gen list

List generation topics.

### Usage

```bash
lh gen list [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--json [fields]` | Output JSON |

---

## Typical Workflow

### Generate and Download an Image

```bash
# 1. Start generation
lh gen image --prompt "A futuristic city at night" --model dall-e-3
# Output: Generation started: gen_abc123 task_xyz789

# 2. Check status (optional)
lh gen status gen_abc123 task_xyz789
# Output: Status: processing (45%)

# 3. Download when ready
lh gen download gen_abc123 task_xyz789 -o ./city.png
# Output: Downloaded to ./city.png
```

### Generate and Download a Video

```bash
# 1. Start generation
lh gen video --prompt "A timelapse of clouds moving over mountains"
# Output: Generation started: gen_def456 task_uvw123

# 2. Wait and download (longer timeout for video)
lh gen download gen_def456 task_uvw123 -o ./clouds.mp4 --timeout 600 --interval 10
```
