# Feature Specifications

## Product scene

`index.html` constructs speaker, headphones, and watch groups using primitive geometry and Three.js materials. Hidden product groups remain in the scene graph but are not visible.

## Controls

OrbitControls uses damping factor `0.06`, minimum distance `4.2`, maximum distance `12`, and polar limits `0.25` to `Math.PI * 0.49`.

## Color state

The palette is Sand `#c5a982`, Slate `#647f9e`, and Rose `#a56768`. Only the active product's `colorMaterials` array is updated.

## CTA

The current CTA opens `mailto:hello@forma.example` with a product-name subject. Variant inclusion is planned.
