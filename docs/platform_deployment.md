# Platform Deployment Overview

## AudioArchitect Ecosystem

AudioArchitect is split into two repositories:

### Public Repository: [audioarchitect](https://github.com/msrproduct/audioarchitect)
**Purpose:** Non-commercial, open-source tools and specifications

**Contains:**
- Neutral playlist formats (JSON/CSV/TXT)
- Platform integration bridges (TIDAL, Spotify, Apple Music)
- API specifications and documentation
- Community tools and utilities

**License:** Open source (non-commercial)

### Private Repository: audioarchitect-premium
**Purpose:** Commercial desktop/mobile/web application

**Contains:**
- Desktop application (Electron + Python)
- Mobile applications (iOS/Android via Capacitor)
- Progressive Web App (PWA)
- Smart randomization algorithms
- Premium features and analytics

**License:** Proprietary

## How They Work Together

```
┌────────────────────────────┐
│  audioarchitect (Public)    │
│                            │
│  • Playlist formats        │
│  • Platform bridges        │
│  • Documentation           │
│  • Community tools         │
└────────────┬───────────────┘
             │
             │ Uses formats & bridges
             │
             ↓
┌────────────────────────────┐
│ audioarchitect-premium     │
│        (Private)            │
│                            │
│  • Desktop app (Electron)  │
│  • Mobile apps (Capacitor)│
│  • Web app (PWA)          │
│  • Smart features         │
└────────────────────────────┘
```

## Deployment Strategy: Client-Side First

### Core Philosophy

**All processing happens on the user's device** - no servers required.

**Benefits:**
- $0/month hosting costs
- User data never leaves their device
- Unlimited scalability
- Privacy-first architecture
- Compliant with streaming service policies

### Three-Phase Rollout

#### Phase 1: Desktop Application
**Platform:** Windows, macOS, Linux  
**Technology:** Electron + Python  
**Distribution:** GitHub Releases, direct download  
**Cost:** $0/month hosting

**Why Desktop First?**
- Full file system access
- Leverage Python for rapid development
- Best performance for power users
- Validate features before mobile/web

#### Phase 2: Mobile Applications
**Platform:** iOS, Android  
**Technology:** Capacitor + JavaScript  
**Distribution:** Apple App Store, Google Play Store  
**Cost:** $99/year (Apple) + $25 one-time (Google)

**Key Change:** Python logic ported to JavaScript (required for mobile)

#### Phase 3: Progressive Web App
**Platform:** Any modern browser  
**Technology:** PWA + JavaScript (shared with mobile)  
**Distribution:** Direct URL (audioarchitect.app)  
**Cost:** $0/month (Vercel/Netlify free tier)

**Advantages:**
- No app store submission
- Instant updates
- Try before installing
- Works on any device

### Total Annual Costs

| Item | Cost |
|------|------|
| Desktop hosting | $0/month |
| Web hosting (Vercel) | $0/month |
| Domain name | $12/year |
| Apple Developer | $99/year |
| Google Play | $25 one-time |
| **Total** | **~$136/year** |

**Compare to traditional SaaS:** $240-540/year in server costs

## Technology Decisions

### Why Electron for Desktop?
- Cross-platform with single codebase
- Can bundle Python backend locally
- Full native OS integration
- Auto-update capabilities

### Why Capacitor for Mobile?
- Reuse web technologies (HTML/CSS/JavaScript)
- Single codebase for iOS and Android
- Native plugin access
- Can be adapted to PWA (Phase 3)

### Why PWA for Web?
- Zero hosting costs
- Installable like native app
- Offline capable
- No app store gatekeeping

## Code Sharing Strategy

### Desktop (Python)
```python
# Premium repo: desktop/python_backend/core/randomizer.py
def randomize_playlist(tracks, options):
    # Python implementation
    # Best performance, full library access
    return randomized_tracks
```

### Mobile + Web (JavaScript)
```javascript
// Premium repo: mobile/src/core/randomizer.js
// Also used by: web/src/core/randomizer.js
export function randomizePlaylist(tracks, options) {
  // JavaScript port of Python version
  // Shared between mobile and web
  return randomizedTracks;
}
```

**Result:** Two implementations of the same algorithm, optimized for their platforms.

## Neutral Formats (This Public Repo)

All platforms use the neutral playlist formats defined in this repository:

### JSON Format
```json
{
  "name": "My Playlist",
  "tracks": [
    {
      "id": "spotify:track:xyz",
      "title": "Song Title",
      "artist": "Artist Name",
      "album": "Album Name",
      "position": 1
    }
  ]
}
```

### CSV Format
```csv
position,id,title,artist,album
1,spotify:track:xyz,Song Title,Artist Name,Album Name
```

### TXT Format
```
My Playlist
1. Song Title - Artist Name (Album Name)
```

**See [playlist_format.md](playlist_format.md) for complete specifications.**

## Platform Bridges (This Public Repo)

Bridges allow importing/exporting playlists from streaming services:

### TIDAL Bridge
- Read user playlists
- Export to neutral JSON/CSV/TXT
- Import from neutral formats
- **No streaming or playback control**

### Spotify Bridge
- Read user playlists
- Create and modify playlists (metadata only)
- Export/import neutral formats
- **No audio playback via API**

### Apple Music Bridge
- Read user library via MusicKit
- Export to neutral formats
- Import playlists
- **No streaming control**

**See [docs/platforms.md](platforms.md) for bridge specifications.**

## Compliance with Platform Policies

### What We Do ✅
- Read playlist metadata
- Create and organize playlists
- Export/import playlist data
- Manipulate track ordering

### What We Don't Do ❌
- Stream audio via APIs
- Control playback
- Download or cache audio files
- Resell or redistribute user data
- Bypass platform features

**This keeps us compliant with:**
- [TIDAL Developer Guidelines](https://developer.tidal.com/documentation/guidelines)
- [Spotify API Terms](https://developer.spotify.com/terms)
- [Apple MusicKit Guidelines](https://developer.apple.com/musickit/)

## For Developers

Want to build on AudioArchitect?

### Using This Public Repo
1. Use neutral playlist formats in your own tools
2. Build integrations with the platform bridges
3. Contribute improvements via pull requests
4. Create community tools and plugins

### Premium Features (Private Repo)
The commercial Premium app includes:
- Smart randomization algorithms
- Cross-platform desktop/mobile/web apps
- Analytics and insights
- Premium integrations

**Premium is closed-source but uses formats and bridges from this public repo.**

## Questions?

For questions about:
- **Neutral formats and bridges:** Open an issue in this repo
- **Premium app features:** Contact via website (when launched)
- **Contributing:** See CONTRIBUTING.md in this repo

---

**Summary:** AudioArchitect is a two-part ecosystem. This public repo provides open formats and bridges. The Premium repo builds commercial apps using those foundations, all running client-side with zero hosting costs.
