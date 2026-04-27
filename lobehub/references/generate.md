# Content Generation

Generate text, images, videos, and audio.

> **Note:** Image, video, and audio generation are asynchronous. Use `gen status` or `gen download` to track progress.

> ⚠️ **ID clarification for `gen status` / `gen download`:**
> These commands take two arguments: `<generationId>` and `<asyncTaskId>`.
> - `generationId` — prefixed with `gen_`, e.g. `gen_abc123`
> - `asyncTaskId` — a UUID printed after `→ Task` in the `gen image` / `gen video` output, e.g. `7ad0eb13-e9a5-4403-8070-1f7fe95b2f95`
>
> Passing `gen_xxx` as the second argument will cause a server error with no useful message.

---

## gen text

Generate text.

### Usage

```bash
lh gen text <prompt> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `-m, --model <model>` | Model ID (default: `openai/gpt-4o-mini`) |
| `-p, --provider <provider>` | Provider name |
| `-s, --system <prompt>` | System prompt |
| `--temperature <n>` | Temperature (0-2) |
| `--max-tokens <n>` | Maximum output tokens |
| `--stream` | Enable streaming output |
| `--json` | Output full JSON response |
| `--pipe` | Read additional context from stdin |

### Examples

```bash
lh gen text "Write a haiku about coding"
cat README.md | lh gen text "summarize this" --pipe
```

---

## gen image

Generate images. Async — returns `generationId` and `asyncTaskId` for tracking.

### Usage

```bash
lh gen image <prompt> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--model <model>` | Model ID (default: `dall-e-3`) |
| `-p, --provider <provider>` | Provider name (default: `openai`) |
| `-n, --num <n>` | Number of images |
| `--width <px>` | Width in pixels |
| `--height <px>` | Height in pixels |
| `--seed <n>` | Random seed |
| `--json` | Output raw JSON |

### Output

```
✓ Image generation started
  Batch ID: gb_xxx
  Generation gen_abc123 → Task 7ad0eb13-e9a5-4403-8070-1f7fe95b2f95
                               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
                               asyncTaskId — use this (not gen_abc123) for status/download

Use "lh gen status <generationId> <asyncTaskId>" to check progress.
```

### Examples

```bash
lh gen image "A sunset over mountains" --model dall-e-3
lh gen image "A cute cat" --model dall-e-3 --provider openai --json
```

---

## gen video

Generate videos. Async — returns `generationId` and `asyncTaskId` for tracking.

### Usage

```bash
lh gen video <prompt> -m <model> -p <provider> [options]
```

### Options

| Option | Required | Description |
| ------ | -------- | ----------- |
| `-m, --model <model>` | Yes | Model ID — use `lh model list <provider>` to find video models |
| `-p, --provider <provider>` | Yes | Provider name |
| `--aspect-ratio <ratio>` | No | e.g. `16:9`, `9:16` |
| `--duration <sec>` | No | Duration in seconds |
| `--resolution <res>` | No | e.g. `720p`, `1080p` |
| `--seed <n>` | No | Random seed |
| `--image <url>` | No | First-frame image URL (image-to-video) |
| `--end-image <url>` | No | Last-frame image URL |
| `--json` | No | Output raw JSON |

### Output

```
✓ Video generation started
  Batch ID: gb_xxx
  Generation gen_abc123 → Task 7ad0eb13-e9a5-4403-8070-1f7fe95b2f95
                               ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
                               asyncTaskId — use this (not gen_abc123) for status/download

Use "lh gen status <generationId> <asyncTaskId>" to check progress.
```

### Examples

```bash
# Find available video models
lh model list volcengine --json | grep -i seedance

# Submit a video generation
lh gen video "A cat on a runway" -m doubao-seedance-2-0-260128 -p volcengine \
  --aspect-ratio 9:16 --duration 5 --resolution 1080p
#   Generation gen_abc123 → Task 7ad0eb13-e9a5-4403-8070-1f7fe95b2f95

