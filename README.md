![Cover](public/YouTube_Transcript_MCP–TranscriptAPI.png)

[![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en/install-mcp?name=transcript-api&config=eyJ1cmwiOiJodHRwczovL3RyYW5zY3JpcHRhcGkuY29tL21jcCJ9) [<img alt="Install in VS Code" src="https://img.shields.io/badge/VS_Code-Install_TranscriptAPI_MCP-0098FF?style=for-the-badge&logo=visualstudiocode&logoColor=white">](https://insiders.vscode.dev/redirect?url=vscode%3Amcp%2Finstall%3F%7B%22name%22%3A%22transcript-api%22%2C%22url%22%3A%22https%3A%2F%2Ftranscriptapi.com%2Fmcp%22%7D)

# TranscriptAPI MCP - Get YouTube Transcripts Everywhere

> Production-grade YouTube transcript extraction for Claude, ChatGPT, Cursor, and 20+ AI tools.
> 200K+ transcripts processed every day. Trusted by YouTubeToTranscript.com & Recapio.com.

[![Website](https://img.shields.io/badge/Website-transcriptapi.com-FF3B00?style=flat)](https://transcriptapi.com) [![Documentation](https://img.shields.io/badge/Docs-API_Reference-06B6D4?style=flat)](https://transcriptapi.com/docs) [![Swagger](https://img.shields.io/badge/Swagger-Try_API-85EA2D?style=flat&logo=swagger)](https://transcriptapi.com/swagger) [![License](https://img.shields.io/badge/License-MIT-green?style=flat)](./LICENSE)

## ❌ Without TranscriptAPI

- ❌ Manual copy-paste from YouTube's clunky transcript UI
- ❌ No transcript access during AI conversations
- ❌ Context switching between browser tabs wastes time
- ❌ Can't efficiently analyze or compare multiple videos
- ❌ Building your own scraper is unreliable and breaks often

## ✅ With TranscriptAPI

- ✅ Paste any YouTube URL, get instant transcript
- ✅ Works seamlessly inside your AI workflow
- ✅ Analyze, summarize, translate videos in natural conversation
- ✅ Compare multiple videos side-by-side
- ✅ Production-grade reliability with 200K+ daily transcripts

**Quick Demo:**

```txt
Summarize the key points from this video:
https://www.youtube.com/watch?v=dQw4w9WgXcQ
```

TranscriptAPI automatically fetches the transcript and your AI analyzes it instantly.

## Two Integration Paths

|                 | MCP Integration                      | REST API                                                  |
| --------------- | ------------------------------------ | --------------------------------------------------------- |
| **Best For**    | AI assistants & chat interfaces      | Developers & applications                                 |
| **Setup**       | Zero-code, just add URL              | Code integration required                                 |
| **Interaction** | Natural language queries             | Programmatic JSON requests                                |
| **Get Started** | [Installation Guide](#-installation) | [API Documentation →](https://transcriptapi.com/docs/api) |

> **Building an app?** Our REST API gives you full programmatic control with JSON responses, timestamps, and metadata.
> Base URL: `https://transcriptapi.com/api/v2` | [View Swagger UI →](https://transcriptapi.com/swagger)

## 🛠️ Installation

> **Requirements:**
>
> - TranscriptAPI account ([sign up free](https://transcriptapi.com))
> - API Key from [dashboard](https://transcriptapi.com/dashboard/api-keys) OR OAuth (for Claude/ChatGPT)

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

Go to: `Settings` -> `Features` -> `MCP` -> `Add New MCP Server`

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
<summary><b>Install in Claude (Desktop & Web) - Recommended</b></summary>

Claude now supports adding MCP servers directly via the "Custom Connector" UI.

**Quick Setup:**

1. Open Claude Settings (click your profile icon -> Settings)
2. Go to **Connectors** -> **Add custom connector**
3. Enter the following details:
   - **Name:** `TranscriptAPI`
   - **URL:** `https://transcriptapi.com/mcp`
4. Click **Add**, then click **Connect** to authorize via your browser.
5. (Optional) In the connector settings, change permissions to "Allow unsupervised" for seamless usage.

**Full Guide:**
For a comprehensive walkthrough with screenshots, please read our [official Claude Integration Guide](https://transcriptapi.com/docs/mcp/claude).

</details>

<details>
<summary><b>Install in Claude Code (CLI)</b></summary>

Run this command in your terminal:

```sh
claude mcp add --transport http transcript-api https://transcriptapi.com/mcp
```

</details>

<details>
<summary><b>Install in ChatGPT (OAuth)</b></summary>

ChatGPT supports OAuth for secure authentication. You will need to enable **Developer Mode** in ChatGPT settings first.

**Quick Setup (Credentials Optional):**

1. In ChatGPT, go to `Settings` -> `Connected Apps` -> `Add`
2. Enter the MCP Server URL: `https://transcriptapi.com/mcp`
3. **Client ID & Secret are optional:**
   - **Leave them blank** to use Dynamic Client Registration (Recommended/Simpler). ChatGPT will automatically register itself.
   - **(Advanced)** Or enter Client ID & Secret from your [dashboard](https://transcriptapi.com/dashboard/mcp-integration) if you prefer Static Registration.
4. Click **Add** and authorize via the browser popup.

**Full Guide:**
For a step-by-step tutorial on enabling Developer Mode, adding the connector, and authorizing, please read our [official ChatGPT Integration Guide](https://transcriptapi.com/docs/mcp/chatgpt).

</details>

<details>
<summary><b>Install in VS Code</b></summary>

[<img alt="Install in VS Code" src="https://img.shields.io/badge/VS_Code-Install_TranscriptAPI_MCP-0098FF?style=for-the-badge&logo=visualstudiocode&logoColor=white">](https://insiders.vscode.dev/redirect?url=vscode%3Amcp%2Finstall%3F%7B%22name%22%3A%22transcript-api%22%2C%22url%22%3A%22https%3A%2F%2Ftranscriptapi.com%2Fmcp%22%7D)

Add this to your VS Code user settings (`settings.json`):

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
<summary><b>Install in Windsurf</b></summary>

Add this to your Windsurf MCP config (`~/.codeium/windsurf/mcp_config.json`):

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
<summary><b>Install in OpenAI Agent Builder</b></summary>

OpenAI Agent Builder currently requires API Key authentication (OAuth not supported yet).

1. Create a new Agent
2. Under "Actions" or "Tools", add a new **MCP Server**
3. URL: `https://transcriptapi.com/mcp`
4. Auth Type: **API Key**
5. Paste your API Key from the [dashboard](https://transcriptapi.com/dashboard/api-keys)

[View Step-by-Step Guide →](https://transcriptapi.com/docs/mcp/openai-agent-builder)

</details>

<details>
<summary><b>Install in Cline</b></summary>

Add to your Cline MCP settings:

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

Add to your Zed `settings.json`:

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

Add to your Roo Code config:

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

Run via CLI:

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

In Settings -> Tools -> AI Assistant -> MCP:

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

In Plugins -> JSON Config:

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

In Settings -> AI -> MCP:

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

In Settings -> Connectors -> Advanced:

```json
{
  "url": "https://transcriptapi.com/mcp",
  "headers": {
    "Authorization": "Bearer YOUR_API_KEY"
  }
}
```

</details>

## 🔐 Authentication

### API Key Authentication

Simple and universal. Works with every MCP client.

1. Get your API key from [dashboard](https://transcriptapi.com/dashboard/api-keys)
2. Keys start with `sk_` prefix
3. Add to config as Bearer token:

```json
"headers": {
  "Authorization": "Bearer sk_your_api_key_here"
}
```

> **Security Note:** Store keys in environment variables where possible and never commit them to version control.

### OAuth Authentication

Automatic, secure authentication without manual key management.

**Dynamic Client Registration (DCR):**

- Supported by: Claude Desktop, ChatGPT
- Just add the MCP URL - client auto-registers
- No credentials needed
- You'll authorize once via browser redirect

**Static Client Registration:**

- Supported by: ChatGPT (optional/required for some setups)
- Get Client ID + Secret from [MCP Integration Dashboard](https://transcriptapi.com/dashboard/mcp-integration)
- More control over client identity

## 🧰 Available Tools

### `get_youtube_transcript`

Fetches the transcript for a given YouTube video.

| Parameter           | Type    | Default      | Description                                    |
| ------------------- | ------- | ------------ | ---------------------------------------------- |
| `video_url`         | string  | **required** | YouTube URL (full, short) or 11-char video ID  |
| `send_metadata`     | boolean | `true`       | Include video title, author, thumbnail         |
| `format`            | string  | `"text"`     | Output format: `"text"` (markdown) or `"json"` |
| `include_timestamp` | boolean | `true`       | Add timestamps to each segment                 |

**Example Output (Text):**

```markdown
# Metadata

## Title: Rick Astley - Never Gonna Give You Up

## Author: RickAstleyVEVO

# Transcript

[0.0s] Never gonna give you up
[4.12s] Never gonna let you down
```

**Example Output (JSON):**

```json
{
  "transcript": [
    { "text": "Never gonna give you up", "start": 0.0, "duration": 4.12 },
    { "text": "Never gonna let you down", "start": 4.12, "duration": 3.85 }
  ],
  "metadata": { "title": "Rick Astley...", "author_name": "RickAstleyVEVO" }
}
```

## 💡 Use Cases & Prompts

| Use Case                   | Example Prompt                                                |
| -------------------------- | ------------------------------------------------------------- |
| 📝 **Summarization**       | "Summarize the key points from this video: [URL]"             |
| 🔍 **Research**            | "What are the main arguments presented in [URL]?"             |
| 📚 **Study Notes**         | "Create study notes from this lecture: [URL]"                 |
| ⚖️ **Comparison**          | "Compare the perspectives in these two videos: [URL1] [URL2]" |
| 🌐 **Translation**         | "Translate this video's content to Spanish: [URL]"            |
| ✍️ **Content Repurposing** | "Turn this video into a blog post: [URL]"                     |

## 💳 Pricing & Rate Limits

| Plan        | Price    | Credits | Rate Limit  |
| ----------- | -------- | ------- | ----------- |
| **Free**    | $0/month | 100     | 60 req/min  |
| **Starter** | $5/month | 1,000   | 200 req/min |

- **1 Credit** = 1 Successful Request (HTTP 200)
- Failed requests or rate-limited requests do not consume credits.
- [View Pricing](https://transcriptapi.com/#pricing) | [Manage Credits](https://transcriptapi.com/billing)

## 🚨 Troubleshooting

<details>
<summary><b>Authentication Errors (401)</b></summary>

- Verify your API key starts with `sk_`
- Check for extra spaces when copying
- Ensure the key is active in your [dashboard](https://transcriptapi.com/dashboard/api-keys)
- If using OAuth, try re-authorizing
</details>

<details>
<summary><b>No Credits (402)</b></summary>

- Check your credit balance at [dashboard](https://transcriptapi.com/dashboard)
- Purchase more credits or upgrade your plan
</details>

<details>
<summary><b>Video Not Available (404)</b></summary>

- The video might not have captions/subtitles enabled
- The video might be private or age-restricted
- The video might be region-locked
</details>

<details>
<summary><b>Rate Limiting (429)</b></summary>

- Respect the `Retry-After` header
- Implement exponential backoff in your client
- Upgrade to a paid plan for higher limits
</details>

<details>
<summary><b>OAuth Issues</b></summary>

- Clear browser cookies and try again
- For ChatGPT, try switching between Dynamic and Static registration
- Ensure popup blockers aren't preventing the auth window
</details>

## 🤝 Connect with Us

- 🌐 **Website:** [transcriptapi.com](https://transcriptapi.com)
- 📚 **Documentation:** [transcriptapi.com/docs](https://transcriptapi.com/docs)
- 🔧 **API Reference:** [transcriptapi.com/docs/api](https://transcriptapi.com/docs/api)
- 💬 **Contact:** [transcriptapi.com/contact](https://transcriptapi.com/contact)

---

© 2025 Zero Point Studio d.o.o.
