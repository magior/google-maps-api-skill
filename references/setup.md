# Setup and Troubleshooting

## API key

Set `GOOGLE_MAPS_API_KEY` in one of these places:

```bash
echo 'GOOGLE_MAPS_API_KEY=your_key_here' >> .env
```

or:

```bash
echo 'GOOGLE_MAPS_API_KEY=your_key_here' >> ~/.env
```

or:

```bash
export GOOGLE_MAPS_API_KEY=your_key_here
```

The bundled CLI searches for the key in this order:

1. Environment variable
2. `.env` in the current working directory
3. `.env` in the home directory
4. Repo-local `.env` files near the script

Get a key from the Google Cloud Console:

- Credentials: [Google Cloud Console](https://console.cloud.google.com/apis/credentials)
- API Library: [Google Cloud API Library](https://console.cloud.google.com/apis/library)

## Common APIs to enable

Enable the APIs you actually use:

- Geocoding API
- Routes API
- Places API (New)
- Elevation API
- Time Zone API
- Air Quality API
- Pollen API
- Solar API
- Weather API
- Address Validation API
- Roads API
- Street View Static API
- Maps Static API
- Geolocation API
- Aerial View API
- Route Optimization API
- Places Insights API

## Error handling

When a command fails, surface the problem clearly instead of working around it silently.

Typical cases:

- `403` / `REQUEST_DENIED` / "API not enabled": the API or billing setup is incomplete
- Missing key: `GOOGLE_MAPS_API_KEY` is not configured
- `400` / `INVALID_REQUEST`: a required parameter is missing or malformed
- `429`: the project is rate-limited
- `ZERO_RESULTS`: the request was valid but returned no matches

## Guided API enablement

If an API appears to be disabled:

1. Tell the user which API looks unavailable.
2. Offer to guide them through enabling it in Google Cloud Console.
3. If browser automation is available in the environment and the user wants help, navigate directly to the API library page and enable it.
4. After enablement, retry the original command.

Useful Google Cloud API library paths:

- Geocoding: `geocoding-backend.googleapis.com`
- Routes: `routes-backend.googleapis.com`
- Places (New): `places-backend.googleapis.com`
- Elevation: `elevation-backend.googleapis.com`
- Time Zone: `timezone-backend.googleapis.com`
- Air Quality: `airquality.googleapis.com`
- Pollen: `pollen.googleapis.com`
- Solar: `solar.googleapis.com`
- Weather: `weather.googleapis.com`
- Address Validation: `addressvalidation.googleapis.com`
- Roads: `roads.googleapis.com`
- Street View Static: `street-view-image-backend.googleapis.com`
- Maps Static: `static-maps-backend.googleapis.com`
- Maps JavaScript: `maps-backend.googleapis.com`
- Maps Embed: `maps-embed-backend.googleapis.com`
- Geolocation: `geolocation.googleapis.com`
- Aerial View: `aerialview.googleapis.com`
- Route Optimization: `routeoptimization.googleapis.com`

Full URL pattern:

```text
https://console.cloud.google.com/apis/library/<api-path>
```

## Notes

- Weather and some environment APIs may require billing on the Google Cloud project.
- Aerial View is limited to supported US addresses.
- Route Optimization requires a GCP project ID in addition to the API key.
