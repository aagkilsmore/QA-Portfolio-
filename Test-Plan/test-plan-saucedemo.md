# Test Plan — SauceDemo Login & Core Flows

## Objective
Verify core functionality and error handling of SauceDemo's login system,
applying manual testing techniques and browser-based network inspection.

## Scope
- Login (valid, invalid, locked-out user)

## Out of Scope
- Backend/server-side login validation (confirmed client-side only — see Test Case 1 notes)
- Performance and load testing

## Environment
- Browser: Chrome
- Tool: Chrome DevTools (Network tab)
- URL: https://www.saucedemo.com

## Test Cases

### Test Case 1: Login attempt with locked-out account
**Steps:** Navigate to saucedemo.com, enter username "locked_out_user" and password "secret_sauce", click Login
**Expected:** User is denied access with a clear reason (account locked)
**Actual:** Login denied. "Epic sadface" icon displayed with message: "Sorry, this user has been locked out."
**Network tab:** No backend API call observed. Only a GET request for the page itself (200, served from cache) — confirms login validation is handled entirely client-side, with no authentication request sent to a server.
**Result:** Pass

### Test Case 2: Login with valid username, invalid password
**Steps:** Navigate to saucedemo.com, enter username "standard_user" and an incorrect password, click Login
**Expected:** Login denied, generic error (should not reveal whether username or password was the issue)
**Actual:** Login denied. "Epic sadface" icon displayed with message: "Username and password do not match any user in this service."
**Network tab:** Same as above — no backend call, client-side validation confirmed.
**Result:** Pass — error message is appropriately generic and doesn't leak which field was wrong

## Summary
Both login scenarios passed as expected. Notable finding: login validation is
handled entirely client-side, with no backend authentication API call observed.
Error messaging is appropriately generic and does not distinguish between an
invalid username and an invalid password, which is good security practice
(prevents account enumeration).
