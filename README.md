# Gym Tracker

A personal workout tracking web app built as a single HTML file. Designed for mobile use, installed as a PWA on iPhone via Safari. No backend, no account required — all data lives on your device.

---

## Live App

```
https://usr241198.github.io/gym-tracker
```

Open in Safari on iPhone → Share → Add to Home Screen.

---

## Features

- 4 pre-loaded workout days with exercises, weights and rep ranges
- Log sets in the format `weight × reps` (one per line)
- Automatic progression tracking — updates symbol after each exercise
- Auto weight update when reps are achieved
- Go back to previous exercises mid-session to correct mistakes
- Add notes per exercise and per session
- Full session history
- Cloud backup via GitHub Gist (auto-syncs after every finished workout)
- Export program and history as CSV
- Copy workout summary as markdown
- Dark mode support
- Installable as a home screen app on iPhone (PWA)

---

## Workout Program

| Day | Name |
|-----|------|
| Day 1 | Upper Pull |
| Day 2 | Lower Glute Heavy |
| Day 3 | Upper Push |
| Day 4 | Lower + Core |

---

## Progression Logic

After each exercise the app calculates a symbol based on your top set:

| Symbol | Meaning | Action |
|--------|---------|--------|
| **+** | Hit top of rep range | Increase weight next session |
| **•** | Within rep range | Stay at this weight |
| **−** | Below rep range | Bad day — weight stays unchanged |

**Auto weight update:** If you log a heavier weight and hit your reps (• or +), the stored weight updates automatically. If you miss your reps (−), the stored weight is left unchanged.

---

## Logging Sets

In the active workout screen, type sets one per line:

```
45 × 10
45 × 9
45 × 8
```

- Use `0 × reps` for exercises where no extra weight is added (e.g. bar only on bench press)
- The app will not advance to the next exercise if the input cannot be parsed
- Use the **← Back** button to return to a previous exercise and correct mistakes

---

## Special Weight Rules

Some exercises have a starting resistance (machine/bar weight) built in:

| Exercise | Starting Resistance |
|----------|-------------------|
| Hip thrust | 22.7 kg |
| Leg press | 75.7 kg |
| Incline machine press | 6.8 kg |
| Front squat | 20 kg (bar) |

For these exercises, log only the **added weight**. The app displays the total automatically.

Some exercises are logged **per hand/side**:
- Single-arm DB row
- Seated hammer curls
- Dumbbell shoulder press
- Step-ups

---

## Data Storage

| Where | What |
|-------|------|
| iPhone Safari LocalStorage | All workout data, session state, history |
| GitHub Gist (private) | Automatic cloud backup after every finished workout |

- Data is private and stored only on your device
- The GitHub token is stored in Safari LocalStorage only — it is never in the app code
- If Safari storage is cleared, data can be restored from the Gist backup

---

## Cloud Sync Setup

Cloud sync is optional. To enable it:

1. Create a GitHub Personal Access Token with **gist scope only**
   - GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)
2. Create a secret Gist at [gist.github.com](https://gist.github.com)
   - Filename: `gym-tracker-data.json`
   - Content: `{}`
   - Click **Create secret gist**
3. Open the app → **Export tab** → **Set up cloud sync**
4. Enter your token and Gist ID → Save & Connect

The app will auto-sync to your Gist after every completed workout session.

---

## Updating the App

1. Make changes to `index.html` (or get an updated file)
2. Go to the repo on GitHub → click `index.html` → pencil icon to edit
3. Select all → delete → paste new content → commit
4. Wait ~60 seconds for GitHub Pages to deploy
5. Pull to refresh the app on your iPhone — no reinstall needed

---

## Repo Structure

```
gym-tracker/
├── index.html       # The entire app — all HTML, CSS and JS in one file
├── icon2.png        # iPhone home screen icon (180×180px)
└── README.md        # This file
```

---

## Tech

- Vanilla HTML, CSS, JavaScript — no frameworks, no build step
- LocalStorage for persistence
- GitHub Gist API for cloud backup
- GitHub Pages for hosting
- Installed as a PWA via Safari's "Add to Home Screen"
