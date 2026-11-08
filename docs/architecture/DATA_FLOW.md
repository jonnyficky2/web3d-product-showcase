# Data Flow

1. Browser loads `index.html`.
2. Import Map resolves Three.js modules through jsDelivr.
3. JavaScript creates scene, products, lights, camera, and controls.
4. User events update local product/color state and DOM attributes/text.
5. The animation loop updates controls, idle rotation, and renders the scene.
6. The CTA constructs a mailto URL in the browser.

No data is persisted or sent to a project-owned backend.
