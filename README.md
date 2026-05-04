# NEXUS // Case Files

### Interactive Detective Mystery — Browser Dev Tools Game

-----

## What This Is

NEXUS is a locally-hosted interactive mystery game where players investigate four open criminal cases that all connect to a single conspiracy. The twist: **clues are hidden using real browser developer tools mechanics** — players must inspect page source, check the console, examine DOM elements, read localStorage, and use the Elements inspector to uncover evidence the UI deliberately conceals.

-----

## How to Run

1. Clone this repo
1. Open `index.html` directly in Chrome (double-click or drag into browser)
1. No server needed — runs entirely in the browser

-----

## Current Cases

|Case        |Status|Theme                            |
|------------|------|---------------------------------|
|The Harlow  |OPEN  |Staged murder at a downtown hotel|
|Ghost Signal|ACTIVE|Encrypted radio transmissions    |
|The Hollow  |COLD  |Missing city auditor             |
|Redline     |ACTIVE|Shell company & financial crime  |

All four cases are connected. The conspiracy centers on a single alias: **VALE**.

-----

## Dev Tools Mechanics (Spoilers for Builders)

The game hides clues in the following locations — add more as you expand:

- **HTML comments** — top of `<head>` and throughout body
- **DOM data-attributes** — `#hidden-alpha` element, hidden via `display:none`
- **CSS comments** — inside `<style>` blocks
- **localStorage** — seeded on page load with case data
- **Console messages** — transmission plays on load; hint system via `NEXUS.*` commands
- **Invisible text** — `#cipher-span` with `visibility:hidden`, inspectable in Elements panel
- **`window.NEXUS` object** — accessible from DevTools console with commands:
  - `NEXUS.status()` — shows progress and available commands
  - `NEXUS.unlock("harlow")` — hint for Harlow case
  - `NEXUS.unlock("signal")` — hint for Ghost Signal
  - `NEXUS.unlock("hollow")` — hint for The Hollow
  - `NEXUS.unlock("redline")` — hint for Redline
  - `NEXUS.scan()` — scans DOM for hidden elements
  - `NEXUS.inspect()` — dumps localStorage case data

-----

## How to Expand

### Adding a New Case

1. Add a new nav item in the sidebar with a color-coded dot
1. Add a new `.panel` div with ID `panel-[casename]`
1. Add evidence cards, suspects, timeline entries
1. Add locked evidence that requires a clue from another case
1. Seed new `localStorage` items in the `window.addEventListener('load')` block
1. Add new HTML comments, data-attributes, or hidden elements as clue sources
1. Add a new entry to `NEXUS.unlock()` hints

### Adding Clue Unlock Mechanics

- Password input boxes (like the existing ones) tied to `checkX()` functions
- Console-only unlocks (players must type a specific `NEXUS.*` command)
- Hidden links that only appear when inspecting a specific element
- CSS `:hover` reveals — content visible only by toggling element styles in inspector

### Adding the Endgame

When all cases are connected, reveal VALE’s true identity. Options:

- A final panel that only unlocks after all clue keys are collected
- A special `NEXUS.resolve()` console command that triggers the reveal
- A hidden page (`/vault.html`) referenced only in decrypted evidence

-----

## File Structure

```
nexus/
├── index.html       ← Main game (all cases, all mechanics)
├── README.md        ← This file
└── (future)
    ├── vault.html   ← Endgame reveal page
    ├── assets/      ← Images, audio files
    └── cases/       ← Individual case pages if splitting out
```

-----

## Roadmap Ideas

- [ ] Add audio file clue (requires frequency key to “tune in”)
- [ ] Add a fake login portal as a red herring
- [ ] Create `vault.html` — the endgame page that reveals VALE
- [ ] Add a second conspirator thread after VALE is unmasked
- [ ] Mobile-responsive sidebar (hamburger menu)
- [ ] Save clue progress to localStorage so game persists across sessions
- [ ] Add a “New Game” reset button
