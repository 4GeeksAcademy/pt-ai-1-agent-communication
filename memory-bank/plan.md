# Implementation Plan

## Goal
Ship an MVP of Night Sky Tracker for mobile users with reliable local sky guidance, NEO visibility, and dark-sky place recommendations.

## Class Cadence and Time Budget
- Schedule assumption: 3 class days per week.
- Development assumption: 60 to 90 minutes of focused build time per class day.
- Delivery strategy: ship small vertical slices each week instead of large subsystem-first work.
- Scope rule: each class session ends with one demoable outcome, even if partial.

## Current Sprint (2 Weeks, 6 Sessions)

### Week 1
- Session 1: finalize MVP scope and acceptance criteria for location, NEO events, and dark-sky suggestions.
- Session 2: scaffold frontend and backend structure and create a health-check endpoint plus a basic mobile landing page.
- Session 3: implement location request flow (Geolocation API + manual fallback) and send location payload to backend.

### Week 2
- Session 4: integrate NASA NEO API in backend with normalized response shape and one query endpoint.
- Session 5: return sunrise/sunset and one event list response for a provided location/time.
- Session 6: polish a demo flow (open app -> allow location -> see sky items), then add minimal tests for location validation and endpoint response shape.

## Sprint Exit Criteria
- Mobile user can provide location (automatic or manual) and receive a valid response.
- Backend returns at least one normalized sky-data payload containing time-aware items.
- One end-to-end demo path is stable enough for classroom walkthrough.
- Basic tests exist for location validation and a core API response contract.

## Phase 1 - Foundations
- Confirm and lock product scope for MVP features from `product-context.md`.
- Finalize architecture and coding standards in `architecture.md` and `conventions.md`.
- Define API surface for location-driven requests (`latitude`, `longitude`, `capturedAtUtc`, optional `accuracyMeters`).
- Set up backend and frontend skeletons using the documented folder layout.

## Phase 2 - Core Data Integrations
- Integrate NASA NEO API for near-earth object visibility.
- Integrate light pollution baseline data source (NASA Black Marble or equivalent processed layer).
- Normalize external provider responses into internal domain models.
- Add retry/fallback behavior for provider failures and rate limits.

## Phase 3 - Location and Time Intelligence
- Implement mobile geolocation via JavaScript Geolocation API.
- Add manual location fallback for denied or unavailable permissions.
- Enforce location validation and freshness rules:
  - Latitude in [-90, 90], longitude in [-180, 180]
  - Freshness window: 15 minutes
  - Accuracy threshold for precision-sensitive features: 5000 meters
- Store timestamps in UTC and render times in device local timezone.

## Phase 4 - User Features
- Sunrise/sunset for current location.
- Event feed with observable celestial events and NEO highlights.
- Direction and time guidance for observation windows.
- Nearby dark-sky place suggestions ranked by light pollution baseline.

## Phase 5 - Quality and Operations
- Add unit tests for event/time calculations and validation rules.
- Add API contract tests for location payload and error handling.
- Add frontend interaction tests for permission and fallback flows.
- Add telemetry for DAU and feature usage against success metric targets.

## Phase 6 - Iteration
- Review usage metrics and user feedback.
- Tune ranking and recommendation logic.
- Expand provider coverage and resilience if needed.

## Exit Criteria for MVP
- Core features in product context are functional on mobile.
- Geolocation and manual fallback flows are both usable.
- NEO visibility and dark-sky suggestions are available for target regions.
- Basic reliability, observability, and test coverage gates are in place.
