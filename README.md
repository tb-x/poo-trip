# Poo's Big Trip

A pixel-art scrolling game for phones and tablets, made for kids around five.

A cute little poo sits in the toilet and wants to go on holiday. Pick a postcard, the toilet flushes, and the poo rides down through the pipes. At the end of the pipes it pops out at the holiday spot, lands, and puts on its holiday hat.

- Pick where to go: **Beach**, **Mountains**, **City**, **Jungle**, or **Surprise!** Places you've visited get a green tick.
- The pipes scroll up as the poo travels down. They branch and join again across five lanes. At every T-junction, tap **left** or **right**: the big arrow buttons, either half of the screen, or the arrow keys. At the edges the pipe bends back on its own.
- If you don't choose, the poo waits at the junction and looks around until you do. There's no timer.
- A red **no entry** sign means a dead end. If the poo goes in anyway, it bonks, sees stars, and goes back the other way.
- A **water splash** marks a pipe that makes the poo whoosh along faster for a moment.
- A **toilet paper roll** clogs the pipe and the poo has to push it slowly until it pops.
- On the way down you pass four layers of soil. The top one is full of old copper and steel pipes. Deeper down there are water pockets, dinosaur bones and crystal caves. Look out for rare finds: a mole, a lost toy car, an old boot, a clay pot, a dinosaur skull, a treasure chest, glowing mushrooms.
- After 12 rows of junctions the poo reaches the holiday spot: sunglasses at the beach, a woolly hat in the mountains, a beret in the city, an explorer hat in the jungle.
- 🏠 in the corner goes back to the list of all games; 🗺️ during a trip goes back to the postcards.

Nothing ever goes badly: a wrong turn only costs a couple of seconds.

The poo, the props and the underground finds are small pixel-art pictures made with [PixelLab](https://pixellab.ai) and kept in `assets/`. Everything else is drawn by the game's own code: the pipes, the toilet, the soil, the holiday scenes, the poo's faces and its hats. Sounds are made in the browser too, and a voice says "Which way?" at the first junction and "Welcome to the beach!" on arrival. On an iPhone, the silent switch mutes them.

## Play offline (add to Home Screen)

On iPhone or iPad, open the game in Safari, tap **Share → Add to Home Screen**, then open it once from the new icon while online. After that it starts full screen and works without internet. Changes arrive on their own: the next online launch downloads them and the one after shows them.

(How: `manifest.webmanifest` gives the icon and full-screen mode; `sw.js`, a service worker, keeps a copy of every file the game uses, including the font and the pictures. The icons `icon-180.png` and `icon-512.png` are rendered from `icon.svg` in headless Chrome.)

## Running locally

It is an `index.html` plus the pictures in `assets/`, with no build step. Serve the folder over HTTP, for example:

```bash
python -m http.server 5205
```

Then open http://localhost:5205. Opening `index.html` straight from disk works too.

## Tuning knobs

These are at the top of the script in `index.html`:

| Constant | Default | What it does |
| --- | --- | --- |
| `TRIP_ROWS` | 12 | Rows of junctions on the way to each holiday spot (keep it even) |
| `DEAD_END_CHANCE` | 0.5 | Chance that one way out of a junction ends at a no-entry sign |
| `MAX_BRANCHES` | 3 | Most pipes running side by side |
| `BASE_SPEED` | 93 | Normal riding speed, in game pixels per second |
| `BOOST_SPEED` / `BOOST_TIME` | 225 / 2.4 s | Speed and length of a water rush |
| `CLOG_SPEED` / `CLOG_TIME` | 24 / 1.6 s | Speed and length of pushing a toilet paper clog |
| `BONK_TIME` | 1.1 s | How long the poo sees stars after a dead end |
| `WATER_CHANCE` | 0.22 | Chance of a water rush on a pipe between two rows |
| `TP_CHANCE` | 0.16 | Chance of a clog on a pipe between two rows |

After changing a picture in `assets/`, bump `ASSET_V` so browsers load the new one.

The sound setting and the visited places are remembered in the browser (`localStorage`, keys starting with `pootrip.`).
