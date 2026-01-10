# AudioArchitect TIDAL Bridge – UI Flow

This document describes a minimal, user-friendly UI flow for **AudioArchitect TIDAL Bridge**, the free, non-commercial app that imports/exports TIDAL playlists using the neutral playlist format.[20][21]

The Bridge app:

- Only talks to **TIDAL + neutral formats** (JSON/CSV/TXT).
- Does **not** offer smart randomization, analytics, or cross-service transfers.
- Uses the same general branding and display style as the Premium app.

---

## Screen 1 – Connect & Load Playlists

**Purpose:** Let the user connect to TIDAL and see their playlists.

Elements:

- App title:
  - “AudioArchitect TIDAL Bridge”
- Connection area:
  - “Sign in with TIDAL” button (following TIDAL design guidelines).[22]
  - Status text: “Not connected / Connected as {username}”.
- Playlist list:
  - Table/grid with columns:
    - Playlist name.
    - Track count.
    - Total duration (hh:mm).
  - Optional extra columns:
    - Description.
    - Owner.
- Actions:
  - “Reload playlists” button.

Behavior:

1. On launch, show “Sign in with TIDAL”.
2. After successful auth, fetch and display user playlists.
3. User selects one or more playlists (checkboxes or multi-select).

No analytics, scores, or recommendations appear on this screen; only basic metadata needed to identify playlists.

---

## Screen 2 – Export Playlists

**Purpose:** Export selected TIDAL playlists to neutral files.

Elements:

- Summary:
  - “Export X playlist(s)”.
- Export options:
  - Format:
    - JSON (recommended; canonical).[21]
    - CSV.
    - TXT (optional, read-only convenience).[19]
  - Destination folder:
    - Display current export folder path.
    - “Change…” button to open a folder picker.
- Actions:
  - “Export” button.
  - “Back” button (to playlist list).

Behavior:

1. User chooses format (JSON default).
2. User confirms or changes destination folder.
3. On “Export”:
   - For each selected playlist, create a file like:
     - `Playlist Name.json`
     - `Playlist Name.csv`
     - `Playlist Name.txt`
   - Show progress and final success message:
     - “Exported 3 playlists to C:\Users\...\AudioArchitect\Exports”.

Exports must always follow the neutral schema (for JSON/CSV) so Premium and other tools can consume them.[21]

---

## Screen 3 – Import Playlists

**Purpose:** Import playlists from neutral files into TIDAL.

Elements:

- File selection:
  - “Choose file…” button (file picker).
  - Supported formats: JSON, CSV (TXT only if import is implemented; optional).[19][21]
- Preview:
  - Show:
    - Playlist title from file.
    - Track count.
    - Total duration.
- Destination in TIDAL:
  - Radio buttons:
    - “Create new playlist in TIDAL”
    - “Update existing playlist” (optional future)
  - New playlist name (default to title from file; editable).

- Actions:
  - “Import to TIDAL” button.
  - “Back” button.

Behavior:

1. User picks a file.
2. App parses file into the neutral playlist structure.
3. Show preview so user can confirm it is the right playlist.
4. On “Import to TIDAL”:
   - Create (or update) the playlist in TIDAL.
   - Add tracks in order of `position`.
   - Show success message and link to open in TIDAL (if available).[23]

---

## Design Rules for TIDAL Bridge UI

- Keep it **simple and focused**:
  - No cross-service transfers.
  - No sorting/randomization tools.
- Respect TIDAL branding guidelines:
  - Use TIDAL logo and naming only as permitted.[22]
  - Include a note in README: “This project is not affiliated with or endorsed by TIDAL.”
- Match Premium’s general look:
  - Similar colors/fonts where possible.
  - Clear, professional appearance.

This UI flow ensures TIDAL Bridge is a useful, non-commercial companion focused on import/export, while pushing advanced features into AudioArchitect Premium.
