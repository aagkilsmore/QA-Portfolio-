# GenAI-Assisted Test Case Generation

## Feature under test
SauceDemo checkout flow (first name, last name, zip code fields)

## Prompt used
"Generate 5 test cases for an e-commerce checkout flow that includes entering
first name, last name, and zip code, then confirming order details before final
purchase. Include both valid and invalid input scenarios."

## AI-generated test cases
1. Valid checkout: enter valid first name, last name, zip code → proceed to order summary
2. Empty first name field → error message, checkout blocked
3. Empty zip code field → error message, checkout blocked
4. Special characters in name field → system should either accept or reject with clear validation message
5. Order summary displays correct item(s), quantity, and total price before final purchase

## My review — executed against SauceDemo

**Case 1 (empty first name):** Confirmed. Error message "First Name is required"
displayed, checkout blocked as expected. AI's prediction was correct.

**Case 2 (empty zip code):** Confirmed. Error message "Postal Code is required"
displayed, checkout blocked as expected. AI's prediction was correct.

**Case 3 (special characters):** I tested this against the zip code field rather
than name, since it's the more realistic real-world input error. Result:
checkout proceeded successfully even with invalid/nonsensical characters in the
zip code field — no validation was enforced. The AI's test case correctly
identified this as a scenario worth checking, but did not predict which outcome
was more likely. Logged as [BUG-004](../02-bug-reports/BUG-004.md).

## Takeaway
The AI was accurate on required-field validation (cases 1 and 2) but couldn't
predict whether the app would actually enforce format validation on the zip
field — it only correctly identified that the scenario needed testing. That
distinction matters: AI-generated test cases are useful for scoping what to
check, but the actual pass/fail verdict still requires a human to run the test
and observe real behavior.
