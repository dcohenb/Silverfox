# Silver Fox Barber Co. — Website

Single-page marketing website for Silver Fox Barber Co., a premium barbershop in Orinda, CA (Theatre Square). Deployed to Cloudflare Workers at `silver.atelerix.net`.

## Project Structure

```
├── public/              # Deploy directory — Wrangler serves from here
│   ├── index.html       # Main single-page site (all HTML/CSS/JS in one file)
│   ├── privacy-policy.html
│   ├── privacy.html
│   └── Photos/          # All images (haircuts, storefront, team headshots)
├── wrangler.toml        # Cloudflare Workers config
├── package.json         # npm scripts for dev/deploy
└── CLAUDE.md
```

## Tech Stack

- **Hosting**: Cloudflare Workers (static assets mode)
- **Build tool**: Wrangler v4 (`npm run deploy`)
- **Framework**: None — pure HTML/CSS/JS, single file
- **Fonts**: Google Fonts — Playfair Display (headings), Inter (body), Space Grotesk (labels/UI)
- **Booking**: Zenoti (external link, no embedded booking)

## Key Commands

- `npm run dev` — local dev server via Wrangler
- `npm run deploy` — deploy to Cloudflare Workers
- `npm run preview` — local preview (offline)

## Domain

- **Production**: `silver.atelerix.net`
- **Zone**: `atelerix.net` (Cloudflare DNS)
- Route configured in Cloudflare dashboard (not in wrangler.toml currently)

## Design System

- **Theme**: Dark background (#0A0A0A) with silver accents (#C0C0C0)
- **CSS custom properties**: `--silver`, `--silver-bright`, `--silver-dark`, `--bg`, `--bg-alt`, `--bg-card`, `--text`, `--text-dim`
- **Metallic text effect**: `background-clip: text` with silver gradient + `shimmer` animation. Used on section titles, CTA heading, and barber names. Keywords in headings are solid white (`-webkit-text-fill-color: #fff`) for contrast.
- **Scroll snap**: `scroll-snap-type: y proximity` on html, `scroll-snap-align: start` on sections
- **Mobile**: 900px breakpoint for responsive layout, `100svh` hero height for mobile browser chrome

## Sections (in order)

1. **Loader** — Staggered text reveal animation
2. **Hero** — Image carousel (5 slides, crossfade + Ken Burns), parallax scrolling
3. **Marquee** — Scrolling service ticker
4. **About** — Two-column grid (image + text)
5. **Services** — Expandable row list with hover animations
6. **Team** — Three barbers: Dave Clark (owner), James Lizotte, Raymond Knapp. Headshots use sketch-to-color filter on hover. Cards have border shimmer on hover.
7. **Gallery** — Horizontal scroll with drag-to-scroll, 3D card tilt, auto-scroll drift
8. **Testimonials** — Rotating cards with dot navigation
9. **Hours & Location** — Split grid with hours table and Google Maps embed
10. **CTA** — Final booking call-to-action
11. **Footer**

## Team / Barbers

- **Dave Clark** — Owner / Barber. Mon–Fri (all Saturdays). IG: @daveismybarber
- **James Lizotte** — Barber. Thu–Mon. IG: @barberjames415
- **Raymond Knapp** — Barber. Tuesdays. IG: @ray_thebarber

Headshot files: `Photos/dave-headshot.jpg`, `Photos/james-headshot.jpg`, `Photos/raymond-headshot.jpg`

## Photo Naming Convention

Photos use descriptive kebab-case names organized by category:
- `barber-action-*.jpeg` — Action shots of barbers working
- `cut-*.jpeg` — Portfolio haircut/style photos
- `storefront-*.jpeg` — Shop exterior and signage
- `*-headshot.jpg` — Team headshots
- `logo.jpeg`, `anniversary-illustration.png` — Branding assets

## Important Notes

- **No prices on website** — prices live in Zenoti only
- **Booking URL**: Currently `https://silverfoxbarber.zenoti.com/webstoreNew/services` as placeholder until real Zenoti booking URL is provided
- **`public/` is the deploy directory** — Wrangler serves from `./public`. All site files live here. Don't put HTML/assets in the project root.
- **All assets must stay under 25MB** — Cloudflare Workers asset size limit. Don't add large video files or uncompressed images.
