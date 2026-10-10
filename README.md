# Midnight Video

A tiny 16-bit video store you walk around at night. Browse twelve horror shelves, grab tapes blind, and take them to the counter. The clerk decides which one you keep, unless you gamble on the Choice of the Day.

**Live site:** `https://empty-astronaut.github.io/midnight-video/`

## How to play

1. Watch your character walk up to the store in the rain (press **A** to skip).
2. Walk the aisles. Face a shelf and press **A** to grab a random tape from that genre. Labels are worn off, so you don't know what you've got.
3. Carry up to **5 tapes**. The HUD at the bottom shows your bag.
4. Walk to the counter at the top of the store and press **A**. The clerk reveals every tape, then slides **one random tape** back to you. House rules.
5. Keep that one, or gamble on the **Choice of the Day**: a random film from any shelf, any rating. It re-rolls every time you reach the counter.
6. Your pick shows up as a tape card with the year, runtime, director, IMDb score and links to IMDb and JustWatch.

Press **B** to check your bag. Talk to the cat if you want. The door at the bottom takes you back outside.

### Controls

| Action | Keyboard | On-screen |
|---|---|---|
| Move | Arrow keys or WASD | D-pad |
| Action / confirm | Z, Enter or Space | A |
| Cancel / bag | X, Esc or Backspace | B |
| Sound on/off | M | |

Works with touch on phones; the D-pad and buttons are under the screen.

## The shelves

| Sign | Shelf | Pulls from |
|---|---|---|
| SLASH | Slasher | slasher |
| SPIRIT | Supernatural | supernatural, possession |
| HAUNT | Haunted House | haunted |
| OCCULT | Folk & Occult | folk, witch |
| BODY | Body Horror | body |
| BEAST | Creatures | creature |
| UNDEAD | Zombies | zombie |
| FANGS | Vampires | vampire |
| PSYCH | Psychological | psych |
| COSMIC | Sci-Fi & Cosmic | scifi, cosmic |
| TAPES | Found Footage | found |
| LAUGHS | Horror Comedy | comedy |

A film can sit on more than one shelf if it has more than one tag. Home-invasion and survival films that have no other tag only turn up as the Choice of the Day.

## The movie list

The list is built into the page: 458 horror films from *Nosferatu* (1922) to 2025. It isn't pulled from IMDb live. IMDb has no free public API, and a static page can't call most third-party APIs without exposing a key.

Ratings are approximate IMDb scores and drift over time. Use the IMDb link on each pick to see the current number.

## Run it

It's one static file: HTML, CSS and vanilla JavaScript drawing to a 320x240 canvas. No build step, no dependencies.

- **Locally:** open `index.html` in a browser.
- **GitHub Pages:** go to **Settings > Pages**, set **Source** to "Deploy from a branch", choose your main branch and the `/ (root)` folder, and save. The file must be named `index.html` and sit at the top level of the repo.

The pixel font (Press Start 2P) loads from Google Fonts. Without a connection it falls back to the system monospace font and still plays.

## Add or edit movies

All the films live in one block in the script in `index.html`, in a constant called `RAW`. Each film is one line with seven fields separated by pipes:

```
Title|Year|Rating|Runtime|tags|Director|Logline
```

For example:

```
The Thing|1982|8.2|109|scifi,creature,body|John Carpenter|An Antarctic research crew learns the thing that thawed out can look like any of them.
```

Rules:

- Runtime is in minutes. Rating is a number like `7.4`.
- Tags are comma-separated with no spaces. Use only these keys: `slasher`, `supernatural`, `possession`, `haunted`, `folk`, `witch`, `body`, `creature`, `zombie`, `vampire`, `psych`, `scifi`, `cosmic`, `found`, `invasion`, `survival`, `comedy`.
- Don't use a `|` or a backtick inside a field.
- Skip any title and year that's already in the list, so a film doesn't show up twice.

To add a shelf, add an entry to the `SHELVES` array (a letter, a name, a short sign code, the tags it pulls from, and two colors) and place that letter as a 3-wide block in the `MAP` grid.

## Credits

Everything is drawn in code: the sprites, the shelves, the rain, the sign. Sound effects are generated in the browser with the Web Audio API, so there are no audio files. Film details are not affiliated with or sourced live from IMDb or JustWatch, which are linked for convenience only.

The old filter-and-roll version of this site lives on as [Daytime Video](https://empty-astronaut.github.io/daytime-video/) for everything that isn't horror.
