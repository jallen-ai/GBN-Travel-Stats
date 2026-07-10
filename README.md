# GBN Black — 9U Travel Ball Stats

A single-page dashboard for the GBN Black team. It pulls live from the team Google
Sheet, so it stays current with no re-deploy — update the sheet, refresh the page.

**Three views:**
- **Season Stats** — sortable table of every Black player + team stat tiles
- **Leaderboards** — ranked bars for AVG, OBP, Hits, RBI, and Walk Rate
- **Who's Hot** — last-5-games average vs. season average, with trend arrows

## How it works

One file: `index.html`. No backend, no build step, no dependencies. It reads the
`Player Totals` and `Recent Form` tabs of the public Google Sheet via Google's
visualization endpoint (which allows cross-origin reads for link-shared sheets)
and filters to `GBN Black`.

The sheet must stay set to **"Anyone with the link — Viewer."** If it's ever made
private, the page can't read it.

## Deploy to GitHub Pages

1. Create a new GitHub repo (e.g. `gbn-black-stats`).
2. Upload `index.html` (and this README) to the repo.
3. Repo **Settings → Pages → Build and deployment**: set **Source = Deploy from a
   branch**, branch `main`, folder `/ (root)`. Save.
4. Wait ~1 minute. Your site is live at
   `https://<your-username>.github.io/gbn-black-stats/`.
5. Share that link with coaches and parents.

## Test locally

```bash
cd gbn-black-dashboard
python3 -m http.server 8000
# open http://localhost:8000
```

## Changing the config

All settings are at the top of the `<script>` in `index.html`:

- `SHEET_ID` — the Google Sheet ID (from its URL)
- `TEAM` — currently `GBN Black`. Change to `GBN White` or `GBN Green` to point the
  same app at another team.

The tab-parsing assumes the current column layout of the `Player Totals` and
`Recent Form` tabs. If those tabs are restructured, update the column indexes in
`parseTotals()` / `parseRecent()`.
