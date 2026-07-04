# France 2026 — Family Expedition Site

This is your whole website: one HTML file, plus the PDFs/MP3s sitting right alongside it in the same repo. No database, no accounts, no monthly bill, no subfolders to worry about.

**Current status:** Briefing I is live. Briefings II–VIII are on the page as "coming soon" until you activate them. The photo album link and route map are already wired up.

## One-time setup (if you haven't already)

1. Create a GitHub repo (e.g. `France-2026`), Public so GitHub Pages is free.
2. Upload `index.html` and all briefing PDFs/MP3s **directly into the repo root** — not inside any folder.
3. Repo **Settings → Pages** → Source: "Deploy from a branch," branch `main`, folder `/ (root)`. Save.
4. Your live URL: `https://yourusername.github.io/France-2026/`

## Releasing Briefing II, III, IV... (each week)

Every briefing already has a slot on the page, greyed out with "Coming soon" until activated.

**1. Upload the two new files** into the repo root, named to match the existing pattern:
- `briefing-2.pdf`
- `briefing-2.mp3`
(then `briefing-3.pdf` / `.mp3`, and so on through `briefing-8`)

**2. Open `index.html`**, search for `Briefing II` (or III, IV...). You'll find a block like this:
```html
<article class="briefing">
  ...
  <span class="briefing-status">Coming soon</span>
  ...
  <div class="briefing-actions">
    <span class="btn disabled">Read the PDF</span>
    <span class="btn disabled">Listen (MP3)</span>
  </div>
</article>
```
Replace it with this pattern (copy Briefing I's working block as a template):
```html
<article class="briefing is-live">
  <div class="briefing-dot"></div>
  <div class="briefing-top">
    <span class="briefing-num">Briefing II</span>
    <span class="briefing-status">Live now</span>
  </div>
  <h3>A Country of Many Countries: Understanding France Through Its History</h3>
  <p class="desc">...</p>
  <div class="briefing-actions">
    <a class="btn primary" href="briefing-2.pdf" target="_blank" rel="noopener">
      <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"/><path d="M14 2v6h6"/></svg>
      Read the PDF
    </a>
  </div>
  <div class="listen-card">
    <div class="listen-card-inner">
      <div class="listen-label">
        <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="10"/><polygon points="10 8 16 12 10 16 10 8"/></svg>
        Listen: Briefing II
      </div>
      <audio controls preload="none" src="briefing-2.mp3"></audio>
    </div>
  </div>
</article>
```
What changes each time: the class `is-live`, the status text `Live now`, the PDF `href`, the audio `src`, the "Listen: Briefing ..." label, and the title/description text.

The audio player sits on the lavender-field illustration (`lavender-field.svg`) by default for every briefing. Want a different background per briefing (e.g. a Normandy beach for Briefing IV, the Eiffel Tower for Briefing V)? Just ask — it's a one-line CSS change per briefing plus a new image.

**3. Re-upload `index.html`** to GitHub, confirming "replace existing file." Live within a minute or two.

You can also just hand Claude the new PDF/MP3 and briefing text each week and say "activate Briefing II" — no manual editing required.

### Why files live in the repo root, not a `files` folder

GitHub's drag-and-drop upload can silently flatten folders — dragging a `files` folder in sometimes uploads only what's inside it, straight into the root, not inside a subfolder as expected. Keeping everything at the root sidesteps that: what you see in the file list is exactly what the links point to.

## The photo album link

Already set up, pointing at your Apple Shared Album. If you ever need to change it, find this near the bottom of `index.html`:
```html
<a class="btn primary" href="https://www.icloud.com/sharedalbum/#B1u532ODWYaCiq" target="_blank" rel="noopener">View &amp; Add Photos</a>
```
and swap in a new link.

Reminder on how sharing works: anyone with the site link can **view** the album (it's the public web view). To let someone **add** their own photos, they need to be individually invited as a participant inside the Photos app itself — the public link alone doesn't grant upload access.

## The route map

Already embedded, pulling live from a Google My Maps map. To add, move, or relabel a pin, just edit the map at [mymaps.google.com](https://www.google.com/maps/d/) — changes appear on the site automatically, no code edit needed. If you ever need to swap to a different map entirely, find this in `index.html`:
```html
<iframe src="https://www.google.com/maps/d/embed?mid=..." width="640" height="480" loading="lazy" style="border:0;"></iframe>
```
and replace the `src` with a new map's embed URL (My Maps → three-dot menu → "Embed on my site" → copy the `src` value).

## The countdown banner

Counts down to August 8, 2026 automatically based on the visitor's own clock — no maintenance needed. If the departure date ever changes, find this in `index.html`:
```javascript
var departure = new Date(2026, 7, 8, 0, 0, 0);
```
Note the month is zero-indexed (`7` = August), so update the year/month/day accordingly.

## Website analytics (GoatCounter)

The site tracks pageviews via GoatCounter, a free, privacy-friendly analytics service (no cookies, no login required from visitors).

**View your stats:** log in at [https://jdbresler.goatcounter.com](https://jdbresler.goatcounter.com) — shows pageviews over time, referring sites, browsers, and rough visitor locations, with history going back as far as you like (unlike GitHub's native 14-day traffic window).

The tracking script is already in `index.html`, right before the closing `</body>` tag:
```html
<script data-goatcounter="https://jdbresler.goatcounter.com/count" async src="//gc.zgo.at/count.js"></script>
```
No action needed — it'll start logging visits as soon as the updated `index.html` is live. It can take about 10 seconds for a pageview to appear in the dashboard, and ad blockers may prevent some visits from being counted (a normal tradeoff with any lightweight analytics tool).
