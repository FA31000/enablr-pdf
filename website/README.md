# Enablr website

Single self-contained page. The logo is embedded as base64, so `index.html` needs no other file.

## Deploy

Cloudflare Pages project `enablr`, output at `enablr.pages.dev`.
If connected to this repository, set **Build output directory** to `website` and leave the build command empty.

## Before attaching ai-enablr.com

1. Remove `<meta name="robots" content="noindex, nofollow">` in the `<head>`. It is there so the test URL is not indexed.
2. Replace the four `mailto:` links with the real booking link.
3. Add the two founder photos, currently initials in a circle.
4. Build `diagnostic.html`, the five-question simulator. The button in the self-diagnostic band points to it.

## House rules

Brand: navy `#0F1E33`, coral `#E7663F`, cream `#FBF8F2`, hairline `#E4DDD0`. Poppins everywhere, Lora italic for the baseline and the pull quote. Never an em dash, the separator is a spaced period.

Layout: one single column definition, `.wrap`, max-width 1120 px with 24 px of side padding. Every band, the nav and the footer use it, which is what keeps the left and right edges identical down the whole page. Do not add horizontal padding anywhere else.
