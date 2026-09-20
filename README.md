<!-- mcp-name: com.transcriptapi/youtube-transcript-and-youtube-search -->

<p align="center">
  <a href="https://transcriptapi.com">
    <img src="public/brand/logo-512.png" width="160" height="160" alt="TranscriptAPI" />
  </a>
</p>

<h1 align="center">YouTube Transcript + YouTube Search MCP for AI Agents</h1>

<p align="center">
  <b>The fastest YouTube transcript + YouTube search MCP for AI agents. Try for free.</b><br/>
  12 tools — transcripts, video &amp; channel metadata, video search, channel browsing, in-channel search, playlist extraction, and new-upload polling — for Claude, ChatGPT, Cursor, VS Code, Claude Code, and 20+ clients.
</p>

<p align="center">
  <a href="https://cursor.com/en/install-mcp?name=transcript-api&config=eyJ1cmwiOiJodHRwczovL3RyYW5zY3JpcHRhcGkuY29tL21jcCJ9"><img alt="Install in Cursor" src="https://img.shields.io/badge/Cursor-Install_MCP-000000?style=for-the-badge&logo=cursor&logoColor=white"/></a>
  <a href="https://insiders.vscode.dev/redirect?url=vscode%3Amcp%2Finstall%3F%7B%22name%22%3A%22transcript-api%22%2C%22url%22%3A%22https%3A%2F%2Ftranscriptapi.com%2Fmcp%22%7D"><img alt="Install in VS Code" src="https://img.shields.io/badge/VS_Code-Install_MCP-0098FF?style=for-the-badge&logo=visualstudiocode&logoColor=white"/></a>
</p>

<p align="center">
  <a href="https://transcriptapi.com"><img src="https://img.shields.io/badge/Website-transcriptapi.com-FF3B00?style=for-the-badge" alt="Website"/></a>
  <a href="https://transcriptapi.com/docs"><img src="https://img.shields.io/badge/Docs-API_Reference-06B6D4?style=for-the-badge&logo=readthedocs&logoColor=white" alt="Docs"/></a>
  <a href="https://transcriptapi.com/swagger"><img src="https://img.shields.io/badge/Swagger-Try_API-85EA2D?style=for-the-badge&logo=swagger&logoColor=white" alt="Swagger"/></a>
  <a href="./LICENSE"><img src="https://img.shields.io/badge/License-MIT-4CAF50?style=for-the-badge" alt="MIT License"/></a>
</p>

