# VFX MUSIC VAULT

Neon music discovery and player by SOURAJIT VFX. The backend is wired to the user's JioSaavn-compatible API.

## Music API configured
Base URL: `https://jiosavanapiryden.vercel.app/api`

The backend uses these provided endpoints:
- Search: `GET /search/songs?query=QUERY&page=0&limit=10`
- Song details / stream metadata: `GET /songs/SONG_ID`

Search results provide title, artist, artwork, and (when supplied by the API) a stream URL. When search results do not include a usable stream URL, the app fetches song details on play and selects the highest-quality available `downloadUrl`. The exact upstream response shape can vary; the backend normalizes common response formats.

## Themes
Use the theme selector in the top header to switch between seven styles: VFX Neon, iOS Light, Music Studio, Cyberpunk X, Glass Luxury, AMOLED Black, and Sunset Glow. Your selected theme is saved in browser localStorage and restored on your next visit.

## Features
- Search JioSaavn tracks by song, artist, or keyword
- Cover artwork and artist/album details
- Stream playback when the API returns a browser-accessible audio URL
- Local playlist: use the ＋ button on search results to save tracks, and the player queue button to view your playlist
- Liked songs and recent history in browser localStorage
- Demo tracks remain available when not searching

## Deploy backend (Render, Railway, or Koyeb)
Deploy this repository as a Node.js service. Build command: `npm install`. Start command: `npm start`. Node.js 18 or newer is required; the server uses the platform-provided `PORT`.

After deployment, test:
- `https://YOUR-BACKEND/api/health`
- `https://YOUR-BACKEND/api/search?q=arijit`
- `https://YOUR-BACKEND/api/song?id=SONG_ID`

## GitHub Pages or InfinityFree
These are static hosts and cannot run `server.js`. Deploy the backend separately on Render/Railway/Koyeb, then edit `config.js` to point the frontend at the deployed backend:

```js
window.VFX_API_BASE = "https://YOUR-BACKEND-DOMAIN";
```

Commit the real backend URL (no trailing slash required). If this remains empty on a static host, live API search and streaming details cannot reach the backend. InfinityFree: upload the static frontend files to `htdocs`; it cannot run the Node.js backend.

## Notes
No API credentials were added or invented. The configured API is an unofficial JioSaavn-compatible service, so availability and response formats can change. Playback depends on the returned stream URL being reachable and allowed by the browser. Follow the API provider's terms and applicable music rights.

## Local run
Install Node.js 18+, run `npm install`, then `npm start` and open `http://localhost:3000`.
