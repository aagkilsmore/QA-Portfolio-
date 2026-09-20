# API Testing — reqres.in Authentication

## Objective
Verify that reqres.in's user-listing endpoint correctly enforces API key
authentication, both accepting valid requests and rejecting invalid ones.

## Tool
Postman

## Test Case 1: Get users list (authenticated)
**Endpoint:** GET https://reqres.in/api/users?page=2
**Headers:** x-api-key: [valid key]

**Steps:** Send GET request with valid x-api-key header

**Expected Result:** 200 OK, JSON response with paginated user data

**Actual Result:** 200 OK — request succeeded once a valid x-api-key header was included

**Note:** Initial attempts without the x-api-key header returned errors (429/403).
This confirmed reqres.in enforces API-key authentication on all endpoints (a 2026
platform change from its earlier no-auth model) — diagnosing this required
checking current API documentation rather than assuming the request itself was
malformed.

**Result:** Pass

## Test Case 2: Get users list (no/invalid API key)
**Endpoint:** GET https://reqres.in/api/users?page=2
**Headers:** x-api-key removed/invalid

**Steps:** Send the same GET request as Test Case 1, but remove or invalidate the x-api-key header

**Expected Result:** Request should be rejected with an authentication/authorization error — not 200

**Actual Result:** 403 Forbidden — API correctly denied the request

**Result:** Pass — confirms the API enforces key-based authentication and does
not process requests without valid credentials

## Summary
Paired positive/negative testing (valid key → 200, invalid/missing key → 403)
confirms reqres.in's authentication layer behaves correctly in both directions.
