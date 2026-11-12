# Design

## Context
The existing weather service provides generic region endpoints. We need to add a Germany‑specific endpoint that pulls data from the German Meteorological Service (DWD). The change introduces a new capability (`weather-germany`) and requires an external HTTP client and caching layer.

## Goals / Non‑Goals
**Goals:**
- Expose `/weather/germany` delivering current weather for Germany.
- Retrieve data from DWD and cache responses for 10 minutes to reduce external load.
- Keep the public API and core service codebase change minimal.

**Non‑Goals:**
- Refactor the entire weather service or redesign the internal data model.
- Provide a persistent database of weather history.

## Decisions
1. **Endpoint path**: `/weather/germany` – a clear country‑specific path.
2. **External client**: Use Node’s `axios` for HTTP requests; It's promise‑based and already present in the project.
3. **Caching strategy**: Use built‑in Redis cache (already in the stack). Store the DWD response keyed by a country code.
4. **Data format**: Return JSON matching existing weather payload structure; extend with DWD‑specific fields.
5. **Error handling**: On DWD API failure, return HTTP 503 with a JSON error message.
6. **Unit tests**: Mock DWD responses and Redis cache to test both cache hit and miss scenarios.

**Alternatives considered**:
- Direct database persistence of DWD data: rejected due to increased complexity and latency.
- Using a third‑party weather API: rejected because the requirement explicitly calls for DWD data.

## Risks / Trade‑offs
- **Reliability**: The change depends on external DWD service uptime. Mitigation: return cached data if available, otherwise 503.
- **Latency**: External call adds latency. Mitigation: caching and keeping the call async.
- **Future compatibility**: If DWD changes schema, this will require a spec update. Mitigation: shield internal representation behind a mapper.
