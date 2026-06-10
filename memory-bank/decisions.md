# Decisions

This is going to contain decisions that have already been made, e.g. when planning I might make some decisions like "any time a component is made, it belongs in /components in an appropriate subfolder.

## 2026-06-10 - NEO data provider
- Decision: Use the NASA NEO API as the primary source for near-earth object visibility data.
- Why: It aligns directly with the product requirement to show observable near-earth objects.
- Consequence: Backend integration should normalize NASA response fields into internal event models before exposing them to clients.

## 2026-06-10 - Mobile location acquisition
- Decision: Use the JavaScript Geolocation API in the frontend to acquire user location on mobile devices.
- Why: The application is mobile-first and needs accurate local coordinates for time, direction, and nearby dark-sky recommendations.
- Consequence: Frontend must handle permission-denied and unavailable-location states with clear fallback UX.
