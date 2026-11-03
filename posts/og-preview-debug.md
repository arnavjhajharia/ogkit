---
title: "Link preview shows no image? 7 og:image checks for Slack, X, Discord and LinkedIn"
tags: webdev, seo, html, beginners
published: false
---
<!-- growth s5 fact-check (2026-11-03): removed the "X uses 1600x900" claim (X docs specify a 2:1 summary_large_image, min 300x157, max 4096x4096, <5 MB); removed relative-URL "works if og:url is set" hedge (spec wants absolute URLs); added server-rendering and bot-blocking checks, which are the most common real causes. No canonical_url: dev.to canonical would hand the ranking to the guide; we want both URLs to rank. Publish with AI Disclosure set. Max 1 dev.to post/day. -->

Your page looks fine in the browser, but when you paste the URL into Slack, X, Discord or LinkedIn you get a title and maybe a description, with **no image**. The crawler usually isn't broken. It's almost always one of these.

## 1. The tags only exist after JavaScript runs

Link-preview crawlers read the **raw HTML** the server returns. Most don't execute JavaScript. If your `og:` tags are injected by React/Vue on the client (a plain SPA, or `react-helmet` without SSR), the crawler never sees them.

Check what the crawler sees:

```bash
curl -s https://yoursite.com/page | grep -i 'og:image'
```

If that prints nothing, render the tags on the server (SSR/SSG, or your framework's metadata API).

## 2. `og:image` is a relative URL

Use an absolute URL with the scheme:

```html
<meta property="og:image" content="https://yoursite.com/og/page.png">
```

`/og/page.png` or `//cdn...` is a common reason for "title but no image".

## 3. The image URL doesn't return an image

Open the image URL in a private window, and also run:

```bash
curl -sI https://yoursite.com/og/page.png
```

You want `200` and `content-type: image/png` (or jpeg/webp). Common failures: a redirect to a login page, a 404 from a dynamic OG route, hotlink protection, or an HTML error page served with a 200.

## 4. A firewall is blocking the crawler

Bot-protection settings (a CDN's "bot fight" mode, WAF rules, rate limits, `robots.txt` disallowing everything) can block `facebookexternalhit`, `Twitterbot`, `Slackbot`, `Discordbot` or `LinkedInBot`. Test with the crawler's user agent:

```bash
curl -sI -A "Twitterbot/1.0" https://yoursite.com/page
```

A `403` or a challenge page here explains a missing preview even when everything else is correct.

## 5. Wrong size or too heavy

**1200 × 630** (about 1.91:1) is the safe default that every major platform crops well. For X, set `twitter:card` to `summary_large_image`, or you get the small square card. Keep the file small: X rejects images over 5 MB, and smaller files simply load more reliably for every crawler. A tall phone screenshot will be cropped to a strip.

Size and per-platform notes: [OG image size guide](https://arnavjhajharia.github.io/ogkit/og-image-size/) (includes a **test your link preview** checklist).

## 6. The platform cached the old (broken) preview

Platforms cache what they scraped the first time. After you fix the tags:

- **Facebook**: Sharing Debugger → "Scrape Again".
- **LinkedIn**: Post Inspector re-fetches the URL.
- **X, Slack, Discord, WhatsApp**: no public refresh button. Change the image filename or add a query string (`og.png?v=2`) so it counts as a new URL.

## 7. Missing the basic tag set

A minimal block that works everywhere:

```html
<meta property="og:title" content="Page title">
<meta property="og:description" content="One sentence.">
<meta property="og:url" content="https://yoursite.com/page">
<meta property="og:image" content="https://yoursite.com/og/page.png">
<meta property="og:image:width" content="1200">
<meta property="og:image:height" content="630">
<meta name="twitter:card" content="summary_large_image">
```

`og:image:width`/`height` let some crawlers render the card on the first share without downloading the image first.

---

## Making the 1200 × 630 image

If you don't have a designer, [ogkit](https://arnavjhajharia.github.io/ogkit/) is a free in-browser card maker I built. It exports a 1200 × 630 PNG and copies the tag block above. Nothing is uploaded and no account is needed. There's an optional [paid preset pack ($12)](https://bharatankh.gumroad.com/l/ogkit-pro) if you want more layouts.

**Related (same Ship Kit):** [App Store screenshot sizes in 2026](https://dev.to/bharat_ankh_920bf0864220a/app-store-screenshot-sizes-in-2026-which-ones-are-actually-required-24f5) · [Favicon cache fixes after deploy](https://dev.to/bharat_ankh_920bf0864220a/favicon-not-updating-after-deploy-5-fixes-for-the-browsers-favicon-cache-34ip) · [LinkedIn OG image size](https://arnavjhajharia.github.io/ogkit/og-image-size/#linkedin-og-image) · [WhatsApp link preview](https://arnavjhajharia.github.io/ogkit/og-image-size/#whatsapp-link-preview).

_This post was drafted with AI assistance and checked against the platforms' docs. ogkit is MIT-licensed: [repo](https://github.com/arnavjhajharia/ogkit)._
