# ADR-001: Zero-Build WebGL Prototype

## Status

Accepted for the current prototype.

## Decision

Keep the application as a browser-loaded `index.html` using an Import Map and CDN-hosted Three.js.

## Evidence

`index.html:99-104` contains the Import Map and module imports; no package manifest or bundler configuration exists.

## Trade-off

This keeps setup simple but sacrifices offline reliability, dependency reproducibility, and build-time optimization.
