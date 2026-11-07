# Pouch

Pouch is Kormie's launch-week companion page for WoW: Forever: one screen at a
time for Kooala the gnome priest, with a week plan, progress bars, the kit
(macros and bindings) and a session log. This repository is the GitHub Pages
copy: https://kormie.github.io/pouch/

## Three copies, one truth

- **The private page** on claude.ai is the editable one. It syncs through the
  account, so the phone and the Mac see the same state.
- **This mirror** is the same `index.html` served by GitHub Pages. With no
  claude.ai runtime around it, the page reads `state.json` beside it and shows
  that. Anything changed here stays in that browser until the next refresh of
  `state.json` replaces it, so it is for reading, not editing.
- **The game** is where most of the data comes from. The
  [Pouch Scribe](https://github.com/kormie/pouch-scribe) addon writes every
  session to `PouchScribe.lua`; a scheduled courier merges that into the
  private page's state with the page's own intake code, then commits the
  merged state here as `state.json`.

```
game (Pouch Scribe) -> PouchScribe.lua -> courier -> private page (db)
                                                 \-> state.json -> this mirror
```

## Running it elsewhere

`index.html` is self-contained (no build, no dependencies). Open it from disk
and it runs standalone with its state in the browser's localStorage; serve the
folder (`python3 -m http.server`) and it also reads `state.json`.

`state.json` is the whole state document: level, week hours, checklists,
decisions, profession and talent bars, the session log. The courier overwrites
it; do not edit it by hand.

MIT, see LICENSE.
