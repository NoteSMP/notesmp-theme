# NoteSMP Themes

This repository contains the **visual theme settings** for the NoteSMP website. The website layout, routes, content, API calls, player data and application behavior remain in [notesmp-website](https://github.com/NoteSMP/notesmp-website).

## Theme slots

| Website option | File |
|---|---|
| Default | Built into the website; preserves its current appearance |
| Theme 1 | `themes/theme-1.json` |
| Theme 2 | `themes/theme-2.json` |
| Theme 3 | `themes/theme-3.json` |
| Theme 4 | `themes/theme-4.json` |

The four starter files intentionally match the current design, except for Theme 1's current blackstone / gold / red experiment. Each slot can be designed independently.

## Why themes use JSON tokens

Theme files are **data, not executable CSS or JavaScript**. The website validates each value and applies only approved visual properties. This lets contributors adjust appearance without giving them a way to change page structure, hide sections, replace application logic, or alter API behavior through arbitrary CSS.

## What can be themed

### Colors

Every color is a six-digit hexadecimal value (`#RRGGBB`).

| JSON key | Website token | Purpose |
|---|---|---|
| `background` | `--bg` | Main page background |
| `surface` | `--surface`, `--panel` | Main cards and panels |
| `surfaceRaised` | `--surface-raised`, `--panel2` | Raised panels and secondary surfaces |
| `text` | `--text` | Primary text |
| `muted` | `--muted` | Secondary text, labels and supporting copy |
| `border` | `--line` | Borders and separators |
| `accent` | `--lime`, `--green` | Primary highlight, active states and key actions |
| `accentSecondary` | `--green2` | Secondary accent |
| `warning` | `--orange` | Warnings and attention states |
| `danger` | `--red` | Errors, destructive and danger states |

All ten color keys are required. Use sufficient contrast between text and its background. The website maps the generic theme tokens onto the color variables used by its different page styles.

### Typography

Typography is configured in the `typography` object. Font family names must be selected from the website's approved font list; themes cannot load arbitrary fonts or external font URLs.

| JSON key | Type / allowed values | Purpose |
|---|---|---|
| `body` | Font name | Main body and interface font |
| `display` | Font name | Headings and display text |
| `mono` | Font name | Monospaced text, numbers and technical details |
| `bodySize` | Number, 12–20 | Base body size in pixels |
| `headingScale` | Number, 0.75–1.5 | Scale factor for primary headings |
| `smallScale` | Number, 0.75–1.5 | Scale factor for compact labels and metadata |
| `bodyLineHeight` | Number, 1.2–2 | Body text line-height multiplier |
| `headingLineHeight` | Number, 0.85–1.4 | Heading line-height multiplier |
| `letterSpacing` | Number, -0.05–0.1 | Body letter spacing in em |
| `headingLetterSpacing` | Number, -0.1–0.05 | Heading letter spacing in em |
| `bodyWeight` | 400, 500, 600, 700, 800 | Body font weight |
| `displayWeight` | 400, 500, 600, 700, 800 | Heading font weight |
| `smallWeight` | 400, 500, 600, 700, 800 | Compact label / metadata font weight |

Approved font families and available weights:

| Font | Type | Available weights |
|---|---|---|
| Manrope | Sans-serif | 400, 500, 600, 700, 800 |
| DM Sans | Sans-serif | 400, 500, 600, 700, 800 |
| Space Grotesk | Sans-serif / display | 400, 500, 600, 700 |
| DM Mono | Monospaced | 400, 500 |
| System UI | System sans-serif | Browser / operating-system defaults |
| Georgia | Serif | Browser / operating-system defaults |

The website loads the web fonts it offers through Google Fonts. System UI and Georgia use local system/browser fonts. The default theme typography is Manrope for body and display, DM Mono for monospace, with a 16px body size and a 1.0 scale for headings and compact text.

### Shapes

| JSON key | Range | Purpose |
|---|---:|---|
| `cardRadius` | 0–28 | Card and panel corner radius, in pixels |
| `controlRadius` | 0–28 | Buttons and control corner radius, in pixels |
| `heroRadius` | 0–40 | Hero container corner radius, in pixels |
| `borderWidth` | 0–4 | Theme-controlled border thickness, in pixels |

### Effects

| JSON key | Allowed values | Purpose |
|---|---|---|
| `shadow` | `none`, `soft`, `strong` | Predefined card shadow |
| `hoverLift` | 0–4 | Hover lift distance, in pixels |
| `motionMs` | 0–600 | Transition duration, in milliseconds |

### Background images

The `backgrounds` object supports `page` and `hero`. Each accepts `null` or an approved HTTPS image URL. URLs are restricted to approved public NoteSMP asset repositories and the existing Minecraft Wiki image location. Add new image assets to the public resources repository rather than embedding data URLs or external tracking URLs.

## Editing a theme

Edit only the JSON file for the slot you are designing. Preserve the property names and types in the starter file. All listed color, shape, effect, background and typography settings are validated. The website falls back to the Default theme if a theme cannot be loaded or contains invalid settings.

Do not add HTML, JavaScript, CSS, API configuration, player data or secrets to this repository.

## Previewing

Choose Theme 1–4 in the selector at the bottom of the website. The choice is stored in that visitor's browser and does not change the theme for anyone else.
