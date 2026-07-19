# Guitar Practice

A simple, self-contained guitar practice app built around a four-week restart plan.

The app is designed to remove the friction of deciding what to practice. Pick your current week and session, start the lesson, and follow the on-screen instructions. Each practice section has a countdown timer and automatically advances when time is up.

## Features

* 4-week, 8-session structured guitar practice plan
* 30-minute guided practice sessions
* Countdown timer for each section
* Automatic progression between practice sections
* Pause, resume, skip, back, and reset controls
* Session timeline showing current progress
* Local progress persistence using `localStorage`
* Responsive layout for desktop and mobile
* No framework, build step, package manager, or external dependencies

## Running Locally

The project is a static HTML app.

You can open `index.html` directly in a browser, or serve the directory with the included dev server script:

```bash
./bin/serve
```

This starts a local web server on port 9000 (pass a different port as the first argument, e.g. `./bin/serve 8080`). Then open:

```text
http://${DOMAIN}:${PORT}
```

## Deployment

The app is deployed via GitHub Pages (serving `main` at the repo root) at:

```text
https://blog.mark-roddy.com/guitar-practice/
```

### Linking to a specific session

You can deep-link directly to a lesson's overview with URL parameters — handy for a calendar event that points at the day's session:

```text
https://blog.mark-roddy.com/guitar-practice/?session=5
https://blog.mark-roddy.com/guitar-practice/?week=3&session=5
https://blog.mark-roddy.com/guitar-practice/?week=3&part=2
https://blog.mark-roddy.com/guitar-practice/?w=3&p=2
```

Supported parameters (each has a long and short form):

* `session` / `s` — absolute session number (1–8, unique across the plan). Enough on its own.
* `week` / `w` + `session` / `s` — explicit week and absolute session.
* `week` / `w` + `part` / `p` — the first (`part=1`) or second (`part=2`) session *within* that week. Useful when you think in terms of "week 3, second session" rather than the absolute session number.
* `week` / `w` alone — that week's first session.

An explicit link always opens that lesson's overview, ignoring any saved progress, so the link is deterministic. As you navigate sessions in the app, the address bar stays in sync (normalized to `?week=W&session=S`) so the current URL is always shareable.

## Project Structure

```text
.
├── bin/
│   └── serve       # local dev web server
├── index.html
└── README.md
```

All application code, styles, lesson content, and timer logic are contained in `index.html`.

## Practice Structure

Each 30-minute session is divided into a few focused sections drawn from three broad categories:

1. **Mechanics / vocabulary** — scales, pentatonic phrasing, chord changes, and fretboard familiarity
2. **Song work** — learning, troubleshooting, or maintaining a current song
3. **Repertoire / playing** — recovering old songs and spending time simply playing music

Across the four weeks, songs move through a loose progression:

```text
Learning → Polishing → Repertoire
```

The goal is not to perfect one song indefinitely, but to keep music moving through the system while rebuilding a consistent guitar-playing habit.

## Progress Saving

The app stores the current lesson and section in the browser using `localStorage`.

Progress is specific to the browser and device being used. Clearing browser storage will reset saved progress.

