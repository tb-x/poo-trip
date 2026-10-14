# Poo's Big Trip

A pixel-art scrolling game for phones and tablets, made for kids around five.

A cute little poo sits in the toilet and wants to go on holiday. Pick a postcard, the toilet flushes, and the poo rides down through the pipes. At the end of the pipes it pops out at the holiday spot, lands, and puts on its holiday hat.

- There are **8 trips**, one per postcard, played in order: **Beach**, **Mountains**, **City**, **Jungle**, **Desert**, **Farm**, **Snow** and **Treasure Island**. Finishing a trip opens the next one; the others show a padlock. Finished trips get a green tick and show the most ducks caught there. Each trip is a bit longer and harder than the one before.
- The pipes scroll up as the poo travels down. They branch and join again across five lanes. At every T-junction, tap **left** or **right**: the big arrow buttons, either half of the screen, or the arrow keys. At the edges the pipe bends back on its own.
- **Rubber ducks** float in some pipes. Catch as many as you can: picking the pipe with more ducks is the puzzle. The 🦆 counter at the top keeps score, and the end card says how many you got out of the most you could have got on that trip, with a 👑 if you got them all. Some ducks sit just before a no-entry sign, so you have to decide whether a duck is worth the bonk.
- A red **no entry** sign means a dead end. If the poo goes in anyway, it bonks, sees stars, and goes back the other way.
- From the City on, some dead ends are **red pump pipes** with arrows pointing up. A pump blows the poo back up to the junction before, so you have to choose again. Avoid the red pipes!
- From the Jungle on, some pipes have a striped **gate** that slides open and shut, with a red or green lamp. The poo waits in front of a shut gate until it opens.
- On the **Farm** and on **Treasure Island** the poo is in a hurry: if you don't choose within about a second and a half, it picks a way itself.
- The **Snow** and **Treasure Island** trips are dark: only the poo's lamp lights the pipes. Ducks glow, signs show faintly, and the lamps on gates and pumps still blink, so you can still plan a way.
- On the other trips there's no timer: the poo waits at a junction and looks around until you choose.
- A **water splash** marks a pipe that makes the poo whoosh along faster for a moment. A **toilet paper roll** clogs the pipe and the poo has to push it slowly until it pops.
- The underground looks deep: caves in the dirt show rock further back, with pillars, glow-worms, old sewer pipes, waterfalls and glowing crystals, and those layers scroll slower than the pipes. Dark rocks and drips slide past the screen edges faster, as if they were close to you.
- On the way down you pass four layers of soil. The top one is full of old copper and steel pipes. Deeper down there are water pockets, dinosaur bones and crystal caves. Look out for rare finds: a mole, a lost toy car, an old boot, a clay pot, a dinosaur skull, a treasure chest, glowing mushrooms.
- At the holiday spot the poo puts on a hat: sunglasses at the beach, a woolly hat in the mountains, a beret in the city, an explorer hat in the jungle, a pharaoh's headdress in the desert, a straw hat on the farm, earmuffs in the snow and a pirate hat on the island.
- The end card has 🗺️ (back to the postcards), **🚽 Again** (the same trip with new pipes) and **Next** (the next trip). 🏠 in the corner goes back to the list of all games; 🗺️ during a trip goes back to the postcards.

Nothing ever goes badly: a wrong turn only costs a few seconds, and every trip ends at the holiday spot.

The poo, the props and the underground finds are small pixel-art pictures made with [PixelLab](https://pixellab.ai) and kept in `assets/`. Everything else is drawn by the game's own code: the pipes, the toilet, the soil and caves, the ducks, gates and pumps, the holiday scenes (including the pyramids, barn, cow, igloo, penguin and pirate ship), the poo's faces and its hats. Sounds are made in the browser too, and a voice says a tip at the start of the trips that bring something new ("Red pipes blow you back up!"), "Which way?" at the first junction and "Welcome to the beach!" on arrival. On an iPhone, the silent switch mutes them.

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

These are at the top of the script in `index.html`. Each trip is one line of the `LEVELS` list:

| Setting | Beach → Island | What it does |
| --- | --- | --- |
| `rows` | 8 → 14 | Rows of junctions on the way (keep it even) |
| `dead` | 0.35 → 0.6 | Chance that one way out of a junction is closed |
| `pump` | 0 → 0.55 | Share of the closed ways that are red pump pipes instead of no-entry signs |
| `ducks` | 0.5 → 0.4 | Chance of one or two ducks on an open pipe |
| `gate` | 0 → 0.35 | Chance of a gate on an open pipe |
| `water` / `tp` | about 0.2 / 0.14 | Chance of a water rush / a toilet paper clog on an open pipe |
| `speed` | 1 → 1.2 | Riding speed, times `BASE_SPEED` |
| `hurry` | Farm, Island | The poo picks a way itself if you take too long |
| `dark` | Snow, Island | Only the poo's lamp lights the pipes |
| `tip` | | What the voice says when the trip starts |

And these apply to every trip:

| Constant | Default | What it does |
| --- | --- | --- |
| `MAX_BRANCHES` | 3 | Most pipes running side by side |
| `BASE_SPEED` | 93 | Normal riding speed, in game pixels per second |
| `BOOST_SPEED` / `BOOST_TIME` | 225 / 2.4 s | Speed and length of a water rush |
| `CLOG_SPEED` / `CLOG_TIME` | 24 / 1.6 s | Speed and length of pushing a toilet paper clog |
| `BONK_TIME` | 1.1 s | How long the poo sees stars after a dead end |
| `STUB_DUCK_CHANCE` | 0.4 | Chance of a duck waiting just before a no-entry sign |
| `GATE_OPEN` / `GATE_SHUT` | 2.4 / 1.8 s | How long a gate stays open, then shut |
| `WHOOSH_SPEED` | 270 | Speed when a pump blows the poo back up |
| `HURRY_WAIT` | 1.6 s | On hurry trips, how long the poo waits before it picks a way |
| `LAMP_R` | 84 | On dark trips, how far the poo's lamp shines, in game pixels |
| `FAR_F` / `MID_F` / `FORE_F` | 0.25 / 0.55 / 1.45 | How fast the far rock, the middle rock and the front edges scroll, compared with the pipes |

After changing a picture in `assets/`, bump `ASSET_V` so browsers load the new one.

The sound setting, the finished trips and the most ducks caught on each are remembered in the browser (`localStorage`, keys starting with `pootrip.`).
