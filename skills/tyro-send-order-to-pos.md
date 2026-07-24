---
name: Send an order into a merchant POS and track its lifecycle
description: Push a food/retail order from an app partner into a merchant Point of Sale via the Tyro Connect Ordering API and follow its status.
api: openapi/tyro-connect-ordering.yml
operations: [create-order, get-order, update-order]
---

# Send an order into a merchant POS and track its lifecycle

Base URL: `https://api.tyro.com/connect`. Auth: OAuth 2.0 client_credentials JWT bearer.

## Steps
1. **create-order** — Submit a new order (line items, modifiers, location) into the merchant POS. You receive an `orderId`.
2. **get-order** — Read current order state.
3. **update-order** — Update the order where the merchant/POS allows it.

## Rules
- Track lifecycle via webhooks: `ORDER_CREATED`, `ORDER_ACCEPTED`, `ORDER_REJECTED`, `ORDER_BEING_PREPARED`, `ORDER_READY`, `ORDER_OUT_FOR_DELIVERY`, `ORDER_FULFILLED`, `ORDER_CANCELLED_BY_CUSTOMER`, `ORDER_CANCELLED_BY_MERCHANT`. Verify `Tyro-Connect-Signature` (HMAC-SHA256) and ignore duplicate/out-of-order/unknown events.
- Errors use `{error|errorMessage, errorCode}`; a `409` indicates an order status conflict.