# Wait and download (use asyncTaskId — the UUID)
lh gen download gen_abc123 7ad0eb13-e9a5-4403-8070-1f7fe95b2f95 -o result.mp4 --timeout 600
```

---

## gen tts

Generate text-to-speech audio.

### Usage

```bash
lh gen tts <text> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--model <model>` | TTS model |
| `--voice <voice>` | Voice to use |

---

## gen asr

Automatic speech recognition (transcription).

### Usage

```bash
lh gen asr <audioFile> [options]
```

### Options

| Option | Description |
| ------ | ----------- |
| `--model <model>` | ASR model |

---

## gen status

Check generation task status.

> ⚠️ `<asyncTaskId>` is the UUID printed after `→ Task` in the `gen image` / `gen video` output.
> Do **not** pass `gen_xxx` here — that will cause a server error.

### Usage

```bash
lh gen status <generationId> <asyncTaskId> [options]
```

### Arguments

| Argument | Description |
| -------- | ----------- |
| `generationId` | Generation ID (`gen_xxx`) |
| `asyncTaskId` | UUID from `→ Task` in gen output (e.g. `7ad0eb13-xxxx-xxxx-xxxx-xxxxxxxxxxxx`) |

### Options

| Option | Description |
| ------ | ----------- |
| `--json` | Output raw JSON |

### Output

Color-coded status:
- **pending** (cyan) — Task is queued
- **processing** (yellow) — Task is being processed
- **success** (green) — Task finished successfully
- **error** (red) — Task failed

### Examples

```bash
lh gen status gen_abc123 7ad0eb13-e9a5-4403-8070-1f7fe95b2f95
lh gen status gen_abc123 7ad0eb13-e9a5-4403-8070-1f7fe95b2f95 --json
```

---

## gen download

Wait for generation to complete and download the result.

> ⚠️ `<asyncTaskId>` is the UUID printed after `→ Task` in the `gen image` / `gen video` output.
> Do **not** pass `gen_xxx` here — that will cause a server error.

### Usage

```bash
lh gen download <generationId> <asyncTaskId> [options]
```

### Arguments

| Argument | Description |
| -------- | ----------- |
| `generationId` | Generation ID (`gen_xxx`) |
| `asyncTaskId` | UUID from `→ Task` in gen output (e.g. `7ad0eb13-xxxx-xxxx-xxxx-xxxxxxxxxxxx`) |

### Options

| Option | Default | Description |
| ------ | ------- | ----------- |
| `-o, --output <path>` | `<generationId>.<ext>` | Output file path |
| `--interval <sec>` | 5 | Polling interval in seconds |
| `--timeout <sec>` | 300 | Timeout in seconds (0 = no timeout) |

### Examples

```bash
lh gen download gen_abc123 7ad0eb13-e9a5-4403-8070-1f7fe95b2f95
lh gen download gen_abc123 7ad0eb13-e9a5-4403-8070-1f7fe95b2f95 -o ./output/video.mp4 --timeout 600
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
# 1. Start generation — note BOTH IDs in the output
lh gen image "A futuristic city at night" --model dall-e-3
#   Generation gen_abc123 → Task 7ad0eb13-e9a5-4403-8070-1f7fe95b2f95

# 2. (Optional) check status
lh gen status gen_abc123 7ad0eb13-e9a5-4403-8070-1f7fe95b2f95

# 3. Download (pass asyncTaskId — the UUID, not gen_abc123)
lh gen download gen_abc123 7ad0eb13-e9a5-4403-8070-1f7fe95b2f95 -o ./city.png
```

### Generate and Download a Video

```bash
# 1. Find available video models
lh model list volcengine --json | grep -i seedance

# 2. Start generation
lh gen video "A timelapse of clouds" -m doubao-seedance-2-0-260128 -p volcengine \
  --aspect-ratio 16:9 --duration 5 --resolution 1080p
#   Generation gen_def456 → Task a1b2c3d4-xxxx-xxxx-xxxx-xxxxxxxxxxxx

# 3. Wait and download (longer timeout for video)
lh gen download gen_def456 a1b2c3d4-xxxx-xxxx-xxxx-xxxxxxxxxxxx -o ./clouds.mp4 --timeout 600
```
