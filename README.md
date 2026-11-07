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

The four starter files intentionally match the current design. They are ready for individual visual directions.

## Why themes use JSON tokens

Theme files are **data, not executable CSS or JavaScript**. The website validates each value and applies only approved visual properties. This lets contributors adjust appearance without giving them a way to change page structure, hide sections, replace application logic, or alter API behavior through arbitrary CSS.

## What can be themed

- Colors: page, surfaces, text, muted text, borders, accents, warnings and errors.
- Background images: page and hero.
- Shapes: card, control and hero corner radius; border thickness.
- Effects: predefined shadow strength, hover lift and transition duration.
- Typography: approved built-in font choices.

Do not add HTML, JavaScript, CSS, API configuration, player data or secrets to this repository.

## Editing a theme

Edit only the JSON file for the slot you are designing. Preserve the property names and types in the starter file. The website validates values and falls back to the Default theme if a theme cannot be loaded or contains invalid settings.

Background image URLs are restricted to approved public NoteSMP asset repositories and the existing Minecraft Wiki hero image. Add new image assets to the public resources repository rather than embedding data URLs or external tracking URLs.

## Previewing

Choose Theme 1–4 in the selector at the bottom of the website. The choice is stored in that visitor's browser and does not change the theme for anyone else.
