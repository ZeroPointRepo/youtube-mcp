---
name: youtube
description: YouTube transcripts, video and channel search, channel browsing and playlist extraction via the bundled TranscriptAPI MCP server. Use when YouTube is or could be relevant — pasted video, channel or playlist links, video IDs, @handles, requests to summarize, quote, transcribe, translate or fact-check a video, research a topic through video, or browse what a creator has posted. Not for uploads, comments or account management.
license: MIT
metadata:
  homepage: https://transcriptapi.com
  publisher: Zero Point Studio
---

# YouTube (TranscriptAPI)

This plugin bundles the hosted **`transcriptapi` MCP server** (`https://transcriptapi.com/mcp`). Its 12 tools are the only data path — never scrape youtube.com and never call the REST API directly from this skill.

**Authentication is automatic.** The MCP server uses OAuth: the first tool call prompts the user to sign in (or create a free account — 100 credits, no card). There is no API key to configure. If tools fail with an auth error, tell the user to complete the sign-in prompt in their client, or re-enable the `transcriptapi` MCP server in settings.

## When to use

**DO use when the user:**

- Pastes a YouTube link or 11-character video ID, or asks to summarize, quote, transcribe, translate or fact-check a video → `get_youtube_transcript`
- Asks what a video says, or wants the spoken content — even without saying "transcript" → `get_youtube_transcript`
- Wants to know what transcript languages are available before spending a credit → `get_youtube_video_info` (free)
- Wants view/like counts, publish date, description, duration, tags, or related videos for a video → `get_video_metadata`
- Wants to find videos, channels, playlists, or movies on a topic → `search_youtube`
- Wants a channel's profile (subscriber count, description, tabs, etc.) → `get_channel_info`
- Names a creator, pastes an `@handle` or channel URL, or asks what a channel posted recently → `get_channel_latest_videos` (free)
- Wants to search *within* a channel → `search_channel_videos`
- Wants a channel's full upload history, Shorts, or live streams → `list_channel_videos`
- Wants the list of playlists on a channel → `list_channel_playlists`
- Wants a channel's community posts → `list_channel_posts`
- Wants a channel's curated Home/podcasts/releases shelves → `get_channel_sections`
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

### `get_youtube_video_info` — FREE
- `video_url` (string, required): full URL, short URL, or 11-character video ID.
- Returns basic metadata (title, author, thumbnail) plus available transcript languages. Call this before `get_youtube_transcript` to pick a language — costs nothing.
- For counts, publish date, description, duration, tags, or related videos, use `get_video_metadata` instead.

### `get_video_metadata` — 1 credit
- `video_url` (string, required); `include` (string array, optional): `"details"` (duration, category, tags, caption tracks) and/or `"related"` (related videos).
- Rich metadata without needing captions — view/like-count text, publish date, structured description, channel summary, thumbnails.

### `search_youtube` — 1 credit per page
- `query` (string, required on first call), `search_type` (string, default `"video"`): `"video"`, `"channel"`, `"playlist"`, or `"movie"` (first call only).
- `sort` (string, default `"relevance"`): `"relevance"` or `"views"`. `upload_date` (string, optional, videos only): `hour`, `today`, `week`, `month`, `year`. `duration` (string, optional, videos only): `short`, `medium`, `long`.
- `continuation` (string, optional): token from a prior call for the next page. Filters apply to the first call only.
- Search returns metadata only. Pick the best results, then pull transcripts for those — don't transcribe everything.

### `get_channel_info` — 1 credit
- `channel` (string, required): `@handle`, channel URL, or `UC…` channel ID.
- Returns the channel's profile (title, handle, verified flag, counts, description, tags, tabs). Check the returned tabs before calling `get_channel_sections` or `list_channel_videos` with a `tab`.

### `get_channel_latest_videos` — FREE
- `channel` (string, required): `@handle`, channel URL, or `UC…` channel ID. No need to resolve a handle first.
- Costs nothing. Prefer it over `list_channel_videos` when recent uploads are enough, and use it freely to check what a creator posted.

### `search_channel_videos` — 1 credit
- `channel` (string, required), `query` (string, required), `continuation` (string, optional).
- Much better than fetching a whole channel and filtering yourself.

### `list_channel_videos` — 1 credit per page
- `channel` (string, required on first call), `tab` (string, default `"videos"`): `videos` (uploads), `shorts`, or `streams`. Repeat the same `tab` when paginating. `continuation` (string, optional).
- Paginated full upload history. Use only when the user genuinely wants the whole catalogue.

### `list_channel_playlists` — 1 credit per page
- `channel` (string, required on first call), `continuation` (string, optional).
- Returns a channel's playlists (id, title, URL, video-count text). Pass an id to `list_playlist_videos` to get its videos.

### `list_channel_posts` — 1 credit per page
- `channel` (string, required on first call), `continuation` (string, optional).
- Returns community (Posts tab) content. Channels without a community tab return an empty list, not an error.

### `get_channel_sections` — 1 credit
- `channel` (string, required), `tab` (string, default `"featured"`): `featured` (Home), `podcasts`, or `releases`.
- Curated, grouped shelves in the channel's own order. `podcasts`/`releases` return empty results on channels that don't have them.

### `list_playlist_videos` — 1 credit per page
- `playlist` (string, required on first call): playlist URL or ID. `continuation` (string, optional).

## Credit hygiene

- `get_channel_latest_videos` is free — reach for it first when checking a channel.
- 1 credit = 1 successful (HTTP 200) request. Failed and rate-limited calls do not consume credits.
- Search first, then transcribe only the videos you actually need. Transcribing a page of search results is the most common way to waste credits.
- Paginate with `continuation` only while the user still needs more.

## Trademark

TranscriptAPI is an independent service and is not affiliated with, endorsed by, or sponsored by YouTube or Google LLC. "YouTube" is a trademark of Google LLC.
