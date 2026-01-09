# AudioArchitect

AudioArchitect is a cross‑platform playlist management tool that helps you randomize, clean up, and move playlists between streaming services without touching the underlying audio streams.

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
