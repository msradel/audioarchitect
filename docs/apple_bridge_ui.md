# AudioArchitect Apple Music Bridge – UI Flow

This document describes a minimal UI flow for **AudioArchitect Apple Music Bridge**, the free, non-commercial app that imports/exports Apple Music playlists using the neutral playlist format.[file:264][file:265]

Key constraints:

- Works only for users with an active **Apple Music subscription** when needed.[web:324][web:327]
- Uses Apple Music API / MusicKit to access playlists and library data for those subscribers.
- Non-commercial; only import/export + basic display (no smart features, no cross-service transfers).

---

## Screen 1 – Connect & Check Subscription

**Purpose:** Let the user connect with Apple Music and verify subscription.

Elements:

- App title:
  - “AudioArchitect Apple Music Bridge”
- Connection area:
  - “Sign in with Apple / Connect to Apple Music” button (following Apple’s design guidelines).
  - Status text:
    - “Not connected”
    - Or “Connected as {Apple ID / display name}”
- Subscription check:
  - Message:
    - If active: “Apple Music subscription: Active”
    - If inactive: “Apple Music subscription is required to access your Apple Music library.”[web:324]

Behavior:

1. On launch, show “Connect to Apple Music”.
2. After auth, check Apple Music subscription status via MusicKit or API.
3. If subscription is active:
   - Proceed to load playlists.
4. If not active:
   - Show clear message and prevent playlist operations.

---

## Screen 2 – List Playlists

**Purpose:** Show the user’s Apple Music playlists and let them select which to export.

Elements:

- Playlist list:
  - Table/grid columns:
    - Playlist name.
    - Track count.
    - Total duration (hh:mm).
  - Optional:
    - Description.
    - Curator/owner (if available via Apple Music API).[web:324]
- Actions:
  - “Reload playlists” button.
  - Checkboxes or multi-select to choose playlists for export.

Behavior:

1. After connection and subscription check, fetch user playlists via Apple Music API/MusicKit.[web:327]
2. Display playlists with basic metadata, enough to identify them.
3. User selects one or more playlists to export.

No analytics, energy graphs, or smart features appear here.

---

## Screen 3 – Export Playlists

**Purpose:** Export selected Apple Music playlists to neutral files.

Elements:

- Summary:
  - “Export X playlist(s)”.
- Export options:
  - Format:
    - JSON (recommended; canonical).[file:265]
    - CSV.
    - TXT (optional, read-only convenience).[file:263]
  - Destination folder:
    - Show current export folder path.
    - “Change…” button for folder picker.
- Actions:
  - “Export” button.
  - “Back” button.

Behavior:

1. User chooses format and confirms folder.
2. On “Export”:
   - For each selected playlist, write `Playlist Name.<ext>` in the chosen folder.
3. Show confirmation:
   - “Exported 2 playlists to C:\Users\...\AudioArchitect\Exports”.

---

## Screen 4 – Import Playlists

**Purpose:** Import playlists from neutral files into Apple Music.

Elements:

- File selection:
  - “Choose file…” button (file picker).
  - Supported formats: JSON, CSV (TXT only if import is implemented and documented).[file:265][file:263]
- Preview:
  - Playlist title from file.
  - Track count.
  - Total duration.
- Destination options:
  - “Create new playlist in Apple Music”.
  - (Optional future) “Update existing playlist”.
  - New playlist name field (defaults to title from file; editable).

- Actions:
  - “Import to Apple Music” button.
  - “Back” button.

Behavior:

1. User picks a neutral-format file.
2. App parses into neutral JSON structure.[file:265]
3. Show preview.
4. On “Import to Apple Music”:
   - Create a new playlist using Apple Music API / MusicKit.
   - Add tracks in the order defined by `position`.
   - Show success message.

---

## Design & Legal Notes

- Apple Music Bridge is:
  - Free and non-commercial.
  - Focused purely on import/export and basic display.
- Requires user consent and valid MusicKit tokens to access personalized data (library, playlists).[web:324][web:327]
- No playback or streaming is implemented; any listening is done through official Apple Music apps.
- Include a clear disclaimer:
  - “This project is not affiliated with or endorsed by Apple or Apple Music.”

The UI should remain simple, mirroring TIDAL Bridge where possible, while respecting Apple’s UX and legal constraints.
