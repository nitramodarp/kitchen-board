# kitchen-board

A single-page kitchen display: weekly dinner menu, recipe library, timers, and a shortcut to AnyList. Hosted on GitHub Pages, meant for a tablet mounted or standing in the kitchen.

## Files

- **index.html** — the whole app (menu grid, recipes, groceries, timers). This is the file GitHub Pages serves.
- **menu.json** — this week's dinners and plans. Edited directly on github.com to push a new week to the tablet.

## menu.json — exact format

```json
{
  "version": "2026-09-23",
  "days": {
    "mon": { "dinner": "Dish name", "plans": "Notes, kid modifications, prep reminders" },
    "tue": { "dinner": "", "plans": "" },
    "wed": { "dinner": "Dish name", "plans": "" },
    "thu": { "dinner": "Dish name", "plans": "" },
    "fri": { "dinner": "Dish name", "plans": "" },
    "sat": { "dinner": "Dish name", "plans": "" },
    "sun": { "dinner": "Dish name", "plans": "" }
  }
}
```

Rules that matter:

- The seven day keys are exactly `mon`, `tue`, `wed`, `thu`, `fri`, `sat`, `sun` — not a `days` array, not full day names.
- Each day is an object with two string fields: `dinner` and `plans`. `plans` can hold multiple lines separated by `\n` (practice times, kid substitutions, prep notes).
- There is no `weekOf`, `lunches`, or `date` field. The board doesn't read a lunch field at all — dinner-only.
- `version` is a plain string, normally the date the menu was written (`YYYY-MM-DD`). It doesn't have to be a real date — it just has to be different from the last one.
- Leave `dinner` and `plans` as empty strings (`""`) for a day with nothing planned. Don't omit the day.

## How updates reach the tablet

The board does **not** auto-apply a new `menu.json`. When it detects the file's `version` has changed, it shows a banner ("Review & import"). Tapping it opens a day-by-day comparison of what's incoming versus what's already on the tablet (including anything typed by hand), and only the days you check get overwritten. This is intentional — the tablet is the primary place the week gets planned by hand, and a background file update should never silently erase that.

## Recipes

Recipes (ingredients with adjustable servings, links, cookbook photos) are **not** stored in `menu.json`. They live only in the tablet's browser storage, attached to a dish name, and build into a library over time via the Recipes tab. There's no file in this repo to edit for recipes — that's all done on the tablet itself. Use the Export button in the Recipes tab to back up the library to a downloadable file.

## When asking an AI to generate a new menu.json

Point it at this README, or paste in the current `menu.json` as a format example, rather than letting it guess field names.
