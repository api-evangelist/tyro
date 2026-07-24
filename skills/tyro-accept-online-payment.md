---
name: Accept an online card payment and refund it
description: Create, authorise/capture, and refund an online card payment with the Tyro Connect Pay API (Tyro.js / TyroSDK companion). Australia-only, AUD.
api: openapi/tyro-connect-pay.yml
operations: [create-pay-request, get-pay-request, patch-pay-request, create-refund-request, get-refund-request]
---

# Accept an online card payment and refund it

Base URL: `https://api.tyro.com/connect`. Auth: OAuth 2.0 client_credentials — POST to `https://auth.connect.tyro.com/oauth/token`, cache the JWT (12h TTL, max 12 tokens / 11h), send it as `Authorization: Bearer <jwt>`. Use `isLive=false` and Tyro test cards while integrating (see `sandbox/tyro-sandbox.yml`).

## Steps
1. **create-pay-request** — Create a Pay Request for the amount (AUD). You receive a `payRequestId` and a Pay Secret; hand the Pay Secret to Tyro.js / TyroSDK to collect card details (or a saved `payMethod` id + `customerId` to charge a stored token). Supports 3-D Secure, Apple Pay and Google Pay.
2. **get-pay-request** — Poll the Pay Request until `status` reaches `AUTHORIZED` or `CAPTURED` (or a terminal `VOIDED`/failure). Card metadata (`firstSixDigits`, `lastFourDigits`, `authorisationCode`) is on `transactionResults[]`.
3. **patch-pay-request** — Optionally update the total while `status` is `AWAITING_PAYMENT_INPUT`, or capture/void an authorised request per the payload contract.
4. **create-refund-request** — Refund a captured Pay Request (full or partial, up to the refundable amount).
5. **get-refund-request** — Confirm the refund reached a terminal state.

## Rules
- Errors return `{error|errorMessage, errorCode}` (NOT RFC 9457). Handle Pay Request codes (`PAY_REQUEST_*`), gateway declines (`DECLINED`, `INSUFFICIENT_FUNDS`, `EXPIRED_CARD`, …) and 3-D Secure codes (`THREED_SECURE_*`). See `errors/tyro-error-codes.yml` and `errors/tyro-decline-codes.yml`.
- No idempotency key: rely on Pay Request state (`AUTHORIZED`/`CAPTURED`/`VOIDED`) — never blindly re-create on a timeout; re-fetch by `payRequestId` first.
- Subscribe to webhooks (`NEW_PAY_REQUEST`, `PAY_REQUEST_SUCCESS`, `PAY_REQUEST_FAILED`, `PAY_REQUEST_VOIDED`, `NEW_PAY_REFUND`); verify `Tyro-Connect-Signature` (HMAC-SHA256) and de-duplicate.
