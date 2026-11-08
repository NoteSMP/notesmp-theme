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

## Theme frame controls

Themes may define an optional `frames` object. Frame configuration is data validated by the website renderer; it does not accept arbitrary CSS or executable content.

| Property | Allowed values | Purpose |
|---|---|---|
| `enabled` | boolean | Enables the frame renderer |
| `style` | `nine-slice`, `off` | Selects the supplied nine-slice PNG renderer |
| `targets.hero`, `targets.panels`, `targets.cards` | boolean | Chooses which component groups receive frames |
| `width` | 8–32 | Rendered nine-slice border width, pixels (Theme 2 uses exactly 10) |
| `hero`, `panel`, `hover` | `bright`, `muted`, `none` | Legacy-compatible selectors; Theme 2 uses the same single asset for every state |

The renderer uses CSS `border-image` with the exact user-supplied 30×30 PNG at `notesmp-ressources/ui/theme-2/frames/panel-9slice.png`. Each of its nine slices is 10×10 pixels; CSS uses `border-image-slice: 10 fill` and a 10px rendered border width. The same artwork is applied to the homepage hero and main section panels. There are no alternate frame variants, separate corner overlays or extra ornament layers.

## Theme 2 visual direction

Theme 2 uses a forest-biome palette and the exact supplied 10×10-per-slice pixel-art border on the homepage hero and main section panels. Do not reintroduce CSS-drawn corner ornaments, secondary outlines, or alternate border images.

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

The `backgrounds` object controls the page and main homepage hero artwork. Optional `textures` and `decorations` objects expose controlled, validated texture and Minecraft item-art variables to the main website renderer.

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

## Optional texture and decoration variables

Theme JSON may provide:
- `textures.pageBase`, `textures.pageAccent`, `textures.panel`: optional approved HTTPS image URLs. The website renderer maps these to `--theme-texture-page-base`, `--theme-texture-page-accent` and `--theme-texture-panel`.
- `decorations.item`: optional approved Minecraft item image URL.
- `decorations.opacity`: 0–1; `decorations.size`: 12–96 pixels.
- `decorations.animation`: `none`, `glow` or `float`.

These are design inputs only. The website owns their placement, masks, animation behavior and responsive styling; theme JSON cannot inject CSS or markup. When omitted, the renderer uses no extra texture or item decoration.

## Component-specific styling

Themes may optionally define `components.creator` to override the creator cards independently of the global palette. Every value is a six-digit hex color (`#RRGGBB`); omitted values fall back to the theme's semantic colors.

| Property | Controls |
|---|---|
| `background`, `hoverBackground` | Creator card fill and hover fill |
| `border`, `hoverBorder` | Creator card outline and hover outline |
| `avatarBackground` | Avatar placeholder background |
| `streamTitle` | Stream title / supporting text |
| `liveText`, `liveBackground`, `liveBorder` | Live status badge |
| `offlineText`, `offlineBackground`, `offlineBorder` | Offline status badge |

Example:

```json
"components": {
  "creator": {
    "background": "#2A0E0E",
    "hoverBackground": "#421515",
    "border": "#A65A2A",
    "hoverBorder": "#F4C542",
    "avatarBackground": "#351111",
    "streamTitle": "#D9B38C",
    "liveText": "#FFE6A0",
    "liveBackground": "#5A2812",
    "liveBorder": "#E7A92E",
    "offlineText": "#D1A98A",
    "offlineBackground": "#241010",
    "offlineBorder": "#75402A"
  }
}
```

The main website retains control of the creator card structure and status behavior; these values only customize its visual presentation.

### Player profile section selector

Themes may also define `components.profileTabs` to customize the Statistics / Advancements / Posts selector on player UUID pages. Each property is a six-digit hex color (`#RRGGBB`); omitted values fall back to the main theme palette.

| Property | Controls |
|---|---|
| `text`, `background`, `border` | Inactive tab |
| `hoverText`, `hoverBackground`, `hoverBorder` | Hovered tab |
| `activeText`, `activeBackground`, `activeBorder` | Selected tab |
| `divider` | Line beneath the tab group |

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
