# NoteSMP Themes

This repository contains the visual configuration for the NoteSMP website. The website's layout, routes, content, API calls, player data and application behavior remain in [notesmp-website](https://github.com/NoteSMP/notesmp-website).

## Theme slots

| Website option | File |
|---|---|
| Default | Built into the website; preserves its standard appearance |
| Theme 1 | `themes/theme-1.json` |
| Theme 2 | `themes/theme-2.json` — Overworld / Minecraft Dungeons-inspired forest palette, section frames, grass-stone accents and loot-gold trim |
| Theme 3 | `themes/theme-3.json` |
| Theme 4 | `themes/theme-4.json` |

Each slot is independent. The JSON files are the editable design surface; the website validates the values and maps them to a controlled set of CSS properties.

## Safe customization model

Theme files are data, not executable CSS or JavaScript. You can change the visual identity—including the hero artwork, font roles, colors, shapes, backgrounds and interaction effects—but cannot use a theme to inject scripts, arbitrary CSS, hide/reorder website sections, replace application logic, or alter API behavior.

Keep the existing JSON property names and value types. The website uses safe defaults for the optional `backgrounds.heroSettings`, `typography.brand` and `typography.ui` properties when they are omitted.

## Colors

All color values must be six-digit hexadecimal strings (`#RRGGBB`). All ten keys are required.

| JSON key | Purpose |
|---|---|
| `background` | Main page background |
| `surface` | Main cards and panels |
| `surfaceRaised` | Raised panels and secondary surfaces |
| `text` | Primary text |
| `muted` | Secondary text, labels and supporting copy |
| `border` | Borders and separators |
| `accent` | Primary highlight, active states and key actions |
| `accentSecondary` | Secondary accent |
| `warning` | Warnings and attention states |
| `danger` | Errors and destructive states |

The website maps these semantic colors onto its existing design tokens. Keep text/background contrast readable.

## Typography

The `typography` object controls separate font roles and type scale. Font names must be selected from the approved list; theme JSON cannot load arbitrary font files or font URLs.

| JSON key | Allowed values | Used for |
|---|---|---|
| `body` | Approved font name | Main body copy |
| `display` | Approved font name | Headings and display text |
| `mono` | Approved font name | Numeric and technical text |
| `brand` | Approved font name | Website wordmark / brand lettering; defaults to `display` |
| `ui` | Approved font name | Buttons and form controls; defaults to `body` |
| `bodySize` | 12–20 | Base body size, pixels |
| `headingScale` | 0.75–1.5 | Heading scale factor |
| `smallScale` | 0.75–1.5 | Compact label / metadata scale |
| `bodyLineHeight` | 1.2–2 | Body line-height multiplier |
| `headingLineHeight` | 0.85–1.4 | Heading line-height multiplier |
| `letterSpacing` | -0.05–0.1 | Body letter spacing, em |
| `headingLetterSpacing` | -0.1–0.05 | Heading letter spacing, em |
| `bodyWeight`, `displayWeight`, `smallWeight` | 400, 500, 600, 700, 800 | Font weights for each text role |

### Approved fonts

| Font | Style | Loaded weights |
|---|---|---|
| Manrope | Modern geometric sans | 400, 500, 600, 700, 800 |
| DM Sans | Neutral sans | 400, 500, 600, 700, 800 |
| Space Grotesk | Technical display sans | 400, 500, 600, 700 |
| Oxanium | Futuristic / sci-fi display | 400, 500, 600, 700 |
| Rajdhani | Narrow game / UI sans | 400, 500, 600, 700 |
| Cinzel | Fantasy / classical serif | 400, 500, 600, 700 |
| Press Start 2P | Pixel-art display | 400 |
| DM Mono | Monospaced | 400, 500 |
| System UI | Local system sans | Browser / OS default |
| Georgia | Local serif | Browser / OS default |

The website loads the listed web fonts through Google Fonts. System UI and Georgia use local system/browser fonts. A font's selected weight should be one that the font actually provides; the browser may synthesize a nearby weight otherwise.

## Theme 2 visual direction

Theme 2 uses a forest-biome palette with a restrained Minecraft Dungeons-style frame language. Main website sections use a single stone-green outer edge with a small grass-green top accent and occasional loot-gold corner detail. Content cards use one accent rail rather than nested outlines. Keep borders structural and consistent; avoid adding multiple inset rectangles or decorative frames around every element.

## Shapes

All values are pixels.

| JSON key | Range | Controls |
|---|---:|---|
| `cardRadius` | 0–28 | Card and panel corners |
| `controlRadius` | 0–28 | Buttons and form controls |
| `heroRadius` | 0–40 | Hero container corners |
| `borderWidth` | 0–4 | Shared theme border thickness |

## Effects

| JSON key | Allowed values / range | Controls |
|---|---|---|
| `shadow` | `none`, `soft`, `medium`, `strong` | Predefined shadow strength |
| `hoverLift` | 0–4 | Hover lift distance, pixels |
| `motionMs` | 0–600 | Shared transition duration, milliseconds |

## Background images and hero art direction

The `backgrounds` object controls the page and main homepage hero artwork.

| JSON key | Type | Purpose |
|---|---|---|
| `page` | `null` or approved HTTPS image URL | Optional page background image |
| `hero` | `null` or approved HTTPS image URL | Homepage hero image |
| `heroSettings.position` | Approved position string | Image focal point / crop |
| `heroSettings.size` | `cover` or `contain` | How the image fits the hero |
| `heroSettings.minHeight` | 240–720 | Hero minimum height, pixels |
| `heroSettings.overlayColor` | Hex color | Tint used to keep hero text readable |
| `heroSettings.overlayOpacity` | 0–0.95 | Strength of the hero tint |

Supported hero positions: `center`, `center top`, `center center`, `center bottom`, `left center`, `right center`, `58% center`, `center 42%`, `center 53%`, and `center 60%`.

Example:

```json
"backgrounds": {
  "page": null,
  "hero": "https://minecraft.wiki/images/Forest.png?536a7",
  "heroSettings": {
    "position": "center 42%",
    "size": "cover",
    "minHeight": 420,
    "overlayColor": "#10251D",
    "overlayOpacity": 0.62
  }
}
```

Image URLs must use HTTPS and an approved public source:
- `minecraft.wiki/images/...`
- `raw.githubusercontent.com/NoteSMP/notesmp-ressources/...`
- `raw.githubusercontent.com/NoteSMP/notesmp-theme/...`
- The matching `cdn.jsdelivr.net/gh/NoteSMP/...@main/...` paths.

Put reusable artwork in the public resources repository where possible. Do not use data URLs, private assets, arbitrary third-party hosts or tracking URLs. A `null` page image leaves the theme's CSS page background in control; a `null` hero image uses the website's built-in hero artwork.

## Example workflow

1. Choose one slot file, such as `themes/theme-2.json`.
2. Set its colors and shapes.
3. Choose separate `body`, `display`, `mono`, `brand` and `ui` fonts.
4. Set `backgrounds.hero` and tune `heroSettings.position`, `size`, `minHeight` and overlay.
5. Adjust effects and typography scales.
6. Commit the JSON change and preview that slot using the selector at the bottom of the website.

The website falls back to Default if a file cannot be loaded or contains invalid settings. The selector choice is stored in each visitor's browser and does not change the theme for other visitors.

## Contribution boundaries

Do not add HTML, JavaScript, CSS, API configuration, player data, credentials or secrets to this repository. Contributors should make changes only to the theme JSON files and follow the approved schema above. The website repository owns the renderer and the allowed property list.
