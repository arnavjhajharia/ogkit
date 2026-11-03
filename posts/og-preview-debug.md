---
title: "Link preview shows no image on Slack/X/Discord — OG debug checklist"
tags: webdev, seo, marketing, beginners
published: false
canonical_url: https://arnavjhajharia.github.io/ogkit/og-image-size/
---

Your page looks fine in the browser. Paste the URL in Slack and you get title + description but **no image**. Usually it is not "the crawler is broken" — it is one of these:

## 1. Missing or wrong `og:image` size

Open Graph expects **1200 × 630** (1.91:1). Tall phone screenshots get cropped oddly or dropped. Twitter/X often uses **`twitter:card` = summary_large_image** with the same asset or **1600 × 900**.

Reference: [OG image size & meta tags](https://arnavjhajharia.github.io/ogkit/og-image-size/#twitter-card) (1200×630 + `summary_large_image`). Facebook-specific: [#facebook-og-image-size](https://arnavjhajharia.github.io/ogkit/og-image-size/#facebook-og-image-size). LinkedIn share card: [#linkedin-og-image](https://arnavjhajharia.github.io/ogkit/og-image-size/#linkedin-og-image). Debugger warnings: [#og-image-warnings](https://arnavjhajharia.github.io/ogkit/og-image-size/#og-image-warnings).

## 2. Relative URL in `og:image`

Crawlers need an **absolute** URL (`https://yoursite.com/og.png`). A path like `/og.png` fails on some parsers unless `og:url` is set correctly.

## 3. Image blocked or too slow

Hotlink protection, auth walls, or 5xx on the image URL → no preview. Test the image URL in a private window.

## 4. Stale cache

Facebook, LinkedIn, and Slack cache previews. After you fix tags, use each platform's debugger / "refresh scrape" tool (where available) or change the image filename. WhatsApp has no public debugger — see [#whatsapp-link-preview](https://arnavjhajharia.github.io/ogkit/og-image-size/#whatsapp-link-preview).

## 5. `og:image` points at HTML

Must be **JPEG/PNG/WebP**, not an HTML page. Common mistake when using dynamic OG routes incorrectly.

---

## Make a correct 1200×630 in the browser

[ogkit](https://arnavjhajharia.github.io/ogkit/) renders social cards on a canvas, exports 1× and 2× PNG, and copies the full `og:` / `twitter:` block. No account, no upload. Preset layouts + grain backgrounds: [ogkit Pro on Gumroad ($12)](https://bharatankh.gumroad.com/l/ogkit-pro).

_Disclosure: AI-assisted; MIT [repo](https://github.com/arnavjhajharia/ogkit). Part of the Ship Kit with [AppShot](https://arnavjhajharia.github.io/appshot/) and [Favikit](https://arnavjhajharia.github.io/favikit/)._
