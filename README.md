# Collins

A coding-agent product site and workstation, built as two static HTML pages — no build step.

| Page | What it is |
|---|---|
| `index.html` | Landing page: 3D hero, a read-only preview of the workstation, models, pocket IDE, integrations. **Get started** opens an install flow that redirects to the workstation. |
| `workstation.html` | The app: tabbed threads with a simulated agent (steps, diffs, terminal, review panel), the prompt bar, and the ad dashboard (watch sponsor ads → earn Rp → convert to tokens that pay for prompts). |

## Run it

Any static file server works. From this folder:

```bash
npx serve .
```

or

```bash
python -m http.server 5179
```

Then open `http://localhost:5179/`. Opening the files straight from disk mostly works too, but a server is closer to production.

## What's inside `workstation.html`

- **Threads** — tabs, hash routing (`#/t/<id>`, `#/ads`), search, new chat, persisted in `localStorage`.
- **Prompt bar** — `@` context menu, `/` commands, model picker, effort slider (Max adds sparks), attachments, dictation, send ↔ stop morph. Port of React Bits *PromptBar*.
- **Thought line** — "Thinking… 3.2s" with a step trace that settles into "Thought for …". Port of React Bits *ThoughtLine*.
- **New-chat backdrop** — WebGL2 ASCII light field. Port of React Bits *GradientASCII*.
- **Ad dashboard** — KPIs, revenue chart with hover, usage (tokens spent per day / model / run), earnings breakdown, conversion at Rp 15.000 → 50M tokens, CSV export.
- **Random ads** — *Slide to play ads* (port of React Bits *SlideCommit*) shuffles the remaining sponsors; the user can't pick.
- **Watch guard** — the ad clock only runs while the tab is visible, focused, large enough and on the ad view. Leaving pauses it, rewinds 2s, flashes the tab title and requires **Resume**. Unfinished ads survive reloads. Tunables live in `GUARD` near the playback code. Reward validation is meant to be confirmed server-side; this is the client half.

## Dependencies (CDN)

- Tailwind CSS Play CDN `3.4.17`
- Three.js `r128` (landing hero)
- Google Fonts: Syne, Instrument Serif, Public Sans, JetBrains Mono

## State

Everything is stored in the browser (`localStorage` keys `collins-*`). Settings → **Reset demo data** clears it.
