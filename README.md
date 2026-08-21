# Drift

A short game about what happens before you decide what you want.

You start with no instructions and no finish line. The screen scrolls right whether
you press anything or not. You dodge, you fall, you respawn, you carry on. There is
no score, no lives, and no way to lose — the only number on screen counts up.

Most people hit `Esc` after about a minute, looking for the exit. What they find is
a single empty field: **What do you actually want?**

Type anything. The scrolling stops. The camera hands itself to you. Your words appear
on the flag at the end of the level, and for the first time falling costs something —
you go back to the last flag you passed, because now there is something to lose.

Then it hands you off to [The Dream Designer Blueprint](https://dreamdesigner.lifesong.io).

---

## Run it

Open `index.html`. That's it — no build step, no npm, no server required.

For a local server (needed only if you want a real URL for testing on your phone):

```bash
cd drift-app && python3 -m http.server 4830   # then http://localhost:4830
```

Deploy: drag the folder into Vercel, or point any static host at it.

## Controls

| | |
|---|---|
| Move | `←` `→` or `A` `D` |
| Jump | `Space`, `↑`, or `W` |
| The field | `Esc` |
| Touch | outer thirds steer, centre jumps |

## How it's built

One file. `index.html` holds the markup, the styles, and the game — vanilla JS on a
2D canvas, no engine and no dependencies. At this size an engine would cost a day
and buy nothing.

The overlays (title, the field, the win screen) are real DOM, not canvas. That's
deliberate: it gets Montserrat, the 30% tracking, and a working text input for free,
and it keeps the type identical to the app this game hands off to.

**State machine:** `title → drift → (field) → turn → walk → win`

`field` is an overlay on top of `drift`, not a state of its own, because you are
allowed to walk back out of it and keep drifting. `Esc to keep drifting` is on that
screen on purpose. The refusal has to be available or the choice isn't one.

## Tuning

Everything worth adjusting is in the `CFG` block at the top of the script:

| Setting | Default | What it does |
|---|---|---|
| `DREAMDESIGNER_URL` | `dreamdesigner.lifesong.io` | where the win screen sends people |
| `ESC_HINT_AT` | `40` | seconds of drifting before the faint `Esc` nudge appears |
| `DRIFT_SPEED` | `190` | px/s the camera shoves you right |
| `WALK_LENGTH` | `2600` | px of designed path after you decide |
| `PX_PER_M` | `8` | world pixels per displayed "meter" |

Difficulty lives in `genDriftChunk()`. The drift is meant to be **dull, not hard** —
a player who is scrambling to survive is engaged, and engagement is the one thing
act one must not give them. Most of the world is continuous ground on purpose.

## Design rules

1. **The mechanic teaches, not the text.** Nothing in this game explains goal-setting.
   The controller does.
2. **Drifting doesn't kill you.** Infinite respawn, zero penalty, no game over. A game
   that kills you for drifting is lying — drifting is completely survivable, and that
   is the actual problem.
3. **Nothing is at stake until something is chosen.** Deaths start costing ground the
   moment a goal exists, and not one second earlier.
4. **Shape carries meaning, never colour.** Platforms are rectangles, hazards are
   triangles, flags are flags. The whole palette is black and white, and it would still
   be fully playable if it weren't.
5. **The palette is DreamDesigner's**, copied from `dreamdesigner-app/app/globals.css`.
   If that moves, move this. The handoff only feels like one product while they match.

## Roadmap

Worlds 2–4 are mapped in [ROADMAP.md](ROADMAP.md).
