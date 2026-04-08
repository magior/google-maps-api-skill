# Security and Deployment Notes

## Local Codex usage

For the main Codex skill use case, the simplest model is local CLI usage:

- store `GOOGLE_MAPS_API_KEY` locally in `.env` or the environment
- run `python3 scripts/gmaps.py ...`
- keep generated HTML zero-key whenever possible

This is the intended default for this repository.

## Why key exposure matters

Any API key embedded in client-side HTML or JavaScript can be viewed by the user in browser developer tools. That may be acceptable for personal local use, but it is not acceptable for multi-user hosted products.

## Deployment modes

### Personal / local CLI

- The user owns the key and the billing.
- Risk is low because the key stays on the user's machine.
- Prefer zero-key embeds for shareable HTML exports.

### Users bring their own key

- Each user supplies their own Google Maps key.
- Keys should be stored securely and used server-side for data APIs.
- Do not embed a user's key in exported HTML pages.

### Platform-owned key

If you later build a hosted product, do not expose the main data key to the browser.

Recommended architecture:

- backend key for data APIs, restricted by server IP
- frontend key only for Maps JavaScript rendering, restricted by HTTP referrer
- server-side prefetch for geocoding, routes, places, weather, and similar APIs

## Shareable export mode

If the user wants an HTML file they can email or post elsewhere:

- prefer Google Maps embed iframes
- use direct Google Maps Street View links
- avoid client-side JavaScript that depends on a secret API key

This makes the export portable and avoids accidental key leakage.

## Practical guidance

- Do not embed `GOOGLE_MAPS_API_KEY` in generated HTML by default.
- Only use the Maps JavaScript API when the user explicitly asks for advanced features and understands the tradeoff.
- For route lines and other advanced views in a hosted app, fetch the data server-side and render the visualization from precomputed results.
