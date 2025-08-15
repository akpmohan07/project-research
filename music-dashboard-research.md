# Music Dashboard Research

## Overview
This document summarizes research on building a personal or public music dashboard using Last.fm, ListenBrainz, and related tools. Includes key findings, options, and action items.

---

## Data Sources

### 1. Last.fm
- **Pros:** Largest ecosystem of scrobblers, widely supported by Spotify, YouTube, Apple Music, etc.
- **Cons:** Closed-source, rate-limited API, data lives on Last.fm servers.
- **API:** Free for read-only endpoints (recent tracks, top tracks, top artists, top albums).

### 2. ListenBrainz
- **Pros:** Open-source, open API, privacy-friendly, unlimited API calls.
- **Cons:** Smaller ecosystem than Last.fm; may require import from Last.fm for full scrobbling coverage.
- **API:** Public and free, supports recent listens, top artists, top tracks.

### 3. Stats.fm / Volt.fm
- **Pros:** Pull Spotify statistics without scrobbling.
- **Cons:** Limited to Spotify, no full scrobbling, unofficial APIs.

---

## Existing Open-Source Dashboard Projects

### Last.fm Dashboards
- [dash.fm](https://github.com/peterdconradie/dash.fm) – Live charts, real-time now-playing, serverless-friendly.
- [dash.fm-improved](https://github.com/BoredDevHQ/dash.fm-improved) – Enhanced version of dash.fm.
- [lastfm-dashboard](https://github.com/Prepel/lastfmdashboard) – Simple dashboard for monitoring Last.fm users.
- [lastfm-dashboard-fe](https://github.com/jfvanin/lastfm-dashboard-fe) – Vue.js frontend (needs backend).

### ListenBrainz Dashboards
- [ListenBrainz Dashboard](https://github.com/Aidan-Price/Listenbrainz_Dashboard) – Uses BigQuery datasets, visual analytics.
- [listenbrainz-local](https://github.com/metabrainz/listenbrainz-local) – Web-based interface to explore ListenBrainz data.

---

## Key Takeaways
- If you want **wide scrobble support**, use **Last.fm**.
- If you want **serverless API and open data**, use **ListenBrainz** (optionally import Last.fm).
- Existing projects like **dash.fm** can be forked and customized for `music.mohanverse.dev`.
- If you don’t want to host anything yourself, stick with **Last.fm API** for a GitHub Pages dashboard.

---

## Action Items

1. **Decide Data Source**
   - [ ] Last.fm only
   - [ ] Last.fm + ListenBrainz import
   - [ ] ListenBrainz only

2. **Collect Useful Links**
   - [ ] GitHub repos for dashboard examples
   - [ ] Articles or tutorials

3. **Decide Deployment**
   - [ ] GitHub Pages (static, serverless)
   - [ ] Subdomain: `music.mohanverse.dev`

4. **Dashboard Features**
   - [ ] Recent tracks
   - [ ] Top artists
   - [ ] Top tracks
   - [ ] Charts / graphs
   - [ ] Album art / interactivity (optional)

5. **Build Minimal Prototype**
   - [ ] HTML + JS + Tailwind
   - [ ] Fetch data from API (Last.fm or ListenBrainz)
   - [ ] Render simple cards or tables

6. **Documentation & Knowledge Base**
   - [ ] Maintain a Markdown log of all projects, notes, and links
   - [ ] Optional: move to Obsidian or Notion for structured notes

---

## Notes
- API keys obtained for Last.fm.
- GitHub Pages is preferred for static deployment.
- Maloja (self-hosted) was considered but ruled out due to hosting requirements.

https://www.reddit.com/r/lastfm/comments/ckhkcn/how_do_i_share_my_scrobbles/
https://www.last.fm/api#getting-started
https://www.reddit.com/r/lastfm/comments/10bhyj0/other_than_lastfm_what_other_music_related_apps/
https://alternativeto.net/software/lastfm/
https://stats.fm/31s2wl7qsxgyjigfvhtrbrxffzlm
