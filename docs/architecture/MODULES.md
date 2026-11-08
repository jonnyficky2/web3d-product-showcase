# Modules

The current source is a single file rather than separate JavaScript modules.

| Logical module | Source evidence | Responsibility |
|---|---|---|
| DOM presentation | `index.html:8-98` | Layout, controls, labels, responsive CSS |
| Renderer setup | `index.html:106-137` | Scene, camera, renderer, lights, floor |
| Product builders | `index.html:153-210` | Procedural speaker, headphones, watch |
| Product state | `index.html:212-258` | Selection, colors, UI synchronization |
| Interaction loop | `index.html:219-275` | OrbitControls, resize, animation, rendering |

No server, API, database, asset loader, shader module, or authentication module exists.
