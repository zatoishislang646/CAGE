# CAGE — a game in six films

> A moody, *Limbo*/*Inside*-style 2.5D side-scroller in which Nicolas Cage plays his way through six of his own movies.

![Title screen](docs/screenshots/title.jpg)

**CAGE** is a parody browser game. The world is drawn in dark, foggy silhouettes like *Limbo* and *Inside*. Nicolas Cage is the one thing in color: a hand-animated caricature in a different costume for each chapter. The whole game is one HTML file with no dependencies, no build step and no external assets.

**▶ Play:** open `index.html` in any modern browser, or turn on GitHub Pages for this repo (see [Deploying](#deploying-to-github-pages)).

---

## The chapters

| # | Film | Cage as… | What you're up against |
|---|------|----------|------------------------|
| I | **Con Air** (1997) | Cameron Poe: mullet, tank top, and the bunny | Prison searchlights (hide behind crates), a crate to push onto a pressure plate that opens a gate, falling cargo you can climb |
| II | **National Treasure** (2004) | Ben Gates in Franklin's multi-lens glasses | Laser grids in the archives that switch on and off in timed waves, moving platforms, a spike pit. Steal the Declaration. |
| III | **The Wicker Man** (2006) | Edward Malus in the bear suit | A bee swarm chases you through a foggy forest (*"NOT THE BEES!"*), plus a crate-and-ledge puzzle |
| IV | **Gone in 60 Seconds** (2000) | Memphis Raines, bleached hair and leather jacket | A 60-second clock, oncoming headlights to jump over, crane containers swinging over the docks |
| V | **Ghost Rider** (2007) | Johnny Blaze, half turned into a flaming skull | Fire jets that erupt in waves, falling rocks, lava |
| VI | **The Rock** (1996) | Stanley Goodspeed with the green flares | Climb Alcatraz before the rising VX gas catches you, with a searchlight at the top |

It ends with a *Face/Off* epilogue. Each chapter hides one collectible: the Bunny, the Declaration, the Wicker Doll, Eleanor's Keys, the Contract and the Green Pearl.

| | | |
|---|---|---|
| ![Con Air](docs/screenshots/01-con-air.jpg) | ![National Treasure](docs/screenshots/02-national-treasure.jpg) | ![The Wicker Man](docs/screenshots/03-wicker-man.jpg) |
| ![Gone in 60 Seconds](docs/screenshots/04-gone-in-60-seconds.jpg) | ![Ghost Rider](docs/screenshots/05-ghost-rider.jpg) | ![The Rock](docs/screenshots/06-the-rock.jpg) |

## The characters

![Character sheet](docs/screenshots/characters.jpg)

Each Cage is a painted caricature head on a vector body drawn in code. The body animates its idle, run, jump and push poses, and the head bobs and tilts with the motion. Every character has a signature idle move: Poe hugs the bunny, Gates' glasses glint red, green and blue, Malus flails at the bees, Raines twirls the keys, Blaze swings a burning chain and Goodspeed waves his flares. Open **`characters.html`** to see all six animating side by side.

## Controls

| Action | Keyboard | Touch |
|---|---|---|
| Move | ← → or A / D | Left fifth of the screen = back, second fifth = forward |
| Jump | Space, ↑ or W | Anywhere on the right side |
| Push a crate | Walk into it | Walk into it |
| Restart from checkpoint | R | — |
| Back to menu | Esc | — |
| Jump to a chapter (title screen) | 1–6 | — |

You can also open `index.html?level=4` to start directly in a chapter.

## How it's built

- **One file, no dependencies.** `index.html` holds the engine, the levels, the art and the sound. The painted heads are embedded as base64 WebP.
- **Rendering:** HTML5 Canvas 2D. Three or four parallax background layers, each drawn in code (watchtowers, archive stacks, dead trees, cranes, mesas, cell blocks), get hazier with distance. On top of that sit god rays, ground fog, a vignette, film grain and a slight flicker.
- **Gameplay:** a frame-rate–independent platformer (capped delta time) with axis-separated AABB collision. It has one-way platforms, moving platforms that carry the player, pushable crates, pressure plates and gates, falling objects that become platforms, searchlights with line-of-sight checks (crates block them), timed lasers and fire jets, cars, a chasing swarm, rising gas and checkpoints.
- **Audio:** everything is generated with the Web Audio API: an ambient drone, footsteps, jumps, landings, gunshots, fire and the buzzing of the bees. There are no audio files.
- **Characters:** the heads were generated as painted caricature portraits on a green screen, then cut out with the scripts in `tools/`. The bodies, costumes, props and effects (flames, bees, flares, chain) are drawn in code and animated procedurally.

## Project structure

```
index.html              The complete, playable game (self-contained)
characters.html         Animated character sheet (all six costumes)
assets/heads/           Cut-out head sprites used in the game (PNG with alpha)
assets/portraits/       The original painted portraits the heads were cut from
tools/chroma_key.py     Removes the green background from the portraits (Pillow + NumPy)
tools/crop_heads.py     Crops and masks the heads and writes heads.json for embedding
docs/screenshots/       Images used in this README
```

## Running locally

No install needed. Double-click `index.html`, or serve the folder:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Deploying to GitHub Pages

1. Push this repo to GitHub.
2. Go to **Settings → Pages**, set **Source** to *Deploy from a branch*, and pick `main` / root.
3. The game will be live at `https://<your-user>.github.io/<repo-name>/`.

The `.nojekyll` file is already included, so Pages serves the files as they are.

## Known limitations

- The difficulty has had very little playtesting; the searchlights in Chapter I are probably the hardest part.
- The painted heads don't blink or lip-sync; only the body is animated.
- The touch controls are basic. The game is built for a keyboard first.

## Disclaimer

CAGE is an **unofficial, non-commercial fan parody**. It is not affiliated with, endorsed by or sponsored by Nicolas Cage, Playdead (*Limbo*, *Inside*), or any film studio or rights holder. Film titles and character names belong to their respective owners and are used here only for parody and commentary. The character portraits are AI-generated caricatures. If you are a rights holder and would like something changed or removed, please open an issue.

## License

The **source code** is released under the [MIT License](LICENSE). The license covers the code only. It grants no rights to any third-party names, trademarks or likenesses shown in the game.
