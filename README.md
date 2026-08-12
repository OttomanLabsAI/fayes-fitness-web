# fayes-fitness-web

The Faye Edwards / **F.I.T — Faye's Intentional Training** website. A single self-contained
HTML page (no build step, no framework), deployed to Cloudflare Workers as static assets.

## Layout

```
public/
  index.html          the home page
  links.html          /links — every destination in one place
  fit-camp.html       /fit-camp
  academy.html        /academy
  community.html      /community
  app.html            /app
  webinar.html        /webinar
  the-book.html       /the-book
  watch.html          /watch
  retreats/
    zanzibar.html     /retreats/zanzibar
    bulgaria.html     /retreats/bulgaria
  assets/fit.css      the whole design system, shared by every page
  404.html            not-found page
  _headers            cache + security headers
wrangler.jsonc        Cloudflare Workers config (static assets only)
```

There is no build step and no templating — each page is plain HTML sharing one
stylesheet. Fonts come from Google Fonts, and the hero portrait and video thumbnail
are remote URLs.

The home page's calls to action route to the inner pages; each inner page carries
the real details and then hands off to where the action happens — booking on
Bookwhen (`bookwhen.com/fayesintentionaltraining`), brochures and signups on
Flodesk, the app on `gcph.tv` plus the App Store / Google Play, the book on
Amazon. `/links` is the link-in-bio page: it replaces the Linktree.

Inner-page copy was rebuilt from Faye's public pages (fayeedwards.co.uk, the
Bookwhen listings, the Zen Zanzibar retreat page, the app-store listings and the
book's publisher description). Prices and itineraries for the trips are only in
the Flodesk brochures, so those pages still hand off for the full picture.

Adding a page: copy the closest existing one, change the copy, and add it to the
`.foot-nav` list in every page's footer and to the `.hub` list in `links.html`.

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

Note that most content now lives in two places — the home page section and the
inner page — so a date change means editing both.

| What | Where in `public/index.html` |
| --- | --- |
| F.I.T Camp date + countdown | `Thu 6 August` in the camp ticket, and `new Date(2026,7,6,...)` in the countdown script (month is 0-indexed) |
| Retreat dates / destinations | the `.set-*` blocks in the "Train somewhere beautiful" section |
| Booking link | `bookwhen.com/fayesintentionaltraining` — top bar here, and the CTAs on `fit-camp.html` / `webinar.html` |
| App price | `.price-chip` in the F.I.T App section |
| Video | YouTube ID `C7QkwNTu8wk` (thumbnail `src` and the embed URL in the script) |
| Contact / socials | the `footer` block |

## Style switcher

The strip under the top bar (`.versions`) flips the whole page between five design
themes — `fit`, `heat`, `edit`, `neon`, `soft` — via `data-theme` on `<body>`.
It ships with **F.I.T** selected. To lock a single style and hide the switcher,
delete the `<div class="versions">…</div>` block and set the theme on `<body data-theme="…">`.
