# fayes-fitness-web

The Faye Edwards / **F.I.T — Faye's Intentional Training** website. A single self-contained
HTML page (no build step, no framework), deployed to Cloudflare Workers as static assets.

## Layout

```
public/
  index.html   the whole site — markup, CSS and JS in one file
  404.html     not-found page
  _headers     cache + security headers
wrangler.jsonc Cloudflare Workers config (static assets only)
```

Everything the page renders lives in `public/index.html`. Fonts come from Google Fonts,
the hero portrait and video thumbnail are remote URLs, and every CTA links out
(Bookwhen, Flodesk, the F.I.T app, YouTube, TikTok, Amazon).

## Local preview

```sh
npx wrangler dev          # serves on http://localhost:8787
```

Or just open `public/index.html` in a browser — there is no build step.

## Deploy

Connected to Cloudflare Workers Builds: pushes to the production branch deploy
automatically. Manual deploy:

```sh
npx wrangler deploy
```

## Editing the content

| What | Where in `public/index.html` |
| --- | --- |
| F.I.T Camp date + countdown | `Thu 6 August` in the camp ticket, and `new Date(2026,7,6,...)` in the countdown script (month is 0-indexed) |
| Retreat dates / destinations | the `.set-*` blocks in the "Train somewhere beautiful" section |
| Booking link | `fayesfitness.bookwhen.com` — appears in the top bar, camp CTA and sticky CTA |
| App price | `.price-chip` in the F.I.T App section |
| Video | YouTube ID `C7QkwNTu8wk` (thumbnail `src` and the embed URL in the script) |
| Contact / socials | the `footer` block |

## Style switcher

The strip under the top bar (`.versions`) flips the whole page between five design
themes — `fit`, `heat`, `edit`, `neon`, `soft` — via `data-theme` on `<body>`.
It ships with **F.I.T** selected. To lock a single style and hide the switcher,
delete the `<div class="versions">…</div>` block and set the theme on `<body data-theme="…">`.
