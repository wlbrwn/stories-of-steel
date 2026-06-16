# Stories of Steel

A cinematic, single-page redesign for [storiesofsteel.com](https://storiesofsteel.com) — a Pittsburgh walking tours business covering three Mon Valley neighborhoods: Braddock, Homestead, and Wilkinsburg.

## File Structure

- `index.html` — the entire site (HTML, CSS, and JS in one file)
- `.claude/launch.json` — dev server config

## Running Locally

```bash
cd "/Users/willbrown/Desktop/Stories of Steel"
python3 -m http.server 3456
```

Open `http://localhost:3456` in Chrome.

## Design Goals

- **Cinematic and immersive** — dark industrial aesthetic, amber/gold accents, serif typography
- **Single-page experience** — no page loads; neighborhoods reveal in-place via animation
- **Color palette:** background `#0f0d08`, amber `#c8963c`, cream text `#ede5d4`, dark card `#1e1a12`
- **Fonts:** Playfair Display (headings) + Inter (body) via Google Fonts

## Homepage Layout

1. **SVG smokestack scene** — perspective illustration of 6 smokestacks per side (12 total), framing a central title block ("Stories of Steel"). Both tops and bases of stacks follow vanishing-point perspective lines converging at the center. Stacks scale linearly in height and maintain consistent height/width proportions (~16:1). Animated amber smoke wisps rise from each stack.

2. **Title block** — peaked roof polygon, "Pittsburgh · Mon Valley" eyebrow text, "Stories / of / Steel" in Playfair Display serif.

3. **Tagline** — "Tour iconic Mon Valley neighborhoods" at 18px with wide letter-spacing, spanning roughly the width of the three arches below.

4. **Three arch portals** — Wilkinsburg, Homestead, Braddock. Postcard images display in black & white; hover turns them color. Clicking an arch triggers a zoom animation that expands it to fill the screen, then reveals a neighborhood detail page.

## Neighborhood Detail Pages

Each neighborhood page includes:
- Established year, name, and description
- Tour stats (duration, stops, distance)
- Stop highlights grid
- CTA buttons (Book Tour, Learn More)
- goBack() returns to homepage cleanly

## Perspective / SVG Notes

- SVG `viewBox="0 -220 900 515"`, `class="scene-svg"` (max-width 920px, overflow visible)
- Vanishing point at approximately `(450, 122)` in SVG coordinates
- Base line (left): `y = 156 + (355 - x) * 139/385`
- Top line passes through VP `(450, 122)` and outer stack cap `(49, -169)`, slope ≈ 0.726
- Stack x-positions (left): L1=330, L2=303, L3=262, L4=206, L5=135, L6=49
- Gaps between stacks taper inward: 15px (L1↔L2) → 35px (L5↔L6), giving more space toward the outer edges

## Zoom Animation

- Full-screen `#zoom-overlay` (z-index 1000) receives the arch's postcard image as background
- `clip-path: inset()` starts at the arch's bounding rect and expands to fullscreen over 1.6s
- `#scene-darken` (z-index 1001) fades in, then `#nbh-page` (z-index 2000) appears
- `goBack()` reverses the sequence

## Deferred / Upcoming

- Booking/reservation system (to discuss with friend)
- Further polish on the zoom animation
- Mobile responsiveness
