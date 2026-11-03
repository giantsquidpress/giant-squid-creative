# Giant Squid Creative — Original Site, Clean HTML

This is the full original thisisgiantsquid.com site (the Webflow-era site, before
the 2026 rebuild), rebuilt as plain self-contained HTML/CSS/JS from the
`giant-squid-mirror-7-26` backup. All 29 pages, as designed and written. Nothing
reworded, nothing redesigned.

## Structure

- 8 root pages: `index.html`, `design.html`, `branding.html`,
  `food-and-drink-consulting.html`, `contact.html`, `fanzine.html`,
  `jp-nihongo-design.html`, `letterpress.html`
- `branding/` — the 6 case studies (Doughnut Time, Dutch Kills, PKNY, Les Bubbles,
  Mister Fitz, Alfred & Constance)
- `blog/` — all 15 'Zine posts
- `assets/css`, `assets/js`, `assets/images`, `assets/fonts` — everything local,
  nothing points at Webflow's CDN or hosting anymore

Open `index.html` directly in a browser — no server needed.

## What got stripped

Google Tag Manager, the Facebook pixel, Google Analytics (gtag/UA-110463858-1),
the Google Search Console verification tag, the TradeDoubler verification comment,
and Webflow's own CMS/publish metadata. All dead weight now that the accounts
behind them are going away with the Webflow/Shopify shutdown. Also dropped the
`integrity=` (SRI) hashes on the CSS/JS tags — they're invalid once the files are
re-hosted locally instead of on Webflow's CDN, and same-origin files don't need them.

## What's still external, on purpose

- Typekit font loading (`use.typekit.net`) — tied to your Adobe Fonts account
- jQuery (Cloudflare CDN) and Masonry.js (cdnjs) — standard libraries, not tracking
- The Instagram feed widget (LightWidget)
- The email signup forms still POST to your existing Mailchimp lists
  (`thisisgiantsquid.us19.list-manage.com`) — confirm that's still live before
  this goes anywhere public

## Two fixes made using the site's own design system, not invented

The two slider-arrow icons on the Branding page (`.svg` files) weren't in any
backup folder under their referenced IDs. Swapped them for the same icon-font
glyph (`w-icon-slider-left` / `w-icon-slider-right`) the homepage hero slider
already uses for the identical arrow — that's the site's own existing fallback,
not a generated substitute.

## One substitution worth a quick look

The PKNY business card photo (`5b3b3c82..._Painkiller-PKNY-businessCard.jpg`)
wasn't in any backup under that upload ID. Found what looks like the same photo
re-uploaded under a different ID in the "GSP website images not used" folder
(`5b435b9f..._Painkiller-PKNY-businessCard-resize.jpg`) and used that instead.
Worth confirming it's the right shot — `branding/pkny-painkiller-tiki-bar.html`.

## Real gaps — flagged, not filled

- **Social-share image** (`og:image`/`twitter:image`, referenced site-wide as
  `GSC-Adwords-template-landscape-1200x628.png`) — not in any backup folder.
  It's still live on Webflow's CDN (confirmed the URL resolves), but neither this
  session's cloud network nor your Mac's network could reach it to pull it down.
  Fastest fix: open
  `https://cdn.prod.website-files.com/5b2487d1a3234fda37a93e93/5cef16465742d72f927bd097_GSC-Adwords-template-landscape-1200x628.png`
  in your own browser and save it into `assets/images/`.
- **Page-load spinner graphic** (`preloader.svg`) — same story, same fix if you
  want it back. Cosmetic only; the loader div is hidden by script almost
  instantly either way.
- **~37 other image/icon references** (team headshots, stock Unsplash photos,
  a few generic UI icons) are leftover Webflow "Business" template placeholders.
  Checked: none of their CSS classes appear anywhere in your actual page
  content, so they never rendered on the live site either. No action needed.
- The `og:image`/`twitter:image` meta tags currently point at a relative path
  (`assets/images/...`). That's fine for opening the file locally, but social
  platforms need an absolute URL — set that once this has a real domain again.
