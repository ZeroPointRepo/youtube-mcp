---
name: youtube
description: YouTube transcripts, video and channel search, channel browsing and playlist extraction via the bundled TranscriptAPI MCP server. Use when YouTube is or could be relevant — pasted video, channel or playlist links, video IDs, @handles, requests to summarize, quote, transcribe, translate or fact-check a video, research a topic through video, or browse what a creator has posted. Not for uploads, comments or account management.
license: MIT
metadata:
  homepage: https://transcriptapi.com
  publisher: Zero Point Studio
---

# YouTube (TranscriptAPI)

This plugin bundles the hosted **`transcriptapi` MCP server** (`https://transcriptapi.com/mcp`). Its six tools are the only data path — never scrape youtube.com and never call the REST API directly from this skill.

**Authentication is automatic.** The MCP server uses OAuth: the first tool call prompts the user to sign in (or create a free account — 100 credits, no card). There is no API key to configure. If tools fail with an auth error, tell the user to complete the sign-in prompt in their client, or re-enable the `transcriptapi` MCP server in settings.

## When to use

**DO use when the user:**

- Pastes a YouTube link or 11-character video ID, or asks to summarize, quote, transcribe, translate or fact-check a video → `get_youtube_transcript`
- Asks what a video says, or wants the spoken content — even without saying "transcript" → `get_youtube_transcript`
- Wants to find videos or channels on a topic → `search_youtube`
- Names a creator, pastes an `@handle` or channel URL, or asks what a channel posted recently → `get_channel_latest_videos` (free)
- Wants to search *within* a channel → `search_channel_videos`
- Wants a channel's full upload history → `list_channel_videos`
- Pastes a playlist link, or wants every video in a series or course → `list_playlist_videos`
- Is researching a topic where talks, lectures, tutorials or reviews are good sources → `search_youtube`, then transcripts of the best hits

**Do NOT use when:**

- A YouTube link appears incidentally (an email signature, an unrelated citation)
- The user is discussing YouTube as a platform rather than asking about specific content
- The user wants to upload, comment, or manage an account — this plugin is read-only

## Tools (exact MCP surface)

### `get_youtube_transcript` — 1 credit
- `video_url` (string, required): full URL (`youtube.com/watch?v=ID`), short URL (`youtu.be/ID`), shorts URL, or a bare 11-character video ID.
- `format` (string, default `"text"`): `"text"` for markdown, `"json"` for per-segment objects with `start` and `duration`.
- `include_timestamp` (boolean, default `true`), `send_metadata` (boolean, default `true`) — metadata adds title, author and thumbnail.
- Use `format="json"` only when you need to cite or seek to exact timestamps; `"text"` is cheaper to reason over.

### `search_youtube` — 1 credit
- `query` (string, required), `search_type` (string, default `"video"`): `"video"` or `"channel"`.
- `continuation` (string, optional): token from a prior call for the next page.
- Search returns metadata only. Pick the best results, then pull transcripts for those — don't transcribe everything.

### `get_channel_latest_videos` — FREE
- `channel` (string, required): `@handle`, channel URL, or `UC…` channel ID. No need to resolve a handle first.
- Costs nothing. Prefer it over `list_channel_videos` when recent uploads are enough, and use it freely to check what a creator posted.

### `search_channel_videos` — 1 credit
- `channel` (string, required), `query` (string, required), `continuation` (string, optional).
- Much better than fetching a whole channel and filtering yourself.

### `list_channel_videos` — 1 credit
- `channel` (string, required), `continuation` (string, optional).
- Paginated full upload history. Use only when the user genuinely wants the whole catalogue.

### `list_playlist_videos` — 1 credit
- `playlist` (string, required): playlist URL or ID. `continuation` (string, optional).

## Credit hygiene

- `get_channel_latest_videos` is free — reach for it first when checking a channel.
- 1 credit = 1 successful (HTTP 200) request. Failed and rate-limited calls do not consume credits.
- Search first, then transcribe only the videos you actually need. Transcribing a page of search results is the most common way to waste credits.
- Paginate with `continuation` only while the user still needs more.

## Trademark

TranscriptAPI is an independent service and is not affiliated with, endorsed by, or sponsored by YouTube or Google LLC. "YouTube" is a trademark of Google LLC.
