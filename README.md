# Factorio Replay Re-enabler

**Use it:** https://gerksterr.github.io/factorio-replay-reenabler/

Factorio switches replay recording off when you load a save in a newer version. This page switches it back on, with the replay starting from the save's current state. The save stays a normal Freeplay game: no scenario, no map editor, no mods.

Everything runs in your browser. The save is never uploaded.

## At every game update

1. Before you load your save in the new version, open your Factorio `saves` folder and copy the save you last made with the previous version, for example `MySave.zip`. Name the copy after that version, for example `MySave_2.1.23.zip`. It keeps the whole replay of that version.
2. Start the new version, load `MySave`, save it under the same name and quit to the menu. Only the game can convert a save to its new version, and this is also when it switches replay off.
3. Drop `MySave.zip` on the page and save the result.
4. Replace `MySave.zip` in your `saves` folder with the downloaded file and keep playing.

Your save keeps its name; only the copies of finished versions carry a version number. Anything you play between steps 2 and 4 isn't recorded.

Each version's copy plays in that version of Factorio (old versions: <https://factorio.com/download/archive>, standalone zip). You can't move the camera freely during a replay: save during it and load that save to look around.

## Extra: start a replay later

To skip the first hours of a long replay:

1. Load your save, choose **Start replay** and save when it reaches the moment the new replay should start (for example `MySave_5h45.zip`).
2. Drop that save and the original on the page.
3. Put the result (`MySave_from_5h45.zip`) in your `saves` folder, load it and choose **Start replay**.

Saves made during a replay contain exactly the actions played so far, so the page can cut the original's action log at that point without decoding it. An earlier normal save of the same game works as the start point too.

## What it changes

A Factorio save keeps its replay as two files: `level-init.dat` (the map when recording started) and `replay.dat` (every input action since, append-only). On a version change the game sets the replay flag in the map header to off and drops `replay.dat`.

**Switching replay back on** sets the replay flag (one byte in the map header) back to on, replaces `level-init.dat` with the save's current map state and writes an empty `replay.dat`.

**Starting a replay later** takes the save with the full replay, replaces its `level-init.dat` with the map from the later start point and its `replay.dat` with the actions after that point.

Every other file in the zip is copied unchanged.

Because the replay now starts from your whole base rather than an empty map, saves get bigger by roughly one compressed copy of the base at the time of the update.

## Known issues

- While watching a replay, keep the mouse off inventory windows the replay opens. Hovering over a slot crashed the game in testing (a crash in the game's own input handling).
- With mods, a replay only plays back with exactly the same mods and versions.

Tested with Factorio 2.1.23 and 2.1.24 (Space Age, no mods). The page understands saves from 2.0 and 2.1 and refuses anything else. Keep a backup of saves you care about.

Unofficial. Not made by or affiliated with Wube Software.
