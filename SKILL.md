---
name: google-maps-api
description: Use when the user needs live Google Maps Platform data or map-oriented outputs via the bundled CLI, including geocoding, routes, places, weather, air quality, pollen, solar, elevation, timezone, address validation, roads, Street View, static maps, geolocation, aerial view, route optimization, or embed URL generation. Do not use it for generic web research when Google Maps API data is not necessary.
---

# Google Maps Platform

Use the bundled CLI in [scripts/gmaps.py](scripts/gmaps.py) as the primary interface for Google Maps Platform requests. The script is stdlib-only and returns structured JSON for most commands.

## Core rules

1. Report blockers immediately. If any API call fails with `403`, `REQUEST_DENIED`, "API not enabled", missing key, or another clear service error, stop and explain the issue plainly. Do not silently fall back to web search.
2. Ask before generating HTML. If the result could reasonably be delivered as text, JSON, or a page, confirm the preferred output format first.
3. Prefer the bundled CLI over ad hoc API calls. Use `python3 scripts/gmaps.py ...` unless the user explicitly wants code changes or a different integration.
4. Prefer zero-key shareable pages. For HTML outputs, default to Google Maps embed iframes and direct Google Maps Street View links instead of exposing API keys in client-side code.

## Workflow

1. Identify the narrowest matching command for the user request.
2. Run the CLI with repo-relative paths, usually `python3 scripts/gmaps.py <command> ...`.
3. Summarize the JSON output clearly instead of dumping raw results unless the user asks for raw JSON.
4. If the user wants a browser-friendly deliverable, ask whether they want an HTML page before generating one.
5. If Google Cloud setup appears incomplete, explain what is missing and point the user to the setup guidance. If browser automation is available and the user wants help, offer a guided enablement walkthrough.

## Common mappings

- "Where is this place?" -> `geocode`
- "What address is at these coordinates?" -> `reverse-geocode`
- "How do I get from A to B?" -> `directions`
- "How far is A from B?" -> `distance-matrix`
- "Find restaurants, hotels, pharmacies, EV chargers..." -> `places-search` or `places-nearby`
- "What are the hours, rating, or phone number?" -> `place-details`
- "What is the weather / air quality / pollen?" -> `weather`, `air-quality`, `pollen`
- "Can I install solar panels here?" -> `solar`
- "What is the elevation / timezone?" -> `elevation`, `timezone`
- "Is this address valid?" -> `validate-address`
- "Snap this GPS trace to roads" -> `snap-roads` or `nearest-roads`
- "Give me a map or embeddable map URL" -> `static-map` or `embed-url`

## Quick examples

```bash
python3 scripts/gmaps.py geocode "1600 Amphitheatre Parkway, Mountain View, CA"
python3 scripts/gmaps.py directions "New York, NY" "Boston, MA" --mode transit
python3 scripts/gmaps.py places-search "best ramen in Tokyo"
python3 scripts/gmaps.py weather 40.7128 -74.0060
python3 scripts/gmaps.py air-quality 40.7128 -74.0060 --health --pollutants
python3 scripts/gmaps.py embed-url --mode place --query "Eiffel Tower"
```

## Setup and references

- For API key setup, Google Cloud enablement, and troubleshooting, read [references/setup.md](references/setup.md).
- For the full command catalog and examples, read [references/api-reference.md](references/api-reference.md).
- For HTML output rules, shareable map pages, and Street View handling, read [references/html-output.md](references/html-output.md).
- For API key handling and deployment security notes, read [references/security.md](references/security.md).

## Notes

- Most commands print JSON.
- Image-producing commands save files locally.
- The script searches for `GOOGLE_MAPS_API_KEY` in the environment, the current directory `.env`, the home directory `.env`, and repo-local `.env` files.
- Keep the skill focused on Google Maps Platform data retrieval and map-oriented outputs rather than general travel planning or web research.
