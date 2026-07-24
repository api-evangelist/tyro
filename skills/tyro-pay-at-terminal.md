---
name: Take an in-store payment on a Tyro EFTPOS terminal
description: Drive a card-present payment on a paired Tyro EFTPOS terminal from a POS using the Tyro Pay Terminal (cloud) API.
api: openapi/tyro-pos-pay-terminal.yml
operations: [create-pay-terminal-request, get-pay-terminal-request, cancel-pay-terminal-request, answer-pay-terminal-prompt, list-pay-terminal-merchants, list-pay-terminal-merchants-terminals]
---

# Take an in-store payment on a Tyro EFTPOS terminal

Base URL: `https://api.tyro.com/connect`. Auth: OAuth 2.0 client_credentials JWT bearer. This is a POS Cloud Connection flow.

## Steps
1. **list-pay-terminal-merchants** / **list-pay-terminal-merchants-terminals** — Resolve the merchant and the terminal(s) paired to it.
2. **create-pay-terminal-request** — Send a payment (or refund) request to a specific terminal; you get a request id.
3. **get-pay-terminal-request** — Poll for the transaction outcome as the cardholder taps/inserts.
4. **answer-pay-terminal-prompt** — Respond to interactive terminal prompts (e.g. signature, account selection) when the request surfaces one.
5. **cancel-pay-terminal-request** — Cancel an in-flight request if the operator aborts.

## Rules
- Errors return `{error|errorMessage, errorCode}`. Poll rather than assume; handle `PENDING`/`UNKNOWN` gateway outcomes by reconciling before retrying.
- Prefer webhooks/WebSockets (`pos/notifications`) over tight polling for terminal state.
