# Proposal

## Why

The current weather API only serves data for a few major regions. There is a growing demand among users in Germany to access official weather information via the German Meteorological Service (DWD). Adding a dedicated Germany weather endpoint will improve local relevance, compliance with local regulations, and user satisfaction.

## What Changes

- Expose a new API endpoint `/weather/germany` that returns the latest weather data sourced from DWD.
- Adjust the data model to accommodate country‑specific attributes.
- Create a service integration client for interacting with the DWD API.
- Document the new endpoint in the public API specification.

## Capabilities

### New Capabilities
- `weather-germany`: Provide a country‑specific weather endpoint backed by the DWD service.

### Modified Capabilities
*(None; the change introduces a wholly new capability.)*

## Impact

- Code changes in the weather service layer and API router.
- New external dependency on DWD API (HTTP client).
- Updated OpenAPI docs for the new endpoint.
- Possible updates to the configuration and deployment for authentication with DWD.
