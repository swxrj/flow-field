# Flow Field

A deterministic flow-field generator that paints in your browser. Every output is built from a layered velocity field and a palette, all derived from a single random seed.

![Preview](assets/preview.png)

## Live demo

[swxrj.github.io/flow-field](https://swxrj.github.io/flow-field/)

## How it works

There is no drawing, painting, or input beyond a seed. Every click rolls a new random number, and from that number the algorithm derives a colour palette, a layered flow field, a sequence of strokes, and a title. Strokes start thick and progressively thin out along the field's curves, tapering to 1px at their ends for a soft, fluid feel. Because the whole pipeline is deterministic, the same seed always produces the same painting, and there are roughly a million palette × flow × title combinations before you see anything close to a repeat.

## Controls

| Control | What it does |
|---|---|
| **Thickness** | Starting thickness of the heaviest stroke (1 = delicate webs, 10 = bold ribbons) |
| **Density** | How many strokes make up the piece |
| **Color** | 1 = monochrome, 10 = 4+ distinct hues including accents from other palettes |
| **Ratio** | 1:1 for profile pics, 9:16 for phone wallpapers, 16:9 for desktop |
| **↻ new artwork** | Re-seed and generate a fresh painting |
| **↓ save image** | Download the current artwork as a high-res PNG |

## Keyboard shortcuts

| Key | Action |
|---|---|
| `space` | New artwork |
| `s` | Save current artwork |
| `1` / `2` / `3` | 1:1 / 9:16 / 16:9 aspect ratio |

## Tech

- Single `index.html` file, no build step, no bundler
- Stroke generation runs in a Web Worker so the UI stays snappy
- [Motion](https://motion.dev) for UI springs, transitions, and the frame parallax tilt
- Canvas 2D rendered with tapered filled polygons so each stroke reads as a variable-width ribbon

## Running locally

Just open `index.html` in a browser. That is genuinely the whole thing.

If you want a local server (some browsers are stricter about module imports from `file://`):

```bash
python3 -m http.server 8080
# then visit http://localhost:8080
```

## Deploying to GitHub Pages

1. Push this folder to a GitHub repo called `flow-field`
2. Repo → **Settings** → **Pages**
3. Source: **Deploy from a branch**, branch `main`, folder `/ (root)`
4. Save. Site goes live at `https://<username>.github.io/flow-field/` in about a minute

Every subsequent `git push` to `main` auto-redeploys.

For perfect social-media preview cards, update the `og:*` and `twitter:*` URLs in `index.html`'s `<head>` to absolute URLs (e.g. `https://<username>.github.io/flow-field/assets/preview.png`).

## Project layout

```
.
├── index.html          # the whole app
├── assets/
│   └── preview.png     # the image shown above
├── README.md
└── .gitignore
```
