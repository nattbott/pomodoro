# 🍅 Pomodoro Timer

A custom Pomodoro timer built with vanilla HTML, CSS, and JavaScript. Inspired by [Pomofocus.io](https://pomofocus.io).

**Live app:** https://nattbott.github.io/pomodoro

---

## Features

- **Pomodoro / Short Break / Long Break** modes with animated countdown ring
- **Multiple task categories** — create named groups like "History Class" or "Finance"
- **Drag and drop** — reorder tasks within a category, or drag tasks between categories. Reorder categories too.
- **Per-task pomodoro counter** — tracks how many focus sessions each task has accumulated 🍅
- **Alarm sounds** — choose between Bell, Digital, or Soft Chime, with adjustable volume
- **Persistent storage** — tasks and categories are saved to localStorage and survive page refreshes
- **Tomato favicon** — because of course

---

## How to use

1. Add a category (e.g. "Work", "Study")
2. Add tasks inside each category
3. Click a task to make it active
4. Start the timer — completed pomodoros are automatically logged to the active task
5. Take a break when the alarm fires, then repeat

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
