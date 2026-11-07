# NoteSMP Themes

This repository contains **visual themes only** for the NoteSMP website.

The website layout, routes, content, API calls, player data, and application behavior remain in [notesmp-website](https://github.com/NoteSMP/notesmp-website). Theme contributors should not need access to that repository.

## Theme slots

| Website option | File |
|---|---|
| Default | Built into the website; preserves the current NoteSMP design |
| Theme 1 | `themes/theme-1.css` |
| Theme 2 | `themes/theme-2.css` |
| Theme 3 | `themes/theme-3.css` |
| Theme 4 | `themes/theme-4.css` |

The four starter files currently match the existing design. They are intentionally blank design slots until a visual direction is chosen.

## What themes may change

- Colors and gradients
- Backgrounds and decorative background images
- Border color, thickness and roundness
- Shadows, glow and surface treatments
- Typography and font styling
- Small hover effects and animations
- Spacing only when it does not change the page layout or content hierarchy

## What themes must not change

- HTML, JavaScript, routes or page structure
- Section visibility, ordering, placement or assignment
- API endpoints, data fetching or player information
- Navigation behavior, forms, controls or accessibility behavior
- Website deployment configuration or secrets

Do not use CSS to hide, remove, reorder, or disable website sections or controls.

## Editing a theme

Edit only the CSS file for the slot you are designing. Keep selectors scoped to visual styling and preserve responsive behavior. Use `:root[data-theme="theme-1"]` (replace the slot name as appropriate) for theme variables.

The website loads the selected CSS file from this repository. Changes to the `main` branch may take a short time to appear because the public CDN caches files.

## Previewing

Choose the corresponding Theme 1–4 option in the theme selector at the bottom of the website. The visitor's selection is saved in their own browser and does not change the theme for other visitors.
