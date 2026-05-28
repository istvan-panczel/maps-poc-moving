# maps-poc-moving

Map + moving-vehicle animation POCs for a promotion app where users watch
an "influencer" travel toward their city.

**Live demo:** https://istvan-panczel.github.io/maps-poc-moving

## POCs

| File | What it shows |
| --- | --- |
| [`index.html`](./index.html) | Leaflet + OpenStreetMap. No API key. Basic A→B animation with play/pause. |
| [`google.html`](./google.html) | Same animation on Google Maps. |
| [`time-snapshot.html`](./time-snapshot.html) | **Closest to production:** car position is derived from real clock time (`departureTime` → `arrivalTime`). Reload the page and the car is exactly where it should be based on `Date.now()`. |
| [`directions.html`](./directions.html) | Same time-based logic, but the route polyline is fetched from the Google **Directions API** so the path snaps to real roads. Requires Directions API enabled on the key (the public demo key only allows Maps JS API, so this page will show an error with the demo key). |
| [`clustering.html`](./clustering.html) | Marker clustering with `@googlemaps/markerclusterer`. ~300 markers around Hungarian cities. Toggle clustering on/off and change marker density to compare. |

## Notes for production

- Google Maps runs entirely client-side. The PHP backend just renders the
  HTML and (optionally) exposes a JSON endpoint with the trip data
  (`departureTime`, `arrivalTime`, waypoints).
- Cache Directions API results per route — the path between two fixed
  points doesn't change, no need to re-bill on every page view.
- The current key is Google's public demo key, which shows a "For
  development purposes only" watermark and can be rate-limited at any
  time. Replace it with a referrer-restricted key from your own Cloud
  project before going live.
