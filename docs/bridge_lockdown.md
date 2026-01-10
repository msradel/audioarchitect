# Bridge Apps Lockdown Specification

This document defines **exactly what Bridge apps are allowed to do** and what they must not do.

Bridge apps include:

- AudioArchitect TIDAL Bridge
- AudioArchitect Apple Music Bridge
- Any future non-commercial service Bridge

They are:

- Free, non-commercial, stand-alone utilities.
- Limited to **one service + neutral formats** (JSON/CSV/TXT).
- Visually consistent with AudioArchitect Premium, but much simpler in behavior.[file:264][file:265]

---

## Allowed Capabilities

### 1. Connect to One Service

- Authenticate with exactly **one** streaming service (e.g., TIDAL for TIDAL Bridge).  
- Use only the official, allowed APIs for:
  - User authentication.
  - Reading user playlists and tracks.[web:19][web:290]

No connections to any other streaming services from a Bridge app.

### 2. Display Playlists and Basic Metadata

Bridges may show:

- Playlist-level info:
  - Name.
  - Track count.
  - Total duration (hh:mm).
  - Optional: description and owner.
- Track-level info:
  - Title.
  - Primary artist.
  - Album.
  - Duration.

Rules:

- Display metadata accurately and legibly, following platform design guidelines when relevant.[web:18]
- No analytics, charts, or scores (no “top artists”, no “energy graphs”, etc.).

### 3. Export Playlists (Service → File)

Bridges may export one or more selected playlists from the service to files in the **neutral formats**:

- JSON (primary format).[file:265]
- CSV.
- TXT (optional, read-only convenience).[file:263]

Behavior:

- User can select one or more playlists to export.
- Each playlist is written to its own file:
  - `Playlist Name.json`
  - `Playlist Name.csv`
  - `Playlist Name.txt`
- Destination:
  - App provides a default export folder (e.g., `AudioArchitect/Exports`).
  - User may choose a different folder via a simple folder picker.

Exports must always follow the neutral schema defined in `docs/playlist_format.md` for JSON/CSV.[file:265]

### 4. Import Playlists (File → Service)

Bridges may import playlists into the service from neutral files:

- Supported input formats:
  - JSON, CSV (TXT only if clearly documented and treated as best-effort).[file:265][file:263]

Behavior:

- User chooses a file via a file picker.
- App parses file into the neutral playlist structure.
- App shows a preview:
  - Playlist title.
  - Track count.
  - Total duration.
- User chooses to:
  - Create a new playlist in the service (default), and optionally edit the newly created playlist name.
- App creates the playlist and adds tracks in the order defined by `position`.

Batch import (multiple files at once) is allowed **only** if the UX makes it clear which files map to which playlists. For v1, single-import per operation is preferred.

---

## Forbidden Capabilities

Bridge apps must **not** do any of the following:

### 1. No Cross-Service Transfers

- No direct transfer between services (e.g., **no** TIDAL → Apple or Apple → TIDAL inside a Bridge).
- A Bridge only knows about:
  - Its one service (e.g., TIDAL).
  - Local files (neutral formats).

Cross-service workflows, if any, must go through:

- Neutral files exported by Bridges, and
- AudioArchitect Premium or other tools that respect platform terms.

### 2. No Smart Features

Bridges must **not** implement:

- Smart randomization modes (shuffle with constraints, energy curves, clustering).
- Analytics or insights (top artists, energy distributions, etc.).
- AI recommendations or automatically generated playlists.

All of these belong strictly in the Premium app.

### 3. No Monetization

Bridge apps are:

- Free to use.
- Non-commercial.

Bridges must **not**:

- Charge for features or access.
- Gate basic import/export behind a paywall.
- Show in-app purchases or ads.

Bridges can mention AudioArchitect Premium in documentation or UI (e.g., “For advanced cleanup and smart randomization, use AudioArchitect Premium”), but:

- Bridges must remain fully useful on their own for import/export.
- Bridges must not cripple basic functionality to force upgrades.

### 4. No Playback or Streaming

Bridges must not:

- Play or stream audio.
- Implement their own audio player.

If linking back to the service is needed:

- Use deep links or URLs that open the official client or web player.

---

## Design & UX Requirements

- Use the same general branding and tone as the Premium app:
  - Consistent fonts, colors, terminology where practical.
- Follow platform-specific branding guidelines when using names/logos:
  - TIDAL, Apple Music, etc. must be referenced according to their rules.[web:18][web:274]
- Include a clear disclaimer, e.g. in README and About screen:
  - “This project is not affiliated with or endorsed by TIDAL/Apple/…”.

---

## Implementation Checklist for Any Bridge

Before releasing or updating a Bridge app, verify:

- [ ] Only one streaming service is used.
- [ ] Only import/export and basic playlist display are implemented.
- [ ] No cross-service logic, no smart randomization, no analytics.
- [ ] No monetization or in-app purchases.
- [ ] JSON/CSV exports match `docs/playlist_format.md`.[file:265]
- [ ] TXT export (if present) matches `docs/playlist_format_txt.md`.[file:263]
- [ ] UI matches `docs/tidal_bridge_ui.md` or similar for the target service.[file:263]
- [ ] Branding and disclaimers align with platform design and legal guidelines.[web:18][web:274]

This document is the reference for what Bridge apps are allowed to do. Any new feature affecting a Bridge must be checked against this specification.
