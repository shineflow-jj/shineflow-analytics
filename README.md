# Shineflow Amazon Seller Analytics

Static marketing landing page for **Shineflow Amazon Seller Analytics**, deployed at
[service.shineflowseattle.com](https://service.shineflowseattle.com).

Pure HTML / CSS / JS — no framework, no build step.

## Structure

```
.
├── index.html           # The entire landing page (inline CSS + JS)
├── privacy.html         # Privacy Policy (SP-API / Brand Analytics data use)
├── logo.png             # Shineflow wordmark (header / footer)
├── favicon.svg          # Site favicon (modern browsers)
├── apple-touch-icon.png # 180×180 home-screen icon (iOS)
├── og-image.png         # 1200×630 Open Graph / Twitter share image
├── og-card.html         # Source template used to regenerate og-image.png
└── README.md
```

Everything the page needs at runtime is `index.html`, `privacy.html`, `logo.png`,
`favicon.svg`, `apple-touch-icon.png`, and `og-image.png`. Fonts (Pretendard, Sora)
load from public CDNs.

## Local preview

Any static file server works — for example:

```bash
python -m http.server 4321
# then open http://localhost:4321
```

## Deploy to Vercel

This is a static site with no build step.

**Option A — Dashboard**
1. Import the repository at <https://vercel.com/new>.
2. Framework Preset: **Other**. Build Command: *(leave empty)*. Output Directory: `.` (root).
3. Deploy. Vercel serves `index.html` at the root automatically.

**Option B — CLI**
```bash
npm i -g vercel
vercel          # preview deploy
vercel --prod   # production deploy
```

### Custom domain
In **Project → Settings → Domains**, add `service.shineflowseattle.com` and point the
DNS `CNAME` to `cname.vercel-dns.com` (per Vercel's instructions). All asset paths are
root-relative or absolute production URLs, so the page works once the domain is attached.

## Regenerating the share image

`og-image.png` is rendered from `og-card.html`. To rebuild it (Chrome/Edge required):

```bash
chrome --headless=new --window-size=1200,630 --virtual-time-budget=3000 \
  --screenshot=og-image.png og-card.html
```
