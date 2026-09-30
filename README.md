# kitchen-board

A single-page kitchen display for a tablet: a paper-style weekly menu (Events | Lunch | Dinner), a Grab & go list, a recipe library, timers, and a shortcut to AnyList. Hosted on GitHub Pages.

## Files

- **index.html** is the whole app. GitHub Pages serves this file.
- **menu.json** is optional. It carries dinners for one dated week so they can be imported onto the tablet.

## Where the data lives

Everything you type on the tablet (events, lunches, dinners, cooks, the Grab & go list, past weeks, recipes, photos) is stored **in the tablet's browser only**. None of it is written to this repo. Use **Export recipe library** in the Recipes tab to download a backup.

This repo is public. Do not put names, addresses, medical details, or event schedules in `menu.json`.

## menu.json format

```json
{
  "weekOf": "2026-09-28",
  "days": {
    "mon": { "dinner": "Dish name", "notes": "Optional prep notes" },
    "tue": { "dinner": "Dish name" }
  }
}
```

- `weekOf` is the Monday of the week, as `YYYY-MM-DD`. A date that isn't a Monday snaps back to that week's Monday.
- `days` uses the keys `mon` `tue` `wed` `thu` `fri` `sat` `sun`. Include only the days being planned. Days left out are never touched.
- `dinner` is the dish name. Extra lines (separated by `\n`) show under it on the board.
- `notes` is optional. It shows in the dish's recipe card, not on the grid.
- `cook` is optional. It adds a "<name> cooks" tag.
- There are no `events`, `lunch`, `version` or `plans` fields. Files in the old format are ignored.

## How an update reaches the tablet

The tablet checks `menu.json` every few minutes and whenever the page is reopened. When the file's contents for a week differ from what was last imported, a banner appears. Tapping it opens a day-by-day review: checked days are brought in, unchecked days are skipped. Events and lunches are never changed by an import. There are no version numbers to bump. Change the file and the banner returns.

The **Import dinners** button on that week reopens the review any time.

## When asking an AI to write a menu.json

Point it at this README, or paste the current `menu.json` as a format example.
