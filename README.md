# Kunthive Work

A standalone one-page index of everything Kunthive has built — client websites,
internal platforms, and Kunthive Labs experiments.

**Live domain:** `work.kuntaio.in`
**Independent** of the kunthive.in marketing site. Nothing here links to it, and
nothing there links here.

Static HTML. No build step, no dependencies, no framework.

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
block in `index.html`. Counters, filters and category groups all derive from
them, so adding a project means copying one block.

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
  did: ["What we built.", "Another point."]
}
```

A smaller client site (`CLIENT_SITES`), grouped by sector:

```js
{ name: "Client name", note: "One line.", stack: "Next.js · Tailwind", url: null }
```

Only set `link` / `url` when the site is confirmed reachable — a green-filled
dot on the page means "we checked this".

---

## Local preview

```bash
python3 -m http.server 8000
# open http://localhost:8000
```
