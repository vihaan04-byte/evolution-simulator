# Evolution Simulator 

A real-time evolution simulator built with vanilla HTML/CSS/JS. Creatures hunt food, drain energy, reproduce, mutate, and die, and over time you can actually watch natural selection happen on screen.

Live at: **https://vihaan04-byte.github.io/evolution-simulator/**

---

## How I built it

I split the work across three AIs — Claude, ChatGPT, and Gemini — each responsible for one module. The idea was to stay under free-tier token limits while keeping the code modular.

- **Claude** → `core.js` — simulation logic, genetics, mutation, energy system
- **ChatGPT** → `renderer.js` — canvas drawing, animation loop
- **Gemini** → `ui.js` — control panels, sliders, stats

I wrote a shared spec first (data structures, function signatures, naming conventions) so all three modules could talk to each other without stepping on each other's code. Then I assembled and debugged the final file myself.


---

## How the simulation works

Each creature has four genes:

| Gene | Range | Effect |
|------|-------|--------|
| Speed | 1–5 | How fast it moves. High speed = high energy cost (quadratic). |
| Size | 1–5 | How big it is. Bigger = larger eating radius, but costs more energy. |
| Sense | 10–100 | Detection radius for food. Can't chase what you can't see. |
| Hue | 0–360 | Just colour. Shifts on mutation so you can visually track lineages. |

Every tick, creatures spend energy based on `0.05 + size²×0.015 + speed²×0.018`. The quadratic cost on speed and size is intentional — it creates real evolutionary pressure instead of just "faster is always better."

When a creature hits 100 energy, it reproduces, spawning a child with slightly mutated genes. When it hits 0 it dies. If the whole population goes extinct, it auto-restarts.

The gene history graph in the bottom right shows average speed, size, and sense over time. After a few minutes you can actually see which traits win in the current food environment.

---

## Controls

- **Mutation Rate** — how much genes shift each birth. Crank it up for chaotic divergence.
- **Food Spawn Rate** — more food = faster population, less selection pressure.
- **Max Population** — caps reproduction. Lower it to make survival harder.

---

## Stack

Just HTML, CSS, and vanilla JS. No libraries, no build tools, no frameworks. One file.
