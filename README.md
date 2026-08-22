# pocketlab.build

The Pocket Lab umbrella site: one static landing page that indexes the runtime
(PocketJS), the research engines grown from it, and the Pocket Museum.

- `public/index.html` is the whole site. Styles are inline; the only external
  requests are Google Fonts.
- `public/assets/` holds the images the page references. `openworld-orchard.jpg`
  is a headless render from the private `pocket-stack/pocket-openworld` repo
  (`--scenario orchard-fire --ticks 420 --seed 7`, bottom toast cropped). The
  rest are copied from `pocket-stack/pocketjs` `site/assets/`.
- Project cards link to stories on [pocketjs.dev](https://pocketjs.dev). The
  navigation links to the live [Pocket Museum](https://museum.pocketlab.build);
  the remaining `*.pocketlab.build` subdomains listed in the index are reserved.
- `public/favicon.svg` is the only icon drawing. `bun tools/icons.ts` rasterizes
  it with headless Chrome into the rest of the family (`favicon.ico`,
  `favicon-96.png`, `apple-touch-icon.png`, `icon-192/512.png`, and a maskable
  512 for Android). `public/safari-pinned-tab.svg` is the hand-flattened
  monochrome version Safari masks for pinned tabs, and `public/site.webmanifest`
  ties the raster set together. Re-run the script after editing the drawing.

## Deploy

An assets-only Cloudflare Worker (no server script), same shape as the
pocketjs.dev site:

```sh
bun install
bun run deploy   # wrangler deploy; provisions pocketlab.build + www on deploy
```

The custom domains require the `pocketlab.build` zone to be active in the
Cloudflare account. `workers_dev` stays on as a fallback preview URL.
