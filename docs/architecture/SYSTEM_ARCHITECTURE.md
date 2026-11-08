# System Architecture

## Runtime model

```mermaid
flowchart LR
  Browser --> HTML[DOM overlay]
  Browser --> WebGL[Three.js WebGLRenderer]
  CDN[jsDelivr CDN] --> Modules[Three.js + OrbitControls]
  UI[Tabs and swatches] --> State[Local JS state]
  State --> Scene[Scene graph]
  Scene --> WebGL
```

The application is a browser-only single page. HTML/CSS provides the overlay; JavaScript owns local state and the Three.js scene; WebGL renders the scene continuously.

## Layers

- Presentation: semantic HTML and inline CSS.
- Interaction/state: `activeProduct`, `activeColor`, idle timer, DOM event listeners.
- Scene: lights, floor, stage group, product groups, camera, controls.
- External runtime: Three.js and OrbitControls from jsDelivr.

## Important constraints

There is no server, persistent data, API, database, authentication, or authorization layer in the repository.
