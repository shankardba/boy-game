# Boy

A tiny single-file browser game: a miniature 3D overworld rendered in the
tilt-shift "diorama" style of the *Zelda: Link's Awakening* remake, played
like a classic 2D top-down adventure — grid movement, a handful of
obstacles, collectible Light Shards, wandering slime enemies, and a couple
of signposts.

Everything lives in `index.html`: Three.js (loaded from cdnjs, no build
step) renders low-poly props on a hand-authored ASCII tile map, a
perspective camera tracks the player from a fixed diorama angle, and two
CSS `backdrop-filter: blur()` bands along the top/bottom edges fake the
tilt-shift depth-of-field look cheaply, without a postprocessing pipeline.
Sound effects are synthesized on the fly with the Web Audio API — no
external assets at all.

## Play

Open `index.html` directly in a browser, or serve the folder:

```bash
cd boy-game
python3 -m http.server 8433
# open http://localhost:8433
```

**Controls:** WASD / Arrow keys to move, Space (or E) to interact with
signs and to poke enemies. On touch devices, an on-screen D-pad and
action button appear automatically. Goal: gather all 6 Light Shards.

## Editing the world

The map is a plain ASCII grid near the top of the `<script>` block:

```
# tree/border   .  grass    , flowers   = path   o rock
~ water         b  bush     H house footprint    S sign
e enemy spawn   $  shard    @ player start
```

Every row must be the same length. Add or move a symbol and the parser
(further down in the script) picks it up automatically — obstacles,
props, shard/sign/enemy lists are all derived from the grid, nothing is
hard-coded twice.

## Integration

This is designed to drop into [shankFiddle](../shankfiddle-site) the same
way the other tools do — copied verbatim into `tools/boy/app.html` behind
a small branded wrapper. See that repo's README for the pattern.
