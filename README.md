# DevCanopy

The static site for [devcanopy.co](https://devcanopy.co/) — the studio page for
RetroCanvas, ForayLab, DevClimate and Patchrail. Plain HTML and CSS: no packages,
build process, or server required.

## Shared tokens

The point of this site is that clicking through to a product feels like staying put.
That is a copy-and-visual decision first — the public pages talk about the *experience*
("learn one, know them all"), never about the design system that delivers it.

Mechanically, it works because this site reuses the tokens the four product apps
already share:

| | |
|---|---|
| Surfaces | `#f7f8fa` bg, `#ffffff` surface, `#f0f2f5` sunken |
| Ink | `#1a1d26` / `#5a5f72` / `#8b90a0` |
| Type | DM Sans (display), Inter (body) — self-hosted from `/fonts/` |
| Spacing | 4px scale |
| Radius | 6 / 10 / 14 / 20px |
| Shadows | four-step ramp |

Every one of those values is copied from the apps' own token files:

- `retro-canvas/frontend/src/index.css`
- `ForayLab/client/src/index.css`
- `devclimate/src/client/index.css`

**If a value in `styles.css` ever disagrees with those files, those files are right.**

DevCanopy takes no brand hue of its own — the parent is ink (`#1a1d26`), and its
accent is the family: ForayLab teal → RetroCanvas indigo → DevClimate purple, in hue
order (`--canopy-sweep`). Each product card is painted in the real brand colour of
the site it links to, which is the whole cohesion mechanism; see the `.card-*` blocks
in `styles.css`.

Product brand hues, for reference:

| Product | Brand | Chip gradient |
|---|---|---|
| RetroCanvas | `#6366f1` | → `#a78bfa` |
| ForayLab | `#0d9488` | → `#67e8f9` |
| DevClimate | `#7e22ce` | → `#e879f9` |
| Patchrail | unshipped — ink, not a hue | |

## Edit the site

- Product cards: the `#products` section in `index.html`. `portfolio/index.html` is
  generated from that same markup — if you change a card, change it in both, or
  re-run the extraction noted in the git history.
- Tagline: "For engineers, by engineers" appears in the hero pill, the canopy diagram's
  root node, both footers, and the social card. Change it in all five.
- Design tokens: the `:root` block at the top of `styles.css`.
- Page titles and social/SEO metadata: the `<head>` of each page.
- Custom domain: `CNAME`.

Preview locally with `python3 -m http.server 8899` from this directory, then open
<http://localhost:8899/>. Opening the files directly with `file://` will not work —
the pages reference `/fonts/` and `/styles.css` by absolute path.

## Regenerating the image assets

All of them derive from one mark: the rounded chip carrying `--canopy-sweep` with the
white canopy glyph. `favicon.svg` is the source of truth for the shape.

The PNGs and the social card are rendered with headless Chrome. With the local server
running:

```sh
# Social card → assets/devcanopy-og.png (1200×630)
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" \
  --headless --disable-gpu --hide-scrollbars --force-device-scale-factor=1 \
  --window-size=1200,630 --virtual-time-budget=6000 \
  --screenshot=assets/devcanopy-og.png \
  http://localhost:8899/assets/og-card.html
```

`assets/og-card.html` is the editable source for the social image and carries the
same command in a comment at the top.

Icons (`favicon-32.png`, `icon-192.png`, `icon-512.png`, `apple-touch-icon.png`) are
rendered from `favicon.svg` at the matching size with `--default-background-color=00000000`
for transparency. Note that `rx` is expressed in the SVG's 32-unit viewBox, not in
pixels — `6` is the suite's `--radius-sm`; the launcher icons use `7`, and the Apple
touch icon is full-bleed (`0`) because iOS applies its own mask.

## Fonts

`/fonts/` holds the same self-hosted `.woff2` files the product apps serve. They are
copied rather than loaded from Google's CDN, which is what the apps do (it avoids
leaking visitor IPs) and guarantees the same typeface rendering on both sides of a
click.

## Publish with GitHub Pages

1. Push to the `main` branch of a public GitHub repository.
2. **Settings → Pages → Build and deployment**: *Deploy from a branch*, `main`, `/(root)`.
3. Confirm `devcanopy.co` as the custom domain, then enable **Enforce HTTPS**.
4. At the registrar, add the DNS records GitHub Pages supplies for the apex and `www`.

See [GitHub's custom domain instructions](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site/managing-a-custom-domain-for-your-github-pages-site)
for current DNS values.
