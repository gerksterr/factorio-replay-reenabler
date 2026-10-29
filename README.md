# Factorio Replay Re-enabler

**Use it:** https://gerksterr.github.io/factorio-replay-reenabler/

Factorio switches replay recording off when you load a save in a newer version of the game. This page switches it back on, with the replay starting from the save's current state. The save stays a normal Freeplay game: no scenario, no map editor, no mods.

Everything runs in your browser. The save is never uploaded.

## At every game update

1. Load your latest save in the new version and immediately **Save as** a new name, for example `mybase_2.1.24`. Quit to the menu.
2. Drop that save on the page and save the result.
3. Put the result in your `saves` folder in place of the file you dropped, and keep playing from it.

Each save then holds the replay for one game version. Watch it in that version of Factorio (old versions: <https://factorio.com/download/archive>, standalone zip). Saving during a replay gives you a normal save you can keep playing from.

## What it changes

A Factorio save keeps its replay as two files: `level-init.dat` (the map when recording started) and `replay.dat` (every input action since, append-only). On a version change the game sets the replay flag in the map header to off and drops `replay.dat`.

The page:

- sets the replay flag (one byte in the map header) back to on,
- replaces `level-init.dat` with the save's current map state,
- writes an empty `replay.dat`,
- copies every other file in the zip unchanged.

Because the replay now starts from your whole base rather than an empty map, saves get bigger by roughly one compressed copy of the base at the time of the update.

## Known issues

- While watching a replay, keep the mouse off inventory windows the replay opens. Hovering over a slot crashed the game in testing (a crash in the game's own input handling).
- With mods, a replay only plays back with exactly the same mods and versions.

Tested with Factorio 2.1.23 → 2.1.24 (Space Age, no mods). The page understands saves from 2.0 and 2.1 and refuses anything else. Keep a backup of saves you care about.

Unofficial. Not made by or affiliated with Wube Software.
