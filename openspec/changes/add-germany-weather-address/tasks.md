# Tasks

## 1. Setup

- [ ] 1.1 Create a new file `src/weather/germany.ts` to house the endpoint logic.
- [ ] 1.2 Add the path `/weather/germany` to the Express router and enable authentication middleware.

## 2. External Integration

- [ ] 2.1 Implement a DWD client in `src/weather/dwdClient.ts` that fetches data from `https://api.dwd.de/...`.
- [ ] 2.2 Add the dependency `axios` to `package.json` if not already present.
- [ ] 2.3 Ensure the client handles HTTP errors and timeouts, returning a clear error structure.

## 3. Caching Layer

- [ ] 3.1 Implement Redis caching logic in `src/weather/cache.ts` with a 10‑minute TTL.
- [ ] 3.2 Write unit tests that verify cache hits return the stored JSON and cache misses trigger the DWD client.

## 4. Payload Mapping

- [ ] 4.1 Map the DWD JSON response to the existing weather payload schema.
- [ ] 4.2 Handle missing or unexpected fields gracefully.

## 5. API Documentation & Specs

- [ ] 5.1 Update the OpenAPI spec to include the new `/weather/germany` endpoint.
- [ ] 5.2 Add example successful and error responses.
- [ ] 5.3 Verify that the spec compiles with `openapi-generator` or similar.

## 6. Integration Tests

- [ ] 6.1 Write an integration test that mocks the DWD API, performs a GET `/weather/germany`, and asserts the JSON fields.
- [ ] 6.2 Verify a second test where the cache is warm and no external call is made.

## 7. Deployment & Verification

- [ ] 7.1 Deploy the change to the staging environment.
- [ ] 7.2 Run end‑to‑end tests against staging to confirm endpoint works.
- [ ] 7.3 Confirm logs for DWD calls and caching behavior are as expected.

## 8. Review & Cleanup

- [ ] 8.1 Review code for linting and style consistency.
- [ ] 8.2 Update `CHANGELOG.md` to document the new Germany weather endpoint.
- [ ] 8.3 Close any related tickets in the issue tracker.

## 9. Archive

- [ ] 9.1 Mark the change as complete and run `openspec archive add-germany-weather-address`.
- [ ] 9.2 Verify the main specs are updated and the change is archived.
