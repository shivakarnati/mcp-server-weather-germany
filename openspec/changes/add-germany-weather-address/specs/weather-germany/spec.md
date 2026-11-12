# Spec Delta

## Purpose
Provide an HTTP endpoint that returns current weather information for Germany, sourced from the German Meteorological Service (DWD).

## ADDED Requirements

### Requirement: Germany Weather Endpoint
The system SHALL provide an HTTP GET endpoint `/weather/germany` that returns weather data in JSON format, including temperature, humidity, wind speed, and forecast.

#### Scenario: Successful retrieval
- **WHEN** a client sends a GET request to `/weather/germany` with valid authentication
- **THEN** the system responds with HTTP 200 and a JSON payload containing temperature, humidity, wind speed, and forecast for Germany.

### Requirement: DWD Integration
The system SHALL retrieve weather data from the DWD public API and cache the results for 10 minutes to reduce external calls.

#### Scenario: Cached response
- **WHEN** a client requests `/weather/germany` and a cached response exists
- **THEN** the system returns the cached JSON payload with HTTP 200.

#### Scenario: Cache miss
- **WHEN** a client requests `/weather/germany` and no cached response exists
- **THEN** the system calls the DWD API, stores the result in cache, and returns the JSON payload with HTTP 200.
