# dewmath

Maths tools for further education, starting with a readiness diagnostic for QQI Level 5 Mathematics for IT (5N18396) and Computational Methods (5N0554).

Everything is a single HTML file with no build step and no server. The site is published from this repository with GitHub Pages.

## Layout

| Path | What it is |
|---|---|
| `index.html` | The landing page: what dewmath is, how the diagnostic works, downloads, stages. |
| `diagnostic.html` | The current diagnostic. Open it bare for the teacher builder, with `#c=…` for a student sitting, with `#analyse` for the class analysis page. |
| `versions/` | Earlier stages, kept so that old links and old results files keep working. |
| `samples/` | A simulated class of twelve results files and one v1-format file, for trying the analysis page. |
| `fonts/` | OpenDyslexic (SIL Open Font License), used by the "Font: OpenDyslexic" display setting. |

## How the diagnostic works

The teacher chooses skills, wording, order, time limit and a question cap in the builder. The settings are packed into the link itself (a few bytes, base64url), so the same link always produces the same sitting. Students answer in the browser; their answers save locally as they go; at the end they download a results file and send it wherever the link told them to (a OneDrive file request, a Microsoft Form with a file upload, or an email). The analysis page reads any number of those files and produces the class report. Nothing is uploaded anywhere by the tool itself.

## Editing the item bank

The bank is the `ITEMS` list near the top of `diagnostic.html`. Each item has a plain-language stem, a mathematical-language stem, and options where exactly one carries `ok:1` and every wrong option carries an error tag (`e:"…"`) described in `ERRORS`. Skills live in `SKILLS` with a level (1 foundation, 2 core, 3 advanced). Append new skills at the end and never reorder the list: a skill's position is its bit in the share code.

## Display settings

The "Display" button on every page sets appearance (light, dark, match device), colour scheme (navy and burnt orange, or slate and teal), font (serif, sans-serif, OpenDyslexic), text size and column width. The choice is stored in the browser and applies across the site.
