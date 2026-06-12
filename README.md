# Simkl Watch Matrix

A personal streaming hub for SIMKL's "Watch Now On" feature.  
Opens with media data pre-loaded from SIMKL. Shows specialist sites first, generalists second.

---

## Setup (5 minutes)

### 1. Create the GitHub repository

1. Go to [github.com/new](https://github.com/new)
2. Repository name: pick anything non-obvious, e.g. `wm-hub` or `xstream` or a random string
3. Visibility: **Public** ← required for free GitHub Pages
   > The page contains only streaming site links — no personal data. An obscure repo name is enough.
4. Click **Create repository**

### 2. Upload the file

1. Click **Add file → Upload files**
2. Upload `index.html`
3. Commit directly to `main`

### 3. Enable GitHub Pages

1. Go to **Settings → Pages**
2. Source: **Deploy from a branch**
3. Branch: `main` / `(root)`
4. Click **Save**

Your site will be live at:
```
https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/
```

---

## Add it to SIMKL

In SIMKL → Settings → Apps → **Watch Now On** → Add Custom Site, paste this entire URL as the **Link URL**:

```
https://YOUR-USERNAME.github.io/YOUR-REPO-NAME/?t=%TITLE%&r=%TITLE_ROMANJI%&y=%YEAR%&s=%S%&e=%E%&ns=%NEXT_S%&ne=%NEXT_E%&type=%TYPE%&at=%ANIME_TYPE%&sid=%SIMKL_ID%&im=%IMDB%&tm=%TMDB%&ki=%KITSU%&al=%ANILIST%&tv=%TVDB%&tvs=%TVDB_SLUG%&tve=%TVDB_EP_ID%&mal=%IMDB_MAL%
```

Replace `YOUR-USERNAME` and `YOUR-REPO-NAME` before saving.

Name it whatever you want (e.g. "Watch Matrix").

---

## Adding your streaming sites

Open `index.html` and find the `const SITES = [` section near the top of the `<script>`.

Each entry looks like this:

```js
{
  name: "SiteName",
  tags: ["anime"],                          // ← one or more: "anime", "movies", "series"
  url:  "https://site.com/{TITLE_SLUG}/{ANILIST}?ep={NEXT_E}"
},
```

### Tag rules

| Tags | Classified as |
|------|---------------|
| `["anime"]` | Anime specialist |
| `["movies"]` | Movie specialist |
| `["series"]` | Series specialist |
| `["movies","series"]` | Dual specialist (shown for movies AND TV, not anime) |
| `["anime","movies"]` | Dual specialist (shown for anime AND movies, not TV) |
| `["anime","movies","series"]` | **Generalist** — always shown at the bottom |

### What shows when

| You open | Shows first | Then at bottom |
|----------|-------------|----------------|
| Anime page | Anime specialists | Generalists |
| Movie page | Movie specialists | Generalists |
| TV/Series page | Series specialists | Generalists |

Sites appear in the order they are listed in the file, within each group.

### Available `{PARAM}` tokens for URLs

```
Titles:
  {TITLE}                 "Attack on Titan"
  {TITLE_PLUS}            "Attack+on+Titan"
  {TITLE_SLUG}            "attack-on-titan"
  {TITLE_UNDERSCORE}      "attack_on_titan"
  {TITLE_ROMANJI}         "Shingeki no Kyojin"
  {TITLE_ROMANJI_PLUS}    "Shingeki+no+Kyojin"
  {TITLE_ROMANJI_SLUG}    "shingeki-no-kyojin"
  {YEAR}                  "2013"

Season/Episode (TV only):
  {S}     1        {SS}    01       {S01}     s01
  {SEASON1} season 1       {SEASON_DASH} season-1
  {E}     1        {EE}    01       {E01}     e01
  {EPISODE1} episode 1     {EPISODE_DASH} episode-1

  Episode title: {EP_TITLE}  {EP_TITLE_PLUS}  {EP_TITLE_SLUG}  {EP_TITLE_UNDERSCORE}

Next-to-watch (recommended for episode links):
  {NEXT_S}   {NEXT_SS}   {NEXT_S01}
  {NEXT_E}   {NEXT_EE}   {NEXT_E01}

Type strings:
  {TYPE}               "tv" / "anime" / "movie"
  {TYPES}              "shows" / "anime" / "movies"
  {TYPE_SHOW}          "show" / "movie"
  {TYPE_SHOWS}         "shows" / "movies"
  {TYPE_SERIES_MOVIE}  "series" / "movie"
  {TYPE_SERIES_MOVIES} "series" / "movies"
  {ANIME_TYPE}         "tv" / "movie" / "ova" / "special"  ← anime only

IDs:
  {SIMKL_ID}   {IMDB}   {TMDB}   {KITSU}
  {ANILIST}    {TVDB}   {TVDB_SLUG}   {TVDB_EP_ID}   {IMDB_MAL}
```

---

## Updating the site

Edit `index.html` locally and re-upload to GitHub (or edit directly in the GitHub web editor).  
Changes go live within ~30 seconds of committing.
