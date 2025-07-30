# 1. Input Validation & Constraints
🧩 Scenario: "As a user, I can update my profile name."

✅ Acceptance: “User can input a name with up to 50 characters.”

❓ Ask:

- What happens if the frontend sends 100 characters?
- Do we trim leading/trailing whitespace?
- What if the name contains emojis or control characters?
- Is the name field nullable?
- Do we need to normalize Unicode?
# 2. Missing or Null Fields
🧩 Scenario: "As a user, I can upload a profile picture."

✅ Acceptance: “User can upload an image file (JPG or PNG).”

❓ Ask:

- What if no file is sent at all?
- What if the file name is missing?
- What if content-type is wrong but file extension is right?
- What if the image is corrupted or has 0 bytes?
- What if the upload endpoint receives a multipart request but no files?
# 3. Boundary & Edge Conditions
🧩 Scenario: "As a user, I can transfer up to $10,000."

✅ Acceptance: “The app should reject transfers above $10,000.”

❓ Ask:

- What if the amount is exactly $10,000? 9999.999999?
- What if the amount is negative?
- Is currency always in the same decimal format (e.g., 2 digits)?
- Do we allow 0 amount? Or cents?
- Is there a minimum threshold?
# 4. Concurrency & Timing
🧩 Scenario: "User can cancel a booking."

✅ Acceptance: “Only future bookings can be canceled.”

❓ Ask:

- What if two cancel requests come at the same time?
- What if the booking is being processed at the same moment?
- Is the current time checked from server or client?
- What if server time and DB time differ slightly?
# 5. Dependency Failures
🧩 Scenario: "System calls an external payment service."

✅ Acceptance: “On success, mark the payment as ‘completed’.”

❓ Ask:

- What happens if the payment service times out?
- What if it responds slowly or with malformed JSON?
- Do we retry on transient errors?
- Do we log the full request/response for debugging?
- How do we ensure idempotency if the same request is sent twice?
  
# 6. Authorization / Role Misuse
🧩 Scenario: "Admin can download user reports."

✅ Acceptance: “Admins can click to export a CSV report.”

❓ Ask:

- What if a non-admin calls the endpoint directly?
- Are roles checked on backend or only UI?
- What happens if a token is expired but still used?
- Do we log unauthorized attempts?
  
# 7. Resource Limits & Quotas
🧩 Scenario: "User can upload documents."

✅ Acceptance: “Each file must be under 5MB.”

❓ Ask:

- What if a user uploads 100 files at once?
- What if total payload exceeds system memory?
- Do we handle file upload streaming to avoid memory overload?
- What if someone uploads a zip bomb?
  
# 8. Data Integrity / Business Rule Violations
🧩 Scenario: "User can submit a claim with an active policy."

✅ Acceptance: “Claim is submitted only if policy is active.”

❓ Ask:

- What if the policy status changed between form display and submission?
- Is policy status checked at submission time?
- What if the claim references a deleted policy ID?
- Are race conditions handled?
# 9. Logging & Error Transparency

🧩 Scenario: "If something goes wrong, user sees a friendly error."

✅ Acceptance: “System shows a generic error page.”

❓ Ask:

- Is the root cause logged (with context like user ID or request ID)?
- Do we avoid exposing stack traces in the API response?
- Is the error recoverable or fatal?
# 10. Assumption Checks
🧩 Scenario: "The system assumes all users have verified emails."

✅ Acceptance: “Email must be verified before accessing dashboard.”

❓ Ask:

- What if a user was created before this rule existed?
- What if email verification record is missing or corrupted?
- Is the check enforced on every dashboard call?

# ✅ Summary Table
| Category  | Defensive Questions to Ask  |
|---|---|
| Input Validation  | Are inputs sanitized, bounded, and correctly typed?  |
| Null/Missing Fields  | Are all required fields present and validated?  |
| Boundary Conditions  |  What happens at limits (0, max, negative)? |
| Concurrency  |  Are race conditions handled safely? |
| Dependency Failure  |  Are timeouts, retries, and fallbacks implemented? |
| Authorization  |  Are timeouts, retries, and fallbacks implemented? |
| Quota/Limits  |  Can the system handle abuse or DoS scenarios? |
| Data Integrity  |  Are business invariants enforced at the DB/API? |
| Logging/Error Handling  |  Are logs useful for debugging, but safe for end users? |
| Implicit Assumptions  |  What assumptions might silently break? |
