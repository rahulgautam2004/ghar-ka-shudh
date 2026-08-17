# Ghar Ka Shudh — 3D Cart (Improved)

## Bugs fixed
- **Broken HTML structure**: a stray `</main>` closing tag existed with no
  matching opening `<main>` tag anywhere in the file (invalid HTML). Added
  the missing `<main>` tag.
- **Fragile WhatsApp order message**: the checkout message mixed manual
  `%0A` newline codes with only some parts URL-encoded, which can break on
  certain browsers/devices. Rebuilt as one plain-text message, encoded once
  with `encodeURIComponent` — reliable on every device.
- **Cart thumbnails had no broken-image fallback**: the original fallback
  script only ran once at page load, before any cart rows existed, so it
  never covered images added later inside the cart. Switched to a
  capture-phase listener on `document` so it also covers cart thumbnails
  added dynamically.
- **Phone number had no validation**: the checkout form accepted any text
  in the phone field. Added a basic format check before sending the order.
- Removed a duplicate/leftover fallback script block and a stray
  `render();` sitting outside the `<script>` tag at the end of the file.
- Cleaned up duplicated CSS rules (`.checkout`, `.checkoutGrid`, `.cartFab`
  were declared twice, once with a pile of `!important` overrides) into a
  single clean rule set.

## Improvements
- **Product images compressed ~94%** (6.1MB → ~370KB) — converted PNG to
  optimized JPEG at the size they're actually displayed.
- **Quantity +/- controls in the cart** — previously you could only remove
  a whole line; now you can adjust quantity up or down per item.
- **Favicon + Open Graph/Twitter meta tags added** — proper browser tab
  icon and link-preview cards when shared on WhatsApp/social.
- **Accessibility**: added `aria-label` to the icon-only WhatsApp button,
  `width`/`height` on all images (prevents layout shift while loading).
- **Performance**: hero/first product images load eagerly, everything else
  lazy-loads.
- All WhatsApp buttons across the site (hero, footer, floating button) now
  open with a friendly pre-filled greeting message instead of a blank chat.
- Same prices, same phone number, same cart/checkout logic and flow —
  nothing about how the business works was changed.

## Deploying
Open `index.html` locally, or deploy the whole folder to Vercel/Netlify/
GitHub Pages (drag-and-drop the folder, or `vercel --prod` from inside it).
