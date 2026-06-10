# Architecture
- Frontend: NextJS with Typescript and TailwindCSS
- Backend: FastAPI with SQLModel
- Database: Postgres hosted on Neon.tech
- Auth: JWT based auth

## External Data Sources
- NASA NEO API: source for near-earth object visibility and related observation data.

## Client Capabilities
- Mobile geolocation: Use the JavaScript Geolocation API on supported mobile browsers to capture user latitude/longitude for local sky and place recommendations.

## Location Data Contract
- Coordinate format: latitude and longitude as decimal degrees.
- Coordinate precision: store up to 6 decimal places (about 0.11 m at the equator) and return up to 5 decimal places in API responses for client use.
- Valid ranges: latitude must be between -90 and 90, longitude must be between -180 and 180.
- Freshness: location is treated as fresh for 15 minutes for event and recommendation queries; after 15 minutes, the client should request updated coordinates.
- Accuracy handling: frontend should pass `accuracy` (meters) when available; backend should reject coordinates with accuracy worse than 5000 m for precision-sensitive features.
- Timezone handling: backend stores timestamps in UTC only; frontend renders event times in the device local timezone.
- Request contract: client sends `latitude`, `longitude`, `capturedAtUtc`, and optional `accuracyMeters` with location-driven queries.
- Fallback behavior: if permission is denied or unavailable, client supports manual location input and marks source as `manual`.

## Design Patterns
- Component-based ui with hooks

## Folder Layout
- `project root/`
    - `src/`: This folder will contain the entry points for both the frontend and backend applications, along with the `package.json` and `requirements.txt`.
        - `frontend/`: This will contain the NextJS app
        - `backend/`: This will contain the FastAPI app

