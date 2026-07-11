---
name: verify
description: Drive the Pomodoro app in a real browser to verify changes end-to-end.
---

# Verifying the Pomodoro app

Single-file vanilla app: `index.html`. No build step, no server. The surface
is a browser window, so verification means driving it with Playwright and
screenshotting.

## Handle

Playwright is not a project dependency. Install it in your scratchpad, not the repo:

```bash
cd "$SCRATCHPAD" && npm init -y && npm install playwright && npx playwright install chromium
```

Load the page over `file://` (URL-encode the spaces in the path):

```js
const APP = 'file:///Users/natjohnson/Library/CloudStorage/Dropbox/Claude%20Code/Projects/code%20projects%202026/pomodoro/index.html';
```

## Fast-forward the clock

Every timer uses `setInterval(fn, 1000)`. Never wait in real time — use
Playwright's clock API, installed **before** `goto` and re-installed after
every `reload()`:

```js
await page.clock.install();
await page.goto(APP);
await page.clock.runFor(60_000);   // 60 timer ticks, instantly
```

Shorten durations first (settings modal → 1 min) so a full run is ~4 min of
mocked time.

## Gotchas

- **Pomodoro expiry lags one tick.** `tick()` checks `timeLeft<=0` at the *start*
  of the next call, so a 25-min timer fires `done!` at 25min **+1s**. Pre-existing;
  the routine runner advances at exactly N seconds. Don't report as a regression.
- **`body` has `transition: background 0.4s`.** Reading `backgroundColor` right
  after a tab/mode switch returns a mid-transition value. `await page.waitForTimeout(600)` first.
- **`.empty-state` and `.drag-handle` exist in both panels.** Scope selectors:
  `#panel-routine .empty-state`.
- **Number inputs reject letters.** `page.fill(el, 'abc')` throws. Use
  `fill('')` + `pressSequentially('abc')`; the value lands as `''`.
- **Each `browserContext` gets fresh `file://` localStorage**, so runs are isolated,
  but a `reload()` within one run keeps state — useful for persistence checks.

## Drag and drop

Rows arm `draggable` on the handle's `mousedown`, so `dragTo()` on the row won't
work. Drive the mouse from the handle and jiggle to trigger the HTML5 drag:

```js
await row.locator('.drag-handle').hover();
await page.mouse.down();
await target.hover();
await page.mouse.move(200, 200, { steps: 4 });   // jiggle
const b = await target.boundingBox();
await page.mouse.move(b.x + b.width/2, b.y + 2, { steps: 4 }); // top half = insert before
await page.mouse.up();
```

## Flows worth driving

- Pomodoro: start / pause / reset / skip, mode tabs, dot + per-task 🍅 increment on expiry.
- Settings: gear opens, Escape + backdrop close, Cancel discards, Save applies and survives reload.
  Saving while the timer runs must not reset the remaining time.
- Routine: add / rename / remove / drag-reorder steps, global default vs per-step override
  (blank input = use default), auto-advance, timeline `current`/`done` classes, completion state.
- Both timers keep ticking while the other tab is shown.
- Durations clamp to [1,180]; blank or non-numeric falls back to the default.
