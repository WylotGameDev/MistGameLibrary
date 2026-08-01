# Mist games repo starter

Drop this into your Mist games repo (the one you point Mist's Settings page
at). It gives you:

```
.
├── manifest.template.json      # blank manifest.json — copy this for each new game
└── Games/
    └── example-game/           # a fully working example entry
        ├── manifest.json
        ├── game/
        │   └── PUT_GAME_FILES_HERE.txt
        └── images/
            ├── header.jpg               460x215   (placeholder)
            ├── library_600x900_2x.jpg   600x900   (placeholder)
            ├── library_hero_2x.jpg     3840x1240  (placeholder)
            └── iconsmall.jpg             32x32    (placeholder)
```

## Adding a new game

1. Copy the whole `Games/example-game/` folder and rename it to whatever
   you want — the folder name is just an internal id, it's never shown to
   players. Use lowercase-with-dashes to keep URLs tidy, e.g. `Games/my-cool-game/`.
2. Open `manifest.json` inside it (or start from `manifest.template.json`)
   and fill in the fields below.
3. Replace the four placeholder images in `images/` with real art at the
   **exact same dimensions** — Mist doesn't resize them.
4. Delete `PUT_GAME_FILES_HERE.txt` and put the game's `.exe` and everything
   it needs inside `game/`, preserving whatever folder layout the game
   itself expects.
5. Commit and push. No launcher update needed — Mist reads the repo's Git
   tree live, so the game appears in the Store the next time it refreshes.

## manifest.json fields

Only these six fields are ever read — everything else (file size, platform,
image URLs, download path) is worked out automatically from the folder
contents, so don't add extra keys, they'll just be ignored.

| Field         | Type            | Required | Notes                                             |
|---------------|-----------------|----------|----------------------------------------------------|
| `name`        | string          | yes      | Display name shown in the Store/Library.           |
| `version`     | string          | yes      | Whatever versioning scheme you like, e.g. `1.2.0`.  |
| `author`      | string          | no       | Defaults to `"Unknown"` if omitted.                 |
| `description` | string          | no       | Shown on the game's store page.                     |
| `genres`      | array of string | no       | e.g. `["Strategy", "Puzzle"]`. Used for filtering.  |
| `tags`        | array of string | no       | e.g. `["Singleplayer", "Indie", "2D"]`.              |

## Image requirements

All four are required for a game to look right in the UI — if one is
missing, that piece of art just won't render for that game.

| File                          | Size (px)   | Used as                        |
|-------------------------------|-------------|---------------------------------|
| `header.jpg`                  | 460 x 215   | Store/card banner               |
| `library_600x900_2x.jpg`      | 600 x 900   | Vertical library cover          |
| `library_hero_2x.jpg`         | 3840 x 1240 | Big hero art on the detail page |
| `iconsmall.jpg`                | 32 x 32     | Small icon                      |

The images in `Games/example-game/images/` are plain generated placeholders
labeled with their required dimensions — swap them out for real art, keeping
the same filenames and pixel sizes.

## The `game/` folder

Everything under `Games/<id>/game/` is downloaded byte-for-byte, keeping its
exact folder structure, into the player's install directory. There's no zip
step and no manual download URL to maintain — whatever you commit there is
exactly what the player gets. If the folder contains a `.exe` anywhere,
Mist marks the game as Windows-compatible automatically.
