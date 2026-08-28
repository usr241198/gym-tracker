# Gym Tracker

A personal workout tracking web app built as a single HTML file. Designed for mobile use, installed as a PWA. No backend, no account — all data lives on the device. 

## Progression Logic

After each exercise the app calculates a symbol based on top set:

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

Some exercises have a starting resistance (machine/bar weight) built in. 

For these exercises, log only the **added weight**. The app displays the total automatically.

Some exercises are logged **per hand/side**:
- Single-arm DB row
- Seated hammer curls
- Dumbbell shoulder press

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

The app will auto-sync. 

---

## Tech

- Vanilla HTML, CSS, JavaScript — no frameworks, no build step
- LocalStorage for persistence
- GitHub Gist API for cloud backup
- GitHub Pages for hosting
- Installed as a PWA via Safari's "Add to Home Screen"
