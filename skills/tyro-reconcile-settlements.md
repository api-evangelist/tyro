---
name: tyro-reconcile-settlements
title: Reconcile a merchant's daily transactions against settlements
description: Pull a merchant's transactions for a terminal business day and the BECS-cleared settlement for a date with the Tyro Connect Reporting API, then reconcile them.
api: openapi/tyro-reporting-api-openapi.yml
apis:
- openapi/tyro-reporting-api-openapi.yml
operations:
- get-reporting-settlements
- get-reporting-transactions
---
# Reconcile a merchant's daily transactions against settlements

Base URL: `https://api.tyro.com/connect`. Auth: OAuth 2.0 client_credentials JWT sent as `Authorization: Bearer <jwt>` (see `authentication/tyro-authentication.yml`).

## Steps
1. **get-reporting-transactions** - `GET /reporting/merchants/{mid}/transactions` with `transactionDate`, `limit` and `page`: the merchant's transactions for one terminal business day. Page through until the result set is exhausted.
2. **get-reporting-settlements** - `GET /reporting/merchants/{mid}/settlements` with `settlementDate`: the BECS-cleared settlement details for the merchant on that date.
3. Match transaction totals for the business day(s) to the settlement amount; flag the difference for review.

## Rules
- Both operations are read-only GETs, so retries are safe; no idempotency key is needed.
- `400` = bad date / parameters, `403` = your app is not authorised for that `mid` (see `errors/tyro-error-codes.yml`).
