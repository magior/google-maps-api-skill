# HTML Output Guidance

Always confirm before generating HTML. If the user might prefer text, JSON, or a page, ask first.

## Default approach

Default to zero-key shareable pages:

- Use Google Maps embed iframes for maps.
- Use direct Google Maps links for Street View.
- Avoid exposing `GOOGLE_MAPS_API_KEY` in client-side HTML whenever possible.

Only use the Maps JavaScript API when the user explicitly asks for advanced client-side interaction such as custom markers, decoded polylines, clustering, or other behaviors that embeds cannot support.

## Embed patterns

### Place map

```html
<iframe
  src="https://maps.google.com/maps?q=Oahu+Hawaii&z=10&output=embed"
  width="100%"
  height="400"
  style="border:0"
  allowfullscreen
></iframe>
```

### Directions map

```html
<iframe
  src="https://maps.google.com/maps?saddr=Los+Angeles+CA&daddr=San+Jose+CA&output=embed"
  width="100%"
  height="400"
  style="border:0"
  allowfullscreen
></iframe>
```

Parameters:

- `q`: place name or address
- `saddr` and `daddr`: origin and destination
- `z`: zoom level
- `output=embed`: required
- `ll`: optional center coordinates

Do not use `loading="lazy"` on Google Maps embed iframes. Off-screen maps may remain blank.

## Street View rule

Never embed Street View with the JavaScript API or the Embed API in generated HTML. Use a direct Google Maps link instead:

```text
https://www.google.com/maps/@?api=1&map_action=pano&viewpoint={lat},{lng}&heading={heading}&pitch={pitch}&fov=90
```

Required fields:

- `map_action=pano`
- `viewpoint={lat},{lng}`

Useful optional fields:

- `heading`
- `pitch`
- `fov`

Avoid the old shorthand `@lat,lng,3a,...` format because it is unreliable.

## Page design guidance

When producing a consolidated page:

- Prefer a single self-contained `.html` file with inline CSS and JavaScript.
- Combine maps, place cards, forecasts, and summary sections into one dashboard when the user asked for a multi-part answer.
- Keep the layout responsive across desktop and mobile.
- Favor cards, badges, section anchors, and concise summaries over raw JSON dumps.

Default visual direction: "Warm Stone Sunrise"

- Background: warm off-white
- Surfaces: white and light stone
- Text: dark stone tones
- Accent: indigo
- Headings: editorial serif feel
- Body: clean sans-serif

Use this theme unless the user asks for a different visual style.

## Save/open behavior

- Save generated pages with descriptive names in the current working directory.
- Open the page automatically in the browser only when the environment and permissions allow it.
- If the environment is headless or opening a browser would require approval, create the file and tell the user where it is.
