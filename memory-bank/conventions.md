# Coding standards

- Use `.editorconfig` files to document and allow for automatic editor configuration.
- Python: Follow PEP8, use the `yapf` formatter.
- Typescript: 2-space indentation.
- Geolocation: Request location via the JavaScript Geolocation API only after user intent, and always provide a fallback flow for denied permissions (manual location input).

## Location Data Standards
- Coordinate format: represent latitude/longitude as decimal degrees.
- Coordinate precision: persist up to 6 decimal places; return up to 5 decimal places in API responses unless a feature explicitly requires more.
- Coordinate validation: reject latitude outside [-90, 90] and longitude outside [-180, 180].
- Freshness policy: treat coordinates older than 15 minutes as stale for event/recommendation endpoints.
- Accuracy policy: when available, include `accuracyMeters`; reject precision-sensitive requests if accuracy is worse than 5000 meters.
- Time standard: persist all backend timestamps in UTC; render times in client local timezone.
- Request payload standard: location-driven requests include `latitude`, `longitude`, `capturedAtUtc`, and optional `accuracyMeters`.
- Source and fallback: if geolocation permission is denied/unavailable, support manual location entry and label source as `manual`.
