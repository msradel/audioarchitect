# Spotify Scope for AudioArchitect Premium

This document defines what AudioArchitect Premium is allowed to do with **Spotify**, with a focus on **non-streaming, metadata-only** functionality and permitted commercial use.[web:319][web:326]

AudioArchitect Premium is:

- A **Non-Streaming SDA** under Spotify’s Developer Policy (no audio playback via API/SDK).[web:326]
- A monetized app that works with Spotify metadata (playlists, tracks, libraries).
- Responsible for respecting all Spotify Developer terms and branding rules.[web:129][web:326]

---

## Allowed Capabilities

### 1. User Authentication & Profile

- OAuth-based login with Spotify.
- Access to:
  - User’s Spotify user ID.
  - Basic profile info allowed by scopes (e.g., display name).[web:321]
- No long-term storage of unnecessary personal data.

### 2. Read Playlists & Library

Using Spotify Web API playlist endpoints:[web:319][web:322][web:331]

- Read user-owned and followed playlists:
  - Names, descriptions, owners, images, collaborative flag.
  - Track lists, including:
    - Titles, artists, albums.
    - Durations.
    - Track IDs/URIs.
- Read liked/saved tracks (if needed) via library endpoints.

All reads are used to build the **neutral playlist format** (JSON/CSV) for internal processing and export.[file:265]

### 3. Write / Update Playlists

Using playlist creation and modification endpoints:[web:319][web:323][web:331]

- Create new playlists on behalf of the user.
- Add/remove/reorder tracks in existing playlists (owned by the user).
- Apply Smart Randomization results by:
  - Creating a new playlist with randomized ordering, or
  - Rewriting an existing playlist’s track order.

Rules:

- Only operate on playlists where the user clearly opted in.
- Never modify playlists silently without user action.

### 4. Smart Randomization & Analytics (Metadata Only)

Allowed Premium features:

- Smart randomization using metadata and audio features (where permitted):
  - Track ordering algorithms (shuffle with constraints, energy curves, clustering).[web:259]
  - Deduplication, trimming, target length selection.
- Analytics / insights:
  - Per-playlist stats (duration, number of artists, etc.).
  - High-level metrics derived from metadata (e.g., avg tempo/energy if using audio features).[web:253][web:262]

Constraints:

- Use Spotify audio features APIs within allowed scopes and rate limits.[web:319]
- Do not expose raw internal IDs or data in ways that violate “no repackaging and selling data” rules.[web:129]

### 5. Export / Import with Neutral Format

- Export Spotify playlists to the neutral JSON/CSV format defined in `docs/playlist_format.md`.[file:265]
- Import from neutral format back into Spotify to:
  - Rebuild playlists.
  - Apply smart randomization results.

Spotify Developer Policy explicitly allows enabling users to transfer the metadata of their playlists to another service, as long as other terms are respected.[web:326]

---

## Forbidden Capabilities

### 1. No Streaming or Playback Control

AudioArchitect Premium must **not**:

- Start, stop, or control playback via Spotify Web API or SDK.[web:329][web:332]
- Embed a Spotify Player using Web Playback SDK in a commercial context (without Spotify’s explicit written approval).[web:332]
- Stream full tracks or previews via API and play them in-app.[web:326][web:332]

Playback behavior:

- When the user wants to listen:
  - Provide links/URIs that open the playlist or track in an official Spotify client.
  - Let Spotify handle playback.

### 2. No Mixed-Stream Services

The app must **not**:

- Combine Spotify content streams with streams from other services in a unified player.[web:326]
- Synchronize Spotify sound recordings with other media (video, slideshows, etc.).[web:326]

### 3. No Data Resale or Standalone Metadata Products

- Do not repackage Spotify metadata or user data as a standalone product.[web:129][web:326]
- Do not sell datasets of tracks, playlists, or analytics derived solely from Spotify’s API.

Data should only be used to provide features inside AudioArchitect for the user.

---

## Monetization Boundaries

Spotify permits limited commercial use for **Non-Streaming SDAs**:[web:326]

Allowed for AudioArchitect Premium:

- Charging users for access to the app (subscription or one-time purchase).
- Possibly showing ads/sponsorships in the app UI (not recommended for v1, but allowed in principle).

Not allowed:

- Monetizing any functionality that turns the app into a Streaming SDA (e.g., controlling playback, embedding a commercial player).[web:326]
- Selling metadata or statistics as a separate service.

---

## Branding & UX Requirements

- Follow Spotify Design & Branding Guidelines for name/logo usage.[web:274]
- Clearly state in README and About:
  - “AudioArchitect is not affiliated with or endorsed by Spotify.”
- Show track/playlist metadata accurately and in line with Spotify’s expectations when referencing Spotify content.[web:274]

---

## Implementation Checklist (Spotify)

Before releasing a Spotify-related Premium feature, verify:

- [ ] No playback or playback control via Spotify APIs/SDKs.
- [ ] Only metadata operations (read/write playlists, library).
- [ ] Smart Randomization uses metadata/audio features; no streaming.
- [ ] Exports/imports use the neutral playlist format (JSON/CSV).[file:265]
- [ ] No cross-service streaming, only metadata transfers.
- [ ] Monetization is tied to the app, not to selling Spotify data or playback.
