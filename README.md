# Bandit Training Guide

Find your next training spot in MapleStory Classic World. This is a community-built guide where players submit their EXP and meso rates, party setups and attack ranges, and anyone can browse the results by level.

**Live site:** https://bluegreytiger.github.io/maple-exp-meso-estimator/

**Add a report:** https://docs.google.com/forms/d/e/1FAIpQLSfNgBMdrfM-7W5Z3FxT0aJmV_ffxNWr3RMmB1Y8XkTJHtmhrg/viewform

## What it does

- Lists training maps with the median (or best) EXP/hr and meso/hr reported by players.
- Filters by your level (with a ± range), skill, time to kill, party size and how recent the reports are.
- Shows top picks for your level: best EXP, best meso and easiest party to find.
- Flags maps with limited data, and lists maps nobody has reported yet.
- Shows the monsters in each map (with icons, levels and spawn counts) and lets you search by monster name.
- Estimates how long a map takes per level once you enter your level, using the game's EXP table.
- Click column headings to sort, pin favorite maps, compare up to three maps side by side, and see the latest reports.
- Expands each map to show every individual report, including attack range, skill, time to kill and notes.
- Links each map name to its page on NiaMeowDB, and each map has an "Add a report" button that opens the form with that map pre-selected.
- Remembers your level between visits and can copy a link to your current filters.
- Works on phones and computers, follows your device's light or dark setting (with a manual switch), and keeps a saved copy of the data in case the spreadsheet can't be reached.

## How it works

There is no server or build step. The whole site is a single `index.html` file.

1. Players submit reports through a **Google Form**.
2. Responses land in a linked **Google Sheet**.
3. The sheet is **published to the web as CSV**.
4. `index.html` fetches that CSV in the browser, groups the reports by map and renders the results.
5. The site is hosted for free on **GitHub Pages**.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The entire site: layout, styles and logic |
| `og.png` | Preview image used when the link is shared (Discord and similar) |
| `README.md` | This file |

## Setup (if you want to run your own copy)

1. Create a Google Form with these questions: Map (dropdown), Level, EXP/Hour, Net Meso/Hour, Difficulty to find a party (1-5 scale), Party Size, Party Average Level, Character Stat Attack Range, Main Attacking Skill, Time to kill and Additional Notes.
2. Link the form to a Google Sheet (Responses tab, then Link to Sheets).
3. In the sheet, go to **File, Share, Publish to web**, choose the responses tab and the **CSV** format, then publish and copy the link.
4. Open `index.html` and edit the settings near the top of the `<script>` section:

   ```js
   const CSV_URL  = "your published CSV link";
   const FORM_URL = "your form's viewform link";
   const MAP_ENTRY = "entry.1234567890"; // the Map question's ID
   ```

   To find the Map question's ID, use the form's three-dot menu, then **Get pre-filled link**, pick any map, submit, and copy the `entry.` number from the link.
5. Put the files in a GitHub repo and turn on **Settings, Pages** (deploy from the `main` branch, root folder).

The page matches spreadsheet columns by the words in their headers (for example "EXP", "Meso", "Party size", "Attack range"), so small wording changes in your question titles are fine.

## Maintaining the data

- **Hide a bad report:** add a column headed `Hide` to the responses sheet and type anything in that row. The row disappears from the site but stays in the sheet.
- **Map list:** the Map dropdown in the form can be kept in sync with the OSMS map list using a small Google Apps Script on a daily timer. Those scripts live in Google Apps Script, not in this repo.
- **Input checks:** the EXP and meso questions can be limited to numbers like `100k`, `1.5m` or `100,000` with form validation.
- **Backups:** make a copy of the responses sheet now and then. Version history in Google Sheets can restore it if something is damaged.
- The published CSV is public, so anyone can read every response, including notes. Don't ask for anything private in the form.

## Credits

- Map list, map IDs and monster spawn data: [OSMS Data Explorer](https://osmsdataexplorer.com) by @ohmi, licensed [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Game content (names, text, stats, images) is © Nexon and is not covered by that license.
- Map pages and the EXP table: [NiaMeowDB](https://meowdb.com/msclassic/maps).
- The layout was inspired by an existing community training guide for the game.
- All numbers come from player submissions.

## Disclaimer

Unofficial fan project, not affiliated with or endorsed by Nexon. MapleStory is a trademark of Nexon. Rates are player-submitted estimates and are not guaranteed. Gear, route, party and uptime change the outcome.
