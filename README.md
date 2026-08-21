# Kunthive Work

A standalone one-page index of everything Kunthive has built — client websites,
internal platforms, and Kunthive Labs experiments.

**Live domain:** `work.kuntaio.in`
**Independent** of the kunthive.in marketing site. Nothing here links to it, and
nothing there links here.

Static HTML. No build step, no dependencies, no framework.

---

## Design

The page is laid out as a **build report**, not a portfolio grid. It reads top to
bottom and nothing is hidden behind a click, so there are no filters and no
accordions — the sticky act rail is the navigation.

The five acts are ordered by **distance from a paying client**: Act 01 is work
someone paid for, Act 05 is work nobody has asked for yet. That gradient is the
only reason they are numbered. Reorder them and the numbering should go too.

| | |
|---|---|
| Ground / ink | `#000` / `#fff` |
| Accent | one amber, `#dd8a3a` → `#966230`, spent on act numerals, live markers, the sign-off and focus rings. Nowhere else. |
| Display | Instrument Serif |
| Body | Plus Jakarta Sans |
| Labels, data, stack | JetBrains Mono |
| Sign-off | Dancing Script |

The signature element is the act numeral: set in Instrument Serif at display
scale, aligned to the right edge of the act rule, filled with an amber-to-bronze
gradient that fades out before the baseline. It is the only place colour appears
at size.

Dark only. There is no light theme and no theme toggle.

---

## Files

| File | Purpose |
|---|---|
| `index.html` | The entire site — markup, styles and script in one file. |
| `_headers` | Security headers, applied by Cloudflare Pages. |
| `robots.txt`, `sitemap.xml` | Search indexing. |
| `CNAME` | Only used by GitHub Pages. Cloudflare Pages ignores it — safe to delete if you never use Pages. |

---

## Deploying on Cloudflare Pages

1. Cloudflare dashboard → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**.
2. Pick the `8harath/Work` repository.
3. Build settings — leave these empty, this is a static site:

   | Setting | Value |
   |---|---|
   | Framework preset | **None** |
   | Build command | *(leave blank)* |
   | Build output directory | `/` |
   | Root directory | `/` |

4. **Save and Deploy.**
5. Once deployed → **Custom domains** → **Set up a domain** → enter `work.kuntaio.in`.
   Cloudflare adds the DNS record automatically if the zone is on your account.

Every push to `main` redeploys automatically.

> **Note:** `work.kuntaio.in` does not currently resolve. Confirm the `kuntaio.in`
> zone is registered and added to Cloudflare before step 5, or the custom domain
> will fail to validate. If the intended domain is `kunthive.in`, update the
> canonical URL and Open Graph tags in `index.html`, plus `sitemap.xml` and `CNAME`.

---

## Editing the work list

Everything on the page renders from two arrays near the top of the `<script>`
block in `index.html`. The cover figures, the acts and the appendix all derive
from them, so adding a project means copying one block.

A featured project (`PROJECTS`):

```js
{
  name: "Project name",
  cat: "Websites",        // Websites | Platforms | Products | Labs | Research
  status: "Live",         // Live | Delivered | Released | Beta | In build | Prototype
  tagline: "One plain sentence on what it is.",
  stack: ["Next.js", "Supabase"],
  link: "https://example.com",              // live URL, or null
  repo: "https://github.com/org/repo",      // source, or null
  problem: "What was actually wrong before this existed.",
  did: ["What we built.", "Another point."],
  shot: "img/name.webp"  // optional screenshot, shown under the entry tagline
}
```

A smaller client site (`CLIENT_SITES`), grouped by sector:

```js
{ name: "Client name", note: "One line.", stack: "Next.js · Tailwind", url: null }
```

Only set `link` / `url` when the site is confirmed reachable. Verification is
the one thing the accent colour is allowed to mark: an amber dot means we
checked the site is live today, a grey dot means delivered but unverified.

A project's `cat` decides which act it lands in, so the acts need no separate
list. `status` is free text and renders as-is in the pill.

`shot` is optional and absent everywhere today — the report currently runs on
type alone. Add the key to a project and a real screenshot renders under that
entry's tagline; leave it out and nothing is drawn.

---

## Local preview

```bash
python3 -m http.server 8000
# open http://localhost:8000
```
