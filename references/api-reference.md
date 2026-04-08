# API Reference

Use the bundled CLI:

```bash
python3 scripts/gmaps.py --help
```

The command surface stays stable and is grouped below by use case.

## Geocoding

```bash
python3 scripts/gmaps.py geocode "1600 Amphitheatre Parkway, Mountain View, CA"
python3 scripts/gmaps.py geocode "Tokyo Tower" --language ja --region jp
python3 scripts/gmaps.py reverse-geocode 37.4224 -122.0856
python3 scripts/gmaps.py reverse-geocode 48.8584 2.2945 --language fr
```

## Routes and Distance

```bash
python3 scripts/gmaps.py directions "New York, NY" "Boston, MA"
python3 scripts/gmaps.py directions "Seattle" "Portland" --alternatives --avoid-tolls
python3 scripts/gmaps.py directions "Home" "Work" --mode bicycling --units imperial
python3 scripts/gmaps.py directions "A" "D" --waypoints "B" "C"
python3 scripts/gmaps.py distance-matrix --origins "New York" "Boston" --destinations "Philadelphia" "Washington DC"
```

## Places

```bash
python3 scripts/gmaps.py places-search "best pizza in Chicago"
python3 scripts/gmaps.py places-search "pharmacy" --location "40.714,-74.006" --radius 1000
python3 scripts/gmaps.py places-search "EV charging" --type "electric_vehicle_charging_station"
python3 scripts/gmaps.py places-nearby 40.7128 -74.0060 --type restaurant --radius 800
python3 scripts/gmaps.py place-details ChIJN1t_tDeuEmsRUsoyG83frY4
python3 scripts/gmaps.py autocomplete "central p" --types "park"
python3 scripts/gmaps.py place-photo "places/PLACE_ID/photos/PHOTO_REF" --max-width 800
```

## Environment and Forecasting

```bash
python3 scripts/gmaps.py weather 40.7128 -74.0060
python3 scripts/gmaps.py weather 40.7128 -74.0060 --mode hourly --hours 48
python3 scripts/gmaps.py weather 40.7128 -74.0060 --mode daily --days 7

python3 scripts/gmaps.py air-quality 40.7128 -74.0060
python3 scripts/gmaps.py air-quality 40.7128 -74.0060 --health --pollutants
python3 scripts/gmaps.py air-quality-history 40.7128 -74.0060 --hours 48
python3 scripts/gmaps.py air-quality-forecast 40.7128 -74.0060

python3 scripts/gmaps.py pollen 34.0522 -118.2437 --days 5
python3 scripts/gmaps.py solar 37.4219 -122.0841
python3 scripts/gmaps.py solar 37.4219 -122.0841 --quality HIGH
python3 scripts/gmaps.py solar-layers 37.4219 -122.0841 --radius 100
```

## Elevation and Time

```bash
python3 scripts/gmaps.py elevation 39.7392 -104.9903
python3 scripts/gmaps.py elevation --locations "39.7392,-104.9903|36.4555,-116.8666"
python3 scripts/gmaps.py elevation --path "36.578,-118.292|36.606,-118.099" --samples 20
python3 scripts/gmaps.py timezone 40.7128 -74.0060
python3 scripts/gmaps.py timezone 35.6762 139.6503 --language ja
```

## Validation and Roads

```bash
python3 scripts/gmaps.py validate-address "1600 Amphitheatre Pkwy, Mountain View, CA 94043"
python3 scripts/gmaps.py validate-address "123 Main St" --region US --enable-usps

python3 scripts/gmaps.py snap-roads "60.170,-24.942|60.171,-24.941|60.172,-24.940"
python3 scripts/gmaps.py snap-roads "60.170,-24.942|60.172,-24.940" --interpolate
python3 scripts/gmaps.py nearest-roads "60.170,-24.942|60.171,-24.941"
```

## Maps and Street View

```bash
python3 scripts/gmaps.py streetview --location "Eiffel Tower, Paris" --size 800x600
python3 scripts/gmaps.py streetview --lat 46.414 --lng 10.013 --heading 90
python3 scripts/gmaps.py static-map --lat 40.714 --lng -74.006 --zoom 13
python3 scripts/gmaps.py static-map --center "Tokyo" --maptype satellite --zoom 12
python3 scripts/gmaps.py embed-url --mode place --query "Eiffel Tower"
python3 scripts/gmaps.py embed-url --mode directions --origin "NYC" --destination "Boston"
python3 scripts/gmaps.py embed-url --mode streetview --lat 46.414 --lng 10.013
```

## Geolocation and Aerial View

```bash
python3 scripts/gmaps.py geolocation
python3 scripts/gmaps.py geolocation --wifi "00:11:22:33:44:55,-65" "66:77:88:99:AA:BB,-72"

python3 scripts/gmaps.py aerial-view check --address "1600 Amphitheatre Pkwy, Mountain View"
python3 scripts/gmaps.py aerial-view render --address "1600 Amphitheatre Pkwy, Mountain View"
python3 scripts/gmaps.py aerial-view get --video-id VIDEO_ID
```

## Route Optimization and Area Insights

```bash
python3 scripts/gmaps.py route-optimize problem.json --project my-gcp-project
python3 scripts/gmaps.py places-aggregate --location "40.714,-74.006" --radius 5000 --type restaurant
python3 scripts/gmaps.py places-aggregate --location "34.052,-118.244" --type cafe --min-rating 4.0 --insight INSIGHT_PLACES
```

## Output expectations

- Most commands print JSON to stdout.
- `streetview` and `static-map` can download binary assets to files.
- `embed-url` only generates URLs and does not perform a live Google API request beyond reading the API key.
- For HTML pages and map embeds, follow the stricter rules in [html-output.md](html-output.md).
