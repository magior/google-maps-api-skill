# Google Maps Platform API Skill for Codex

This repository packages a Codex-first skill around a single stdlib-only CLI for **20+ Google Maps Platform APIs**.

Fork note: this project is a fork of [tivojn/google-maps-api-skill](https://github.com/tivojn/google-maps-api-skill).

## What it does

The bundled CLI in [scripts/gmaps.py](scripts/gmaps.py) covers:

- Geocoding and reverse geocoding
- Routes and distance matrices
- Places search, nearby search, details, autocomplete, and photos
- Weather, air quality, pollen, and solar
- Elevation and time zone lookups
- Address validation and roads APIs
- Street View, static maps, geolocation, aerial view, and route optimization
- Embeddable map URL generation

## Codex skill layout

This repository is already structured as a skill root:

```text
google-maps-api/
├── SKILL.md
├── agents/
│   └── openai.yaml
├── references/
│   ├── api-reference.md
│   ├── html-output.md
│   ├── security.md
│   └── setup.md
├── scripts/
│   └── gmaps.py
├── examples/
│   └── trip-plan-example.html
└── ...
```

## How to use it with Codex

According to the Codex skills docs, repository-scoped skills live under `.agents/skills`, and user-wide skills live under `$HOME/.agents/skills`.

To use this skill in Codex, place or symlink this directory at one of these paths:

- `.agents/skills/google-maps-api`
- `$HOME/.agents/skills/google-maps-api`

Codex detects skills from the containing folder and reads [SKILL.md](SKILL.md) plus optional metadata from [agents/openai.yaml](agents/openai.yaml).

## Setup

Add your Google Maps API key:

```bash
echo 'GOOGLE_MAPS_API_KEY=your_key_here' >> .env
```

or:

```bash
echo 'GOOGLE_MAPS_API_KEY=your_key_here' >> ~/.env
```

Get a key from the [Google Cloud Console](https://console.cloud.google.com/apis/credentials), then enable the APIs you need in the [API Library](https://console.cloud.google.com/apis/library).

More setup and troubleshooting guidance is in [references/setup.md](references/setup.md).

## CLI usage examples

```bash
python3 scripts/gmaps.py geocode "1600 Amphitheatre Parkway, Mountain View, CA"
python3 scripts/gmaps.py directions "New York, NY" "Boston, MA" --mode transit
python3 scripts/gmaps.py places-search "best ramen in Tokyo"
python3 scripts/gmaps.py weather 40.7128 -74.0060
python3 scripts/gmaps.py air-quality 40.7128 -74.0060 --health --pollutants
python3 scripts/gmaps.py solar 37.4219 -122.0841
python3 scripts/gmaps.py validate-address "1600 Amphitheatre Pkwy, Mountain View, CA 94043"
python3 scripts/gmaps.py embed-url --mode place --query "Eiffel Tower"
```

Run `python3 scripts/gmaps.py --help` to see the full command surface.

## HTML output

The skill can support browser-friendly outputs such as maps, route pages, and dashboards, but it should ask before generating HTML. For shareable outputs, prefer zero-key embeds and direct Google Maps links.

See:

- [references/html-output.md](references/html-output.md)
- [examples/trip-plan-example.html](examples/trip-plan-example.html)

## Security model

This repository is primarily designed for local Codex use with a user-owned Google Maps API key. For hosted or multi-user deployments, treat key exposure as a security concern and move data API access server-side.

See [references/security.md](references/security.md) for the detailed notes.

## Why this repo stays lightweight

- No third-party Python dependencies
- A single CLI entrypoint for all supported APIs
- Skill instructions kept concise, with long-form material moved to `references/`

## License

MIT
