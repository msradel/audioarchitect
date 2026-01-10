# AudioArchitect

AudioArchitect is a cross‑platform playlist management tool that helps you randomize, clean up, and move playlists between streaming services without touching the underlying audio streams.

## Project structure

AudioArchitect is split into two parts:

- **AudioArchitect (this repo)** – Open-source Bridges, neutral playlist formats, and platform documentation. Focused on non-commercial tools that help you export/import and clean up playlists between services without touching audio streams.
- **AudioArchitect Premium (private)** – Commercial app with proprietary smart randomization, analytics, and deeper integrations. The code and detailed implementation live in a separate private repository.

The Bridges and Premium app both use the same neutral playlist formats defined in `docs/playlist_format.md`.

## Features

- Smart playlist randomization that preserves variety even in very large playlists  
- Import and export playlists between supported platforms  
- Duplicate detection and basic cleanup tools  
- Backend API built with FastAPI and a desktop UI client (planned)

## Project Status

AudioArchitect is under active development. The original `tidal_tool.py` CLI and related scripts have been moved into the `legacy/` folder and are no longer the primary interface.

## Tech Stack

- Python 3.12 backend with FastAPI  
- Planned desktop app (JavaScript/Node-based)  
- Git for version control, GitHub for hosting

## Getting Started (Development)

```bash
git clone https://github.com/msradel/audioarchitect.git
cd audioarchitect
# backend setup steps will go here once finalized
