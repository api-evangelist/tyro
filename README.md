# Tyro Payments

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Tyro Payments is an ASX-listed Australian payments company (ASX:TYR) and one of the country's
largest merchant acquirers outside the major banks, holding its own Australian banking licence.
Founded in 2003, Tyro provides EFTPOS terminals, in-person and online card acceptance, and
integrated payments for more than 70,000 Australian merchants across hospitality, retail and
health. Home market is Australia.

Tyro's developer surface, **Tyro Connect**, is a genuinely API-first platform. It exposes a family
of versioned REST APIs served from a single base URL — `https://api.tyro.com/connect` — secured with
OpenID Connect / OAuth 2.0 (Auth0-backed, client-credentials and device-code flows). Alongside the
APIs, Tyro ships **Tyro.js**, mobile SDKs, and **Tap to Pay** (SoftPOS) for card-present and online
payments.

## Developer resources

- Developer landing: https://www.tyro.com/resources/developer/
- Tyro Connect docs: https://docs.connect.tyro.com/
- API reference (App Partners): https://docs.connect.tyro.com/app/apis/
- Authentication: https://docs.connect.tyro.com/app/authentication
- Webhooks: https://docs.connect.tyro.com/app/webhooks
- Status: https://status.tyro.com/
- GitHub: https://github.com/tyro

## APIs

All served from `https://api.tyro.com/connect`, authenticated with OpenID Connect / OAuth 2.0.
Machine-readable OpenAPI 3.1.0 documents for each are harvested verbatim into [`openapi/`](openapi/).

**Payments**

- **Pay API** — server-side companion to Tyro.js and mobile SDKs for online card acceptance:
  pay requests, saved pay methods (tokenization), refunds, 3-D Secure, Apple Pay / Google Pay.
- **Pay Terminal API** — drive Tyro EFTPOS terminals in-store from a Point of Sale.
- **Embedded Payments API** — Tap to Pay on iPhone / Android (SoftPOS) card-present transactions.
- **Refunds API** — search prior Tyro transactions and issue refunds.
- **Reporting API** — merchant settlement and transaction reporting for reconciliation.

**Hospitality & POS network**

- **Ordering API** — send food/retail orders into merchant POS systems.
- **Booking API** — exchange reservation/booking information with POS.
- **Menu API** — sync published menu / catalogue data from POS to app partners.
- **Tables Management API** — table (floor-plan) data for pay-at-table workflows.
- **Sales Data API** — itemised sales transaction data from POS.
- **Loyalty Data API** — connect loyalty/rewards providers to Tyro merchants.
- **Location API** — resolve merchant location details by Tyro Connect location id.
- **Referrals API** — submit and track merchant referrals into Tyro.

## Other surfaces

- **Tyro eCommerce (MPGS)** — enterprise online card gateway, white-labelled Mastercard Payment
  Gateway Services, documented at `tyro.gateway.mastercard.com` (Mastercard-owned spec).
- **Tyro Point of Sale (Integrated EFTPOS)** — legacy terminal integration docs at
  `docs.integrated-eftpos.tyro.com`.
- **Tyro Health** — separate health claims/payments product line with its own developer hub at
  `tyrohealth.com/developers`.

## Authentication

OpenID Connect / OAuth 2.0 (Auth0-backed).

- Issuer: `https://auth.connect.tyro.com/`
- Token endpoint: `https://auth.connect.tyro.com/oauth/token`
- Discovery: `https://auth.connect.tyro.com/.well-known/openid-configuration`
- Flows: Client Credentials (server-to-server / POS cloud), Device Authorization (POS instances)

---

Maintained by [Kin Lane](https://apievangelist.com) — kin@apievangelist.com — as part of the
[API Evangelist](https://apievangelist.com) network.