> **Powering 15M+ transcripts every month** · 500K+ transcripts processed daily · 49ms median response time
> Trusted in production by [youtubetotranscript.com](https://youtubetotranscript.com) (~11M/mo) and [recapio.com](https://recapio.com) (~2.8M/mo).

---

## Why TranscriptAPI MCP

Most YouTube MCP servers do one thing — pull a single transcript. **TranscriptAPI MCP is a full toolkit**: transcripts, video search, channel search, channel browsing, playlist extraction, and free RSS-based upload tracking — all from one remote endpoint, all designed for AI agents.

|                                          | TranscriptAPI MCP | Typical YouTube MCP |
| ---------------------------------------- | ----------------- | ------------------- |
| Hosting                                  | ✅ Remote (no local install) | ❌ Local stdio install |
| Tools                                    | ✅ 12 tools        | ❌ 1 (transcript only) |
| YouTube search                           | ✅ Yes             | ❌ No |
| Channel & playlist extraction            | ✅ Yes             | ❌ No |
| Latest-uploads monitoring (free)         | ✅ Yes             | ❌ No |
| OAuth 2.1 + API key auth                 | ✅ Both            | ❌ Usually neither |
| Production scale (15M+ req/mo)           | ✅ Yes             | ❌ Hobbyist scrapers |
| Works on mobile Claude & web Claude      | ✅ Yes             | ❌ No |
| Agent-friendly error messages            | ✅ Yes             | ❌ Bare HTTP codes |

**Quick taste:**

```txt
Find Andrew Huberman's three most-viewed videos about sleep,
get the transcript of each, and write a 5-bullet comparison.
```

That single prompt uses 3 of our 12 tools — `search_youtube`, `search_channel_videos`, `get_youtube_transcript` — without you writing a line of code.

---

## 🧩 Install as an Agent Plugin <sub>· **easiest**</sub>

This repository root is a conformant **[Agent Plugins 1.0.0](https://agent-plugins.org/specification)** package — the portable format published 2026-08-06 and supported by ChatGPT, Codex, Cursor, GitHub Copilot, Kiro and VS Code. One install gets you the MCP server **and** a bundled `youtube` skill that teaches your agent when to use each tool and how not to waste credits.

```text
plugin.json                    # Agent Plugins 1.0.0 manifest
mcp.json                       # hosted MCP server, streamable-http, OAuth (no keys)
skills/youtube/SKILL.md        # when + how to use the 12 tools
.cursor-plugin/plugin.json     # Cursor plugin manifest, same MCP + skill (+ marketplace.json)
```

**VS Code** — Command Palette → **Chat: Install Plugin From Source**, then paste:

```txt
https://github.com/ZeroPointRepo/youtube-mcp
```

Or register a local clone in `settings.json`:

```json
"chat.pluginLocations": { "/absolute/path/to/youtube-mcp": true }
```

**Cursor** — **Customize** in the sidebar → find the plugin → **Install**. For a local clone:

```bash
git clone https://github.com/ZeroPointRepo/youtube-mcp ~/.cursor/plugins/local/transcriptapi
```

Then **Developer: Reload Window**.

**Add to Cursor** — MCP server only, no clone. Paste this deeplink into your browser:

```txt
cursor://anysphere.cursor-deeplink/mcp/install?name=transcriptapi&config=eyJ1cmwiOiJodHRwczovL3RyYW5zY3JpcHRhcGkuY29tL21jcCJ9
```

**ChatGPT, Codex, GitHub Copilot, Kiro, any other client** — point your client's plugin mechanism at this repository, or at a local clone. Agent Plugins 1.0.0 standardizes the *package format*, not installation, so each client owns its own install flow.

### 30-second example

```txt
Summarize this video for me: https://youtu.be/dQw4w9WgXcQ
```

The agent calls `get_youtube_transcript`, gets the full timestamped transcript and summarizes it. **No API key to configure** — the first call opens an OAuth sign-in (free account, 100 credits, no card). Then try:

```txt
What has @TED posted in the last month?     → get_channel_latest_videos (free)
Find talks on protein folding, summarize the best three.
                                             → search_youtube, then transcripts
```

There are **no credentials in this package** — Agent Plugins 1.0.0 forbids embedded secrets, and authorization is client-managed. Verify the package yourself:

```bash
curl -sO https://agent-plugins.org/schemas/1.0.0/plugin.schema.json
curl -sO https://agent-plugins.org/schemas/1.0.0/mcp.schema.json
npx ajv-cli@5 validate --spec=draft2020 -s plugin.schema.json -d plugin.json
npx ajv-cli@5 validate --spec=draft2020 -s mcp.schema.json    -d mcp.json
```

---

## 🛠️ Quick Install

> **Requirements:**
>
> - A TranscriptAPI account ([sign up free](https://transcriptapi.com) — first 100 credits free)
> - An API key from your [dashboard](https://transcriptapi.com/dashboard/api-keys) **OR** use OAuth (Claude, ChatGPT)

> **Recommended: Add a Rule to Auto-Invoke TranscriptAPI**
>
> Add this rule to your AI client so you don't need to explicitly ask for transcripts:
>
> ```txt
> When I share a YouTube URL, automatically use the TranscriptAPI MCP tool
> to fetch the transcript before responding. This applies to any video analysis,
> summarization, or question about YouTube content.
> ```

<details>
<summary><b>Install in Cursor (One-Click / Manual)</b></summary>

**One-Click Install:**

[![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en/install-mcp?name=transcript-api&config=eyJ1cmwiOiJodHRwczovL3RyYW5zY3JpcHRhcGkuY29tL21jcCJ9)

**Manual Configuration:**

Go to: `Settings` → `Features` → `MCP` → `Add New MCP Server`

- **Name:** `transcript-api`
- **Type:** `SSE` (Remote)
- **URL:** `https://transcriptapi.com/mcp`

Or edit `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "transcript-api": {
      "url": "https://transcriptapi.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

</details>

<details>
<summary><b>Install in Claude (Desktop & Web) — Recommended</b></summary>

Claude supports adding MCP servers directly via the "Custom Connector" UI.

**Quick Setup:**

1. Open Claude Settings (click your profile icon → Settings)
2. Go to **Connectors** → **Add custom connector**
3. Enter the following details:
   - **Name:** `TranscriptAPI`
   - **URL:** `https://transcriptapi.com/mcp`
4. Click **Add**, then click **Connect** to authorize via your browser.
5. (Optional) In the connector settings, change permissions to "Allow unsupervised" for seamless usage.

**Full Guide:** [Claude Integration Guide →](https://transcriptapi.com/docs/mcp/claude)

</details>

<details>
<summary><b>Install in Claude Code (CLI)</b></summary>

```sh
claude mcp add --transport http transcript-api https://transcriptapi.com/mcp
```

</details>

<details>
<summary><b>Install in ChatGPT</b></summary>

ChatGPT supports OAuth for secure authentication. Enable **Developer Mode** in ChatGPT settings first.

**Quick Setup:**

1. In ChatGPT, go to `Settings` → `Connected Apps` → `Add`
2. Enter the MCP Server URL: `https://transcriptapi.com/mcp`
3. **Client ID & Secret are optional:**
   - **Leave them blank** to use Dynamic Client Registration (recommended/simpler).
   - **(Advanced)** Or enter Client ID & Secret from your [dashboard](https://transcriptapi.com/dashboard/mcp-integration) for static registration.
4. Click **Add** and authorize via the browser popup.

**Full Guide:** [ChatGPT Integration Guide →](https://transcriptapi.com/docs/mcp/chatgpt)

</details>

<details>
<summary><b>Install in VS Code</b></summary>

[<img alt="Install in VS Code" src="https://img.shields.io/badge/VS_Code-Install_TranscriptAPI_MCP-0098FF?style=for-the-badge&logo=visualstudiocode&logoColor=white">](https://insiders.vscode.dev/redirect?url=vscode%3Amcp%2Finstall%3F%7B%22name%22%3A%22transcript-api%22%2C%22url%22%3A%22https%3A%2F%2Ftranscriptapi.com%2Fmcp%22%7D)

Or add this to VS Code user settings (`settings.json`):

```json
"mcp.servers": {
  "transcript-api": {
    "type": "http",
    "url": "https://transcriptapi.com/mcp",
    "headers": {
      "Authorization": "Bearer YOUR_API_KEY"
    }
  }
}
```

</details>

<details>
<summary><b>Install in OpenAI Agent Builder</b></summary>

OpenAI Agent Builder currently requires API Key authentication (OAuth not yet supported).

1. Create a new Agent
2. Under "Actions" or "Tools", add a new **MCP Server**
3. URL: `https://transcriptapi.com/mcp`
4. Auth Type: **API Key**
5. Paste your API Key from the [dashboard](https://transcriptapi.com/dashboard/api-keys)

[Step-by-Step Guide →](https://transcriptapi.com/docs/mcp/openai-agent-builder)

</details>

<details>
<summary><b>Install in Windsurf</b></summary>

Add to `~/.codeium/windsurf/mcp_config.json`:

```json
{
  "mcpServers": {
    "transcript-api": {
      "serverUrl": "https://transcriptapi.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

</details>

<details>
<summary><b>Install in Cline</b></summary>

```json
{
  "mcpServers": {
    "transcript-api": {
      "url": "https://transcriptapi.com/mcp",
      "type": "streamableHttp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

</details>

<details>
<summary><b>Install in Zed</b></summary>

In Zed `settings.json`:

```json
{
  "context_servers": {
    "transcript-api": {
      "source": "remote",
      "url": "https://transcriptapi.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

</details>

<details>
<summary><b>Install in Roo Code</b></summary>

```json
{
  "mcpServers": {
    "transcript-api": {
      "type": "streamable-http",
      "url": "https://transcriptapi.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

</details>

<details>
<summary><b>Install in Amp</b></summary>

```sh
amp mcp add transcript-api https://transcriptapi.com/mcp --header "Authorization: Bearer YOUR_API_KEY"
```

</details>

<details>
<summary><b>Install in Augment Code</b></summary>

In `settings.json` under `augment.advanced`:

```json
"augment.advanced": {
  "mcpServers": [
    {
      "name": "transcript-api",
      "url": "https://transcriptapi.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  ]
}
```

</details>

<details>
<summary><b>Install in Kilo Code</b></summary>

In `.kilocode/mcp.json`:

```json
{
  "mcpServers": {
    "transcript-api": {
      "type": "streamable-http",
      "url": "https://transcriptapi.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

</details>

<details>
<summary><b>Install in JetBrains AI Assistant</b></summary>

In Settings → Tools → AI Assistant → MCP:

```json
{
  "mcpServers": {
    "transcript-api": {
      "url": "https://transcriptapi.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

</details>

<details>
<summary><b>Install in Gemini CLI</b></summary>

In `~/.gemini/settings.json`:

```json
{
  "mcpServers": {
    "transcript-api": {
      "httpUrl": "https://transcriptapi.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

</details>

<details>
<summary><b>Install in Qwen Coder</b></summary>

In `~/.qwen/settings.json`:

```json
{
  "mcpServers": {
    "transcript-api": {
      "httpUrl": "https://transcriptapi.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

</details>

<details>
<summary><b>Install in Google Antigravity</b></summary>

```json
{
  "mcpServers": {
    "transcript-api": {
      "serverUrl": "https://transcriptapi.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

</details>

<details>
<summary><b>Install in Trae</b></summary>

```json
{
  "mcpServers": {
    "transcript-api": {
      "url": "https://transcriptapi.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

</details>

<details>
<summary><b>Install in LM Studio</b></summary>

In `mcp.json`:

```json
{
  "mcpServers": {
    "transcript-api": {
      "url": "https://transcriptapi.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

</details>

<details>
<summary><b>Install in BoltAI</b></summary>

In Plugins → JSON Config:

```json
{
  "mcpServers": {
    "transcript-api": {
      "url": "https://transcriptapi.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_API_KEY"
      }
    }
  }
}
```

</details>

<details>
<summary><b>Install in Warp</b></summary>

In Settings → AI → MCP:

```json
{
  "transcript-api": {
    "url": "https://transcriptapi.com/mcp",
    "headers": {
      "Authorization": "Bearer YOUR_API_KEY"
    }
  }
}
```

</details>

<details>
<summary><b>Install in Perplexity Desktop</b></summary>

In Settings → Connectors → Advanced:

```json
{
  "url": "https://transcriptapi.com/mcp",
  "headers": {
    "Authorization": "Bearer YOUR_API_KEY"
  }
}
```

</details>

---

## 🔐 Authentication

### API Key

Simple and universal. Works with every MCP client.

1. Get your API key from your [dashboard](https://transcriptapi.com/dashboard/api-keys)
2. Keys start with `sk_` prefix
3. Add to config as a Bearer token:

```json
"headers": {
  "Authorization": "Bearer sk_your_api_key_here"
}
```

> **Security:** Store keys in environment variables where possible and never commit them to version control.

### OAuth 2.1

Automatic, secure authentication without manual key management.

**Dynamic Client Registration (DCR):**

- Supported by: Claude Desktop, Claude Web, ChatGPT
- Just add the MCP URL — client auto-registers
- No credentials needed
- You'll authorize once via browser redirect

**Static Client Registration:**

- Supported by: ChatGPT (optional)
- Get Client ID + Secret from the [MCP Integration Dashboard](https://transcriptapi.com/dashboard/mcp-integration)
- More control over client identity

Full reference: [Authentication docs →](https://transcriptapi.com/docs/mcp/claude)

---

## 🧰 Available Tools

All 12 tools are exposed automatically once you connect. **1 credit = 1 successful (HTTP 200) request.** Failed/rate-limited calls do not consume credits.

> **Which video tool?** Use `get_youtube_video_info` (free) to discover transcript languages before fetching a transcript. Use `get_video_metadata` (1 credit) for view/like counts, publish date, description, duration, tags, or related videos.

### 1. `get_youtube_transcript`

Fetch the transcript for any YouTube video — as markdown (with metadata) or structured JSON. Drop the output straight into summarizers, search indexes, or AI pipelines.

| Parameter           | Type    | Default      | Description                                    |
| ------------------- | ------- | ------------ | ---------------------------------------------- |
| `video_url`         | string  | **required** | YouTube URL (full or short) or 11-char video ID |
| `send_metadata`     | boolean | `true`       | Include video title, author, thumbnail         |
| `format`            | string  | `"text"`     | `"text"` (markdown) or `"json"`                |
| `include_timestamp` | boolean | `true`       | Add timestamps to each segment                 |

**Cost:** 1 credit per successful request.

**Example output (markdown):**

```markdown
# Metadata

## Title: Rick Astley - Never Gonna Give You Up
## Author: RickAstleyVEVO

# Transcript

[0.0s] Never gonna give you up
[4.12s] Never gonna let you down
```

**Example output (JSON):**

```json
{
  "transcript": [
    { "text": "Never gonna give you up", "start": 0.0, "duration": 4.12 },
    { "text": "Never gonna let you down", "start": 4.12, "duration": 3.85 }
  ],
  "metadata": { "title": "Rick Astley...", "author_name": "RickAstleyVEVO" }
}
```

---

### 2. `get_youtube_video_info` <sub>· **FREE**</sub>

Basic metadata (title, author, thumbnail) plus the list of available transcript languages — call this before `get_youtube_transcript` to pick a language. No credit used.

| Parameter   | Type   | Default      | Description                                     |
| ----------- | ------ | ------------ | ------------------------------------------------ |
| `video_url` | string | **required** | YouTube URL (full or short) or 11-char video ID |

**Cost:** Free.

For view/like counts, publish date, description, duration, tags, or related videos, use `get_video_metadata` instead.

---

### 3. `get_video_metadata`

Rich video metadata without needing captions: title, view/like-count text, publish date, structured description + links, uploading-channel summary, and thumbnails. Optional `include` extras pull heavier player-sourced data (duration, category, tags, caption-track inventory) and related videos.

| Parameter   | Type     | Default | Description                                                                                          |
| ----------- | -------- | ------- | ----------------------------------------------------------------------------------------------------- |
| `video_url` | string   | **required** | YouTube URL (full or short) or 11-char video ID                                                  |
| `include`   | string[] | _none_  | Extras: `"details"` (duration, category, tags, caption tracks) and/or `"related"` (related videos)     |

**Cost:** 1 credit per successful request.

**Example prompt:**

```txt
Get the view count, publish date, and tags for https://youtu.be/dQw4w9WgXcQ.
```

---

### 4. `search_youtube`

Search YouTube for videos, channels, playlists, or movies. Filter by type, sort, upload date, or duration, and paginate with a continuation token — perfect for discovery, research, and building content pipelines.

| Parameter      | Type   | Default      | Description                          |
| -------------- | ------ | ------------ | ------------------------------------ |
| `query`        | string | **required** (first call) | Search query            |
| `search_type`  | string | `"video"`    | `"video"`, `"channel"`, `"playlist"`, or `"movie"` (first call only) |
| `sort`         | string | `"relevance"` | First-page sort: `"relevance"` or `"views"` |
| `upload_date`  | string | _none_       | First-page upload window (videos only): `hour`, `today`, `week`, `month`, `year` |
| `duration`     | string | _none_       | First-page duration bucket (videos only): `short` (under 4m), `medium` (4–20m), `long` (over 20m) |
| `continuation` | string | `null`       | Token from a prior call for next page |

**Cost:** 1 credit per page (~20 results per page).

**Example prompt:**

```txt
Search YouTube for "transformer architecture explained" and pick the
top 3 results by relevance.
```

---

### 5. `get_channel_info`

A channel's profile: title, `@handle`, verified flag, subscriber/video-count text, description, keywords, tags, thumbnails, banners, and the tabs it exposes. Not paginated.

| Parameter | Type   | Default      | Description                                  |
| --------- | ------ | ------------ | ---------------------------------------------- |
| `channel` | string | **required** | `@handle`, channel URL, or `UC…` channel ID |

**Cost:** 1 credit per successful request.

Check the returned tabs before calling `get_channel_sections` or `list_channel_videos` with a `tab`.

---

### 6. `get_channel_latest_videos` <sub>· **FREE**</sub>

Get the ~15 most recent uploads from any channel via RSS — no credits required. Perfect for monitoring, daily recaps, or triggering downstream pipelines.

| Parameter | Type   | Default      | Description                                  |
| --------- | ------ | ------------ | -------------------------------------------- |
| `channel` | string | **required** | `@handle`, channel URL, or `UC…` channel ID |

**Cost:** Free.

**Example prompt:**

```txt
Every morning, list new uploads from @lexfridman and @hubermanlab.
```

---

### 7. `search_channel_videos`

Search inside one specific channel for videos matching a query. Great for researching a creator's content or finding niche topics in large channels.

| Parameter      | Type   | Default      | Description                          |
| -------------- | ------ | ------------ | ------------------------------------ |
| `channel`      | string | **required** | `@handle`, channel URL, or `UC…` ID |
| `query`        | string | **required** | Query to search within the channel   |
| `continuation` | string | `null`       | Pagination token                     |

**Cost:** 1 credit per page (~30 results per page).

**Example prompt:**

```txt
On Andrew Huberman's channel, find every video about sleep.
```

---

### 8. `list_channel_videos`

List a channel's feed with pagination. Use `tab` to choose the uploads feed (default, ~100/page), Shorts, or live streams (~48/page). Ideal for building databases, bulk transcript extraction, or auditing a channel's full content library.

| Parameter      | Type   | Default      | Description                          |
| -------------- | ------ | ------------ | ------------------------------------ |
| `channel`      | string | **required** (first call) | `@handle`, channel URL, or `UC…` ID |
| `tab`          | string | `"videos"`   | Which feed: `videos` (uploads), `shorts`, or `streams` (live). Repeat the same `tab` when paginating. |
| `continuation` | string | `null`       | Pagination token                     |

**Cost:** 1 credit per page.

---

### 9. `list_channel_playlists`

Paginated list of the playlists on a channel (id, title, URL, video-count text, thumbnails). Pass a returned playlist id to `list_playlist_videos` to get its videos.

| Parameter      | Type   | Default | Description                                          |
| -------------- | ------ | ------- | ------------------------------------------------------ |
| `channel`      | string | **required** (first call) | `@handle`, channel URL, or `UC…` ID |
| `continuation` | string | `null`  | Pagination token                                        |

**Cost:** 1 credit per page.

---

### 10. `list_channel_posts`

Paginated list of a channel's community (Posts tab) content — text, publish time, like-count text, and attachments (image, multi-image, video, playlist, or poll). Channels without a community tab return an empty results list, not an error.

| Parameter      | Type   | Default | Description                                          |
| -------------- | ------ | ------- | ------------------------------------------------------ |
| `channel`      | string | **required** (first call) | `@handle`, channel URL, or `UC…` ID |
| `continuation` | string | `null`  | Pagination token                                        |

**Cost:** 1 credit per page.

---

### 11. `get_channel_sections`

The curated, grouped sections of a channel page — titled shelves of videos, playlists, shorts, or featured channels, in the channel's own order. Not paginated.

| Parameter | Type   | Default      | Description                                                     |
| --------- | ------ | ------------ | ---------------------------------------------------------------- |
| `channel` | string | **required** | `@handle`, channel URL, or `UC…` ID |
| `tab`     | string | `"featured"` | Which curated page: `featured` (Home), `podcasts`, or `releases` |

**Cost:** 1 credit per successful request.

`podcasts` and `releases` exist only on channels that have them (empty results otherwise).

---

### 12. `list_playlist_videos`

Get every video in a YouTube playlist (PL/UU/LL/FL/OL IDs supported). Process entire courses, lecture series, or curated collections in a single call.

| Parameter      | Type   | Default      | Description                  |
| -------------- | ------ | ------------ | ---------------------------- |
| `playlist`     | string | **required** (first call) | Playlist URL or playlist ID |
| `continuation` | string | `null`       | Pagination token             |

**Cost:** 1 credit per page (~100 results per page).

---

## 💡 Use Cases & Prompts

| Use Case                       | Example Prompt                                                                                  |
| ------------------------------ | ----------------------------------------------------------------------------------------------- |
| 📝 **Summarize a video**       | "Summarize the key points from this video: [URL]"                                               |
| 🔍 **Research a topic**        | "Search YouTube for the 5 most-watched videos on neural radiance fields; summarize each."        |
| 🧠 **Study notes**             | "Create study notes from this MIT lecture series playlist: [PLAYLIST URL]"                       |
| ⚖️ **Compare perspectives**    | "Compare arguments in these two videos: [URL1] [URL2]"                                          |
| 🌐 **Translate**               | "Translate this video's transcript to Spanish: [URL]"                                           |
| ✍️ **Repurpose content**        | "Turn this video into a 1,500-word blog post: [URL]"                                            |
| 📡 **Monitor a creator**       | "Each morning, list new uploads from @hubermanlab and tell me which to watch."                  |
| 🏛️ **Build a content database** | "Pull every video from @veritasium and store title + transcript."                              |
| 🎯 **Competitor analysis**      | "Search inside @MKBHD for any video about [competitor product] and summarize the takeaways."   |

---

## 💳 Pricing & Rate Limits

| Plan                | Price             | Credits      | Rate Limit  |
| ------------------- | ----------------- | ------------ | ----------- |
| **Free**            | $0 (one-time)     | 100          | 60 req/min  |
| **Starter Monthly** | $5/month          | 1,000/month  | 200 req/min |
| **Starter Annual**  | $54/year ($4.50/mo) | 1,000/month  | 300 req/min |

- **1 Credit** = 1 successful request (HTTP 200)
- Failed and rate-limited requests do **not** consume credits.
- `get_channel_latest_videos` is **free** (no credits charged).
- [View pricing](https://transcriptapi.com/#pricing) · [Manage credits](https://transcriptapi.com/billing)

---

## 🚨 Troubleshooting

<details>
<summary><b>Authentication errors (401)</b></summary>

- Verify your API key starts with `sk_`
- Check for extra spaces when copying
- Ensure the key is active in your [dashboard](https://transcriptapi.com/dashboard/api-keys)
- If using OAuth, try re-authorizing
</details>

<details>
<summary><b>No credits (402)</b></summary>

- Check your credit balance at the [dashboard](https://transcriptapi.com/dashboard)
- Purchase more credits or upgrade your plan
</details>

<details>
<summary><b>Video not available (404)</b></summary>

- The video might not have captions/subtitles enabled
- The video might be private or age-restricted
- The video might be region-locked
</details>

<details>
<summary><b>Rate limiting (429)</b></summary>

- Respect the `Retry-After` header
- Implement exponential backoff in your client
- Upgrade to a paid plan for higher limits
</details>

<details>
<summary><b>OAuth issues</b></summary>

- Clear browser cookies and try again
- For ChatGPT, try switching between Dynamic and Static registration
- Ensure popup blockers aren't preventing the auth window
</details>

---

## 🔗 Also available as a REST API

Building an app instead of an agent? The same backend ships as a JSON REST API.

|                 | MCP                         | REST API                                                  |
| --------------- | --------------------------- | --------------------------------------------------------- |
| **Best for**    | AI assistants & agents      | Apps & backend services                                   |
| **Setup**       | Add a URL                   | Code integration                                          |
| **Get started** | This README                 | [API docs →](https://transcriptapi.com/docs/api) · [Swagger →](https://transcriptapi.com/swagger) |

Base URL: `https://transcriptapi.com/api/v2`

---

## 🤝 Connect

- 🌐 **Website:** [transcriptapi.com](https://transcriptapi.com)
- 📚 **Docs:** [transcriptapi.com/docs](https://transcriptapi.com/docs)
- 🔧 **API Reference:** [transcriptapi.com/docs/api](https://transcriptapi.com/docs/api)
- 🤖 **MCP Setup Guides:** [Claude](https://transcriptapi.com/docs/mcp/claude) · [ChatGPT](https://transcriptapi.com/docs/mcp/chatgpt) · [OpenAI Agent Builder](https://transcriptapi.com/docs/mcp/openai-agent-builder)
- 💬 **Contact:** [transcriptapi.com/contact](https://transcriptapi.com/contact)
- 📂 **Listed in:** [awesome-agent-plugins](https://github.com/ZeroPointRepo/awesome-agent-plugins), our directory of verified Agent Plugins on the open standard

---

## 📋 MCP Registry

This server is published to the official [Model Context Protocol Registry](https://registry.modelcontextprotocol.io/) under the name:

```
com.transcriptapi/youtube-transcript-and-youtube-search
```

---

<p align="center">
  <sub>© 2026 Zero Point Studio d.o.o. · Released under the <a href="./LICENSE">MIT License</a></sub>
</p>
