---
name: Distribute a LiveRamp segment to a destination platform
description: Take an existing LiveRamp segment and get it delivered to a marketing destination, from picking the destination through confirming the delivery landed.
api: openapi/liveramp-activation-api-openapi.yml
base_url: https://api.liveramp.com/activation
operations:
  - Get v2/Destinations
  - Get v2/Destination::Integrations
  - Create v2/IntegrationConnection
  - Get v2/IntegrationConnection
  - Create v2/DistributionManager
  - Create v2/DistributionManager::SegmentConfigs
  - Get v2/Segments
  - Get v2/SegmentStatuses
  - Get v2/Deliveries
generated: '2026-08-13'
method: generated
source: openapi/liveramp-activation-api-openapi.yml, https://developers.liveramp.com/activation-api/reference/distribution-api-overview
---

# Distribute a LiveRamp segment to a destination platform

LiveRamp's Activation API distributes audience segments to marketing platforms. Five nouns matter,
in this order: **Destination** (the platform), **Destination Integration** (a specific way into
that platform), **Integration Connection** (your customer's authorized link to it), **Distribution
Manager** (the recurring distribution job), and **Segment Config** (a segment enrolled in that
job). Deliveries are the receipts.

## Before you start

- Get a bearer token from `https://serviceaccounts.liveramp.com/authn/v1/oauth2/token` using the
  OAuth 2.0 password grant: `grant_type=password`, `username=<Account ID>`,
  `password=<Secret Key>`, `scope=openid`, `client_id=liveramp-api`.
- The token is short-lived — the documented example expires in **600 seconds**. Fetch a new one
  when you get a **403** for token expiration. Share one token across a thread; do not refresh per
  call.
- Send `Authorization: Bearer <access_token>` and the `LR-Org-Id` header naming the customer
  organization you are acting for. `LR-Org-Id` replaced the older `LR-Customer-Id`.
- You cannot self-provision. A LiveRamp representative issues the Service Account, and **each of
  your customers needs their own**.

## Steps

1. **Find the destination.** `Get v2/Destinations` lists the platforms available to this
   organization. `Get v2/Destination` reads one.
2. **Find the integration inside it.** `Get v2/Destination::Integrations` lists the integrations
   for a destination; `Get v2/Destination::Integration` reads one. The integration — not the
   destination — is what you connect to.
3. **Create the connection.** `Create v2/IntegrationConnection`. Read it back with
   `Get v2/IntegrationConnection` and check `oauthStatus`, which is one of `NotApplicable`,
   `Authorized`, or `Unauthorized`. If it is `Unauthorized`, the destination needs an OAuth
   authorization first — run the *Authorize a destination over OAuth* skill and come back.
4. **Create the distribution manager.** `Create v2/DistributionManager`, bound to the integration
   connection. This is the durable object that owns the recurring distribution.
5. **Enroll segments.** `Create v2/DistributionManager::SegmentConfigs`. **Hard limit: 500
   segments per call.** Batch accordingly; the matching delete
   (`Delete v2/DistributionManager::SegmentConfigs`) carries the same cap. Use `Get v2/Segments`
   first if you need to resolve segment IDs.
6. **Watch the segment.** `Get v2/SegmentStatuses` reports distribution status. It is scoped to
   **either** first-party (onboarding) **or** data-marketplace segments — you must pass exactly
   one of the segmentID parameter families, never both.
7. **Confirm delivery.** `Get v2/Deliveries` lists what actually went out.

## Rules an agent must not break

- **No idempotency contract.** The Activation API publishes no `Idempotency-Key` header and no
  deduplication behavior. A retried `Create v2/DistributionManager` or
  `Create v2/IntegrationConnection` can create a second object. Read before you re-create.
- **Errors are not RFC 9457.** Expect `{"error": {"message", "code", "requestId"}}`. Quote
  `requestId` to support.
- **Two operations return 207 Multi-Status.** A 2xx does not mean every item in the request
  succeeded — read the per-item results.
- **No rate-limit headers exist.** LiveRamp documents no `X-RateLimit-*` / `RateLimit-*` response
  headers on this API, so you cannot read remaining quota. Pace yourself and back off on 5xx
  (1s, 2s, 4s, 3–5 attempts).
- **TLS 1.2 minimum**, and all traffic passes through Cloudflare — a non-allowlisted source IP
  gets a Cloudflare error page rather than a LiveRamp error document.

## Cross-references

- `authentication/liveramp-authentication.yml`
- `conventions/liveramp-conventions.yml`
- `errors/liveramp-error-codes.yml`
- `rate-limits/liveramp-rate-limits.yml`
