# Spinning Pattern Cube

An animated, Rubik's-style cube drawn in a single HTML file, with no libraries or build step.

The cube is viewed from its top corner, so its outline is a hexagon with three faces visible. Each face has a 3×3 grid of tiles, and each tile is a 7×7 grid of small shapes:

- solid circle
- solid square (rounded corners)
- solid triangle (rounded corners)
- circle with a small round hole
- square with a small round hole

Every tile uses one shape type and a color gradient that radiates from its center, blending between two of six colors (red, orange, yellow, green, blue, purple). All shapes always face the viewer, even while layers are turning.

## The animation

The cube runs a 6-step sequence on a loop, pausing 2.5 seconds between steps:

1. **One layer** turns 90°.
2. **Two parallel layers** turn, never including the layer from step 1. If the two layers touch, they spin in opposite directions.
3. **All three layers** of one side turn **in a wave**: left to right, right to left, top to bottom or bottom to top.
4. Same as step 1.
5. Same as step 2.
6. **Hexagon rings:** the inner, middle and outer rings around the center corner slide along hexagonal tracks. The inner and outer rings go counterclockwise and the middle ring goes clockwise, each a third of the way around.

Steps 1 to 5 pick their layers and directions at random each time the page loads. Every turn is a legal Rubik's move, so the cube always ends up viewed from its top corner. During a layer turn, anything behind the turning layer is hidden, and the gaps that open up show a grid of small gray dots.

## How to view it

### On your computer

1. Download or clone this repository.
2. Double-click `spin-box.html` to open it in a web browser (Chrome, Edge, Firefox or Safari).

That's it; there's nothing to install.

### Online with GitHub Pages

1. In this repository on GitHub, go to **Settings → Pages**.
2. Under **Build and deployment**, set the source to **Deploy from a branch**, choose `main` and `/ (root)`, then click **Save**.
3. After a minute or two, the cube will be live at:
   `https://ashwins14.github.io/spinning-cube-proj/spin-box.html`

(GitHub Pages only serves a page at the bare site address if it's named `index.html`, so include `spin-box.html` at the end of the link.)

## Viewing options

You can add these to the end of the page's address:

| Option | What it does |
| --- | --- |
| `?still` | Shows the cube at rest with no animation |
| `?t=6700` | Freezes the animation at that many milliseconds |
| `?seed=42` | Replays the same sequence of random turns every time |

For example: `spin-box.html?t=6700` shows the wave in step 3 mid-turn.

## How it's built

- **One file:** `spin-box.html` contains all the HTML, CSS and JavaScript.
- **Canvas drawing:** the cube is drawn on an HTML `<canvas>`. Each frame, every shape's 3D position is projected to the screen and drawn as a flat shape, back to front.
- **Cube model:** the cube is stored as 27 cubies with stickers. Each finished turn snaps the stickers into their new positions, so the cube never drifts out of alignment.
- **Settings:** the timing, sizes and colors are constants at the top of the script (for example `PHASE_PAUSE`, `TURN_MS` and `WAVE_STAGGER`).
