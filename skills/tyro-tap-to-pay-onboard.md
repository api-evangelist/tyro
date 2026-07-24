---
name: Onboard a merchant device for Tap to Pay (Embedded Payments)
description: Register a Reader and device connection so a mobile device can accept card-present payments via the Tyro Embedded Payments (SoftPOS / Tap to Pay) SDK.
api: openapi/tyro-pos-embedded-payments.yml
operations: [list-embedded-payments-locations, create-reader, create-embedded-payments-connection, authorise-embedded-payments-mid-test, get-embedded-payments-transaction, list-embedded-payments-transactions]
---

# Onboard a merchant device for Tap to Pay (Embedded Payments)

Base URL: `https://api.tyro.com/connect`. Auth: OAuth 2.0 client_credentials JWT bearer. Sandbox: obtain sandbox credentials + merchant ID from Tyro; Reader creation returns a preconfigured Reader (see `sandbox/tyro-sandbox.yml`).

## Steps
1. **list-embedded-payments-locations** — List the merchant locations available to your partner integration.
2. **create-reader** — Create a Reader (Tap to Pay device). In sandbox the returned Reader is preconfigured by Tyro; the `TAPTOPAY_READER_CREATED` webhook may fire more than once.
3. **create-embedded-payments-connection** — Create a device connection with the returned `readerId`; the SDK uses this connection to submit card-present transactions.
4. **authorise-embedded-payments-mid-test** — (Sandbox) Authorise a merchant ID to exercise the Account Authorisation flow.
5. **get-embedded-payments-transaction** / **list-embedded-payments-transactions** — Retrieve transaction outcomes (note: single-transaction fetch is not available on sandbox).

## Rules
- Subscribe to `TAPTOPAY_*` webhooks (reader created/status, transaction success/failed/refunded, merchant-id enabled/disabled); verify `Tyro-Connect-Signature` and de-duplicate.
- Certification (Technical Review) is required before going live — see `https://docs.connect.tyro.com/certification/embedded-payments-sdk`.
