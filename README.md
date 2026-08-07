# Enablr one-pager V10 . how to render and edit

Everything needed to regenerate the PDF from the HTML is in this folder.

## Files

| File | Role |
|---|---|
| `Enablr_One-Pager_V10.html` | the source. All the content and all the CSS live here, single file. |
| `pagebg.png` | full-page A4 background, 1240 x 1754 px. Carries the cream page and the navy-to-coral band at the top of every page. |
| `logo-header.png` | running header logo, 150 x 35 px, top-left of every page except page 1. Rendered at native size, so do not resize it. |
| `enablr-logo.png` | the lockup on page 1, 1674 x 400 px, rendered at 11 mm tall. |
| `Enablr_One-Pager_V10.pdf` | the reference output, to compare against. |

The three PNGs must sit **in the same folder** as the HTML, with **these exact filenames**. They are referenced by relative path in the CSS (`url(pagebg.png)`, `content:url(logo-header.png)`, `<img src="enablr-logo.png">`).

## Rendering

The PDF is produced with **WeasyPrint**, not with a browser. A browser print will not reproduce the page background, the running header or the page counter.

```bash
pip install weasyprint
weasyprint Enablr_One-Pager_V10.html Enablr_One-Pager_V10.pdf
```

## Fonts

**Poppins** and **Lora** must be installed on the machine that renders. Without them WeasyPrint falls back to Helvetica and the whole layout shifts.

```bash
# Debian / Ubuntu
sudo apt install fonts-poppins fonts-lora
# macOS, or any OS: download from Google Fonts and install
# https://fonts.google.com/specimen/Poppins
# https://fonts.google.com/specimen/Lora
```

## Things to know before editing

- **WeasyPrint does not support `flex-wrap`, `justify-content: space-between` for vertical distribution, or `margin-top: auto`.** Rows are built as explicit flex rows. Vertical alignment is done with hardcoded values measured on the render, see below.
- **Three hardcoded alignment values** in the method block, page 1. If you change the content of the navy block or of the two Track cards, these must be re-measured:
  - `.mtip svg height="62mm"` : the height of the coral-pointed navy shape. Must equal the navy block height.
  - `.tcard margin-bottom: 21px` : the gap between Track A and Track B. Set so that Track A aligns with the top of the navy block and Track B with its bottom.
  - `.mleft` and `.mtracks` paddings.
  The reliable method is to render, measure the pixel extents of the navy block and of the two cards, then adjust. Do not estimate by eye.
- **The document is designed to fit exactly 3 pages.** Adding content will push it to 4. Recover space by tightening line heights and paddings, never by dropping body text below 7 pt.
- **Placeholders left on purpose**, in coral: `[ X ] hours of training per month` in the Track A pricing row, and `[ photo to add ]` for both founders.
- The final CTA banner is `position: absolute; bottom: 0` so it pins to the bottom of the last page, above the footer.
- Brand: navy `#0F1E33`, coral `#E7663F`, cream `#FBF8F2`, sand `#EFE7D8`, hairline `#E4DDD0`, teal `#1F8A80`. Poppins for everything, Lora italic for the baseline and the quote. Never use an em dash, the house style uses a spaced period as a separator.

## Structure

1. Header, intro, quote
2. `01` What it does for your business, 4 benefit rows
3. `02` The method: navy mapping block, Track A and Track B, ownership line
4. `02` continued, page 2: the 4 technical layers plus 2 hexagon badges
5. `03` How we work with you, the pricing table
6. `04` Who it is for
7. `05` Case studies, page 3
8. `06` Who we are
9. Final CTA banner
