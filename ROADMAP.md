# Drift — Roadmap

World 1 (the Drift) is built. Everything below is logged, not started.

The long game: the four worlds are the four DreamDesigner tiers, and the abilities
you unlock as you play **are** the score. By the time you finish, the game has already
assessed you — the Blueprint just confirms it in words.

| World | Tier | The lie it breaks | Status |
|---|---|---|---|
| 1 | The Drifter | "Something will come along." | **Built** |
| 2 | The Dreamer | "I know what I want, it's in my head." | Logged |
| 3 | The Builder | "I set goals. I just don't stick to them." | Logged |
| 4 | The Designer | "I've got the system. Now what?" | Logged |

---

## World 2 — The Dreamer
**DreamDesigner section: Goals**

> *"You know what you want. It lives in your head, which is the one place a goal
> cannot work from. The gap is capture, not desire."*

You can **see** the flag from the opening frame. You cannot reach it. Every route
runs out, every ledge stops short, and the flag stays exactly as far away as it was.

The level only becomes completable as you perform the four capture behaviours the
Blueprint actually asks about:

| Behaviour | Blueprint question | Mechanic |
|---|---|---|
| Write it | `goals_written` | already done in World 1 — carries forward |
| Picture it | `goals_pictures` | collect image fragments; the assembled picture rises into the sky as a permanent landmark you can navigate by from anywhere |
| Speak it | `goals_speak` | checkpoints don't activate on touch, they activate on your voice — mic on, say it, the flag plants |
| Look at it | `goals_look` | a "look up" input; the longer since you last looked, the more the path ahead dims |

The lesson is structural: a goal you can see but never touch is not a goal, it's a view.

**Build notes:** the voice checkpoint is the risky one — Web Speech API, permission
prompt, and a typed fallback that has to not feel like the consolation prize. Prototype
that alone before committing to the world.

---

## World 3 — The Builder
**DreamDesigner sections: Daily Practice + Action & Follow-Through**

> *"You set goals and you return to them. What is missing is rhythm, the daily contact
> that turns a plan into an identity."*

The streak world. **Your jump height is your streak.** Play today, the boots hold.
Miss a day, they reset, and the gap you cleared yesterday will physically not let you
through — you have to go back and earn the height again.

Not a punishment. Just honest physics. This is the only world that can't be finished
in one sitting, by design, and it's the one that turns the game into a daily ritual.

Also here:
- **The ghost** (`act_track`) — every run leaves a translucent ghost of your last
  attempt. Later sections are only readable by watching where the ghost died.
- **Get back on** (`act_back`) — one counter, and it's the only score in the game:
  seconds between falling and moving again. Not deaths. Recovery time.
- **Unfinished business** (`act_finish`) — any section you abandon partway stays on
  the map, grows, and leaks obstacles into the sections you're trying to finish now.

**Build note:** this is the world that needs persistence — `localStorage` at minimum,
an account if it ever needs to survive a device change. Everything up to here is
stateless, so World 3 is where the architecture actually changes.

---

## World 4 — The Designer
**DreamDesigner sections: Environment & Influence + Mindset & Belief**

> *"You are running the loop most people never start: written, seen, spoken, revisited.
> Your work now is depth, not repair."*

The flag is easy to reach. That's the twist — World 4 isn't about arriving, it's about
what you're carrying and who's in the room.

- **Carry** (`env_people`) — you wear a backpack of NPCs. Some are anchors, some are
  balloons. Drop-off stations let you choose who rides. Nobody comments on it.
- **Rooms** (`env_rooms`) — a hub of doors. Standing in a room of people further along
  than you fills your meter. A room of drifters drains it. No combat, just proximity.
- **Noise** (`env_input`) — ads, notifications, and autoplay video spawn as obstacles
  from the background. One powerup, an input filter, stops the spawns.
- **Self-talk** (`mind_selftalk`) — your own thought bubbles render as terrain. Kind
  ones are platforms. Cruel ones are spikes. Every fork asks you to pick a line about
  yourself.
- **Go again** (`mind_again`) — the level gets measurably *easier* the more you retry,
  and tells you so. Quitting is the only failure state the game has.

---

## Cut from the original fifteen, still good

Ideas that didn't make the four-world spine but shouldn't be lost:

- **Two Brothers** — split screen, one controller, identical inputs. One character has
  a lit path and a visible flag, one has neither. Sixty seconds, no text. This is the
  most *shareable* thing on the whole list — a single screenshot that argues the entire
  thesis — and it's a weekend build. Strong candidate for a standalone teaser that
  points at Drift, rather than a world inside it.
- **Blueprint** — a plan screen before each level where you place three platforms
  yourself, then play the level you drew. A bad plan makes an unwinnable level and you
  go back and re-plan. Fits `prac_plan` ("plan the day before the day starts") better
  than anything currently in World 3.
- **Lantern** — dark cave, two tiles of visibility, and each goal behaviour widens the
  light one ring. Clarity as literal sight distance. Overlaps World 2's "look at it"
  mechanic; might be the better version of it.

---

## Open questions

- **Mobile.** Touch works and portrait is framed correctly, but a phone shows a narrow
  slice of world. Worth a portrait-specific camera before this gets shared anywhere
  people will open it on a phone — which is everywhere.
- **Sound.** There is none. The drift phase in particular is asking for a loop that
  never resolves, and a resolution the moment the goal is written. Probably the single
  highest-impact addition per hour spent.
- **Does the Esc nudge appear too late?** Currently 40 seconds. Untested on anyone who
  isn't Josh. Watch a real player before changing it.
- **Capture.** The win screen hands off to the Blueprint rather than taking an email
  itself. Right call while Drift is a static file. Revisit if it ever outperforms the
  Blueprint's own front door.
