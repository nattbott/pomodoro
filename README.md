# 🍅 Pomodoro Timer

A custom Pomodoro timer built with vanilla HTML, CSS, and JavaScript. Inspired by [Pomofocus.io](https://pomofocus.io).

**Live app:** https://nattbott.github.io/pomodoro

---

## Features

Two tabs across the top: **Pomodoro** and **Routine**.

### Pomodoro

- **Pomodoro / Short Break / Long Break** modes with animated countdown ring
- **Customizable durations** — click the ⚙ gear to set each mode's length (1–180 min)
- **Multiple task categories** — create named groups like "History Class" or "Finance"
- **Drag and drop** — reorder tasks within a category, or drag tasks between categories. Reorder categories too.
- **Per-task pomodoro counter** — tracks how many focus sessions each task has accumulated 🍅
- **Alarm sounds** — choose between Bell, Digital, or Soft Chime, with adjustable volume

### Routine

- **Build an ordered routine** of named steps — Shower, Lotion, Hair, …
- **Global default step length**, overridable per step (leave a step's box blank to use the default)
- **Add, remove, and drag-reorder** steps
- **Auto-advance** — when a step's timer runs out the alarm sounds and the next step begins
- **Alternating step colors** — the background flips between purple and teal on every step, so an advance is obvious even from across the room
- **Progress timeline** along the bottom, with the current step highlighted and finished steps checked off
- **Completion state** when every step is done

Everything — tasks, categories, timer settings, and your routine — is saved to
localStorage and survives a refresh. And there's a tomato favicon, because of course.

---

## How to use

**Pomodoro tab**

1. Add a category (e.g. "Work", "Study")
2. Add tasks inside each category
3. Click a task to make it active
4. Start the timer — completed pomodoros are automatically logged to the active task
5. Take a break when the alarm fires, then repeat

**Routine tab**

1. Set the default step length
2. Add your steps in order, giving any step its own length if it differs from the default
3. Hit **Start routine** — it walks through each step, advancing automatically

---

## Running locally

No build step needed. Just open `index.html` in any browser.

```bash
open index.html
```

---

## Built with

- Vanilla HTML / CSS / JavaScript
- Web Audio API (for alarm sounds)
- localStorage (for persistence)
- No frameworks, no dependencies
