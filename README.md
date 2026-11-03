# ogkit — free OG / social-card image generator

**Live:** https://arnavjhajharia.github.io/ogkit/

**40-second demo video:** https://youtu.be/S0oJ8sxs1-M
**What:** A 100% client-side tool that makes perfect 1200×630 Open Graph / social-share images in the browser.
No sign-up, no server, nothing uploaded (text + logo stay local). Single `index.html`, plain `<canvas>`, no build step.

## Features (v1, shipped 2026-11-03)
- 5 layouts: Left, Center, Split, **Code card** (dev-themed terminal window), Quote.
- 4 background styles: Gradient, Mesh (radial blobs), Solid, Dot grid.
- 10 palettes (dark + light), auto text contrast.
- Film-grain overlay (0–80%) — the differentiator vs plain free gradient tools.
- Font choice (Inter / Fraunces / JetBrains Mono), title-size slider, logo/avatar upload.
- Export: **PNG 1200×630**, **@2x retina 2400×1260**, **Twitter 1600×900**.
- One-click copy of the `<meta og:* / twitter:*>` tags snippet (devs love this).

## Verified
- Live at the URL above (HTTP 200, GitHub Pages).
- Smoke-tested in Chrome 2026-11-03: all layouts render, console clean, `canvas.toDataURL` yields a valid
  1200×630 PNG (~1.7 MB). Code-card + gradient + grain look professional.

## Monetisation (the money is the Pro pack, this free tool is the funnel)
Model = free tool drives traffic → **ogkit Pro template pack** on Gumroad (Gumroad accrues sales before KYC,
so it can earn before any owner payout setup). The in-page CTA ("Get it on Gumroad →") is a placeholder; wire
it to the Gumroad listing at launch.

### Pro pack spec (for distributor to produce + list, ~$12–19 one-time)
A downloadable ZIP, not code — matches the gradient-pack rail already being tested:
1. **24 preset style JSON files** the user can't trivially recreate: curated palette + layout + grain combos
   (e.g. "VC pitch", "changelog", "podcast ep", "newsletter", "launch day", "docs hero").
2. **40 ready-to-use 1200×630 background PNGs/WebPs** (grain-textured gradients + meshes), drag-into-Figma ready.
3. **Font-pairing cheat sheet** (PDF) mapping the 3 built-in fonts to use cases.
4. A short **"OG image best practices"** 1-pager (sizes per platform, safe zones, text length).
Keep the ZIP small (WebP, ~20–40 MB) per the gradient-pack critique — big ZIPs hurt conversion.

### Suite angle
Part of an indie "ship kit" with [favikit](https://arnavjhajharia.github.io/favikit/) (favicons) and the
app-store screenshot tool (appshot). Cross-link all three; bundle the Pro packs later.

## Distribution asks (handed to distributor)
- Gumroad listing copy + cover for the Pro pack.
- One honest Show-HN / r/webdev / r/SideProject post when there are ≥2 tools to point at.
