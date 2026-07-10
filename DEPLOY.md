# How to Live in 13 Days — Poetry Flipbook

A minimal, fluid virtual flipbook for your chapbook with realistic page-turn animation and per-poem SVG doodles.

---

## Files

- **index.html** – The flipbook interface (page-turn, navigation, styling)
- **data.json** – Your poems + doodle definitions (auto-generated)

Both files must be in the same directory.

---

## Deploy to GitHub Pages

### Option 1: Using an Existing Repo

If you already have `anuragsharmaas999-commits.github.io`:

1. Clone it locally
2. Create a new folder (e.g., `poetry-book/`)
3. Drop `index.html` and `data.json` into that folder
4. Push to GitHub
5. Visit: `https://anuragsharmaas999-commits.github.io/poetry-book/`

### Option 2: Create a New Repo for the Book

1. Create a new GitHub repo named `poetry-book` (or anything you want)
2. Clone it locally
3. Add `index.html` and `data.json` to the root
4. In Settings → Pages, set "Source" to main branch, root folder
5. Push and wait ~1 minute for deployment
6. Your site goes live at: `https://anuragsharmaas999-commits.github.io/poetry-book/`

---

## Features

**Page-Flip Animation**  
Swipe between spreads with a realistic 3D page-turn (desktop) or slide (mobile).

**Navigation**  
- Buttons: Prev / Next
- Keyboard: Arrow keys (← → ↑ ↓)
- Mobile: Buttons only (swipe not yet implemented, but buttons work)

**Minimal Design**  
- Cream background, forest-green accents
- Georgia serif for poem titles and body
- Hairline dividers, small-caps eyebrows
- Responsive: works on desktop, tablet, mobile

**Per-Poem Doodles**  
Monoline SVG silhouettes (flower, rain, candle, etc.) drawn in your accent color. Add more by editing `data.json` and the `doodleData` object in `build.py`.

**Responsive**  
- Desktop: two-page spread with 3D flip
- Tablet: two-page spread with 3D flip
- Mobile: single page with slide animation

---

## Customization

### Change Colors

Edit the `:root` variables in `index.html`:

```css
:root {
    --cream: #faf8f5;      /* background */
    --text: #2c2c2c;       /* text color */
    --accent: #3c5a4e;     /* doodles, buttons, accents */
    --light: #e8e6e3;      /* dividers */
}
```

### Change Fonts

Look for `font-family` in the CSS. Currently:
- Poetry titles: Georgia (serif)
- Body: Georgia (serif)
- Buttons/UI: System font

To use Google Fonts, add to the `<head>`:

```html
<link href="https://fonts.googleapis.com/css2?family=Newsreader&display=swap" rel="stylesheet">
```

Then update the CSS:

```css
.poem-title {
    font-family: 'Newsreader', serif;
}
```

### Add or Edit Doodles

Doodles are SVG paths in `data.json`. To add a new one:

1. Edit `build.py` and add to the `DOODLES` dictionary:

```python
"newname": '<circle cx="50" cy="50" r="30" />',
```

2. In the poems list, set `"doodle": "newname"` on any page
3. Re-run: `python3 build.py > data.json`
4. Upload new `data.json`

SVG uses a 0-0 to 100-100 viewBox, so coordinates scale nicely. Monoline style works best (no fills, just strokes).

---

## Testing Locally

If you have Python:

```bash
cd poetry-book/
python3 -m http.server 8000
```

Then open: `http://localhost:8000/`

(You need a local server because `fetch()` doesn't work with `file://` URLs.)

---

## Mobile Tips

- Buttons work on all devices
- Mobile shows one page at a time (easier to read)
- Font sizes scale with viewport width (`clamp()`)
- Touch-friendly button sizing

---

## What's Inside

**index.html**
- HTML5 structure
- CSS with CSS Grid (two-page layout) and CSS 3D transforms (page-flip)
- Vanilla JavaScript (no dependencies)
- Loads `data.json` dynamically

**data.json**
- Array of 25 pages (cover, epigraph, 3 prologue poems, 17 main poems, essay, colophon)
- Each page has type, title, doodle reference, and body text
- `doodles` object contains SVG path definitions

---

## Known Limitations

- Swipe gestures not implemented (buttons work fine)
- No printing stylesheet yet (could add if needed)
- Doodles are monoline only (no complex fills/shadows)

---

## Next Steps

1. Download both files
2. Push to GitHub Pages (Option 1 or 2 above)
3. Share the link: `https://your-github-username.github.io/poetry-book/`

Done. Your poems are live.
