---
name: Submit and track a LiveRamp privacy request
description: File a data-subject request (opt-out, deletion) with LiveRamp and track it, using the one endpoint in the portfolio that is safely retryable.
api: openapi/liveramp-privacy-api-openapi.yml
base_url: https://privacy-api.liveramp.com
operations:
  - Create PrivacyRequests
  - Get PrivacyRequests
generated: '2026-08-13'
method: generated
source: openapi/liveramp-privacy-api-openapi.yml, https://developers.liveramp.com/privacy-api/reference/error-handling-retries
---

# Submit and track a LiveRamp privacy request

Two operations, and the only endpoint in the entire LiveRamp portfolio with a documented
idempotency contract.

## Before you start

- Auth is a bearer JWT (`BearerAuth`, `bearerFormat: JWT`) obtained from the LiveRamp service
  account token service at `https://serviceaccounts.liveramp.com/authn/v1/oauth2/token`.
- Two environments are declared in the specification: production
  `https://privacy-api.liveramp.com` and staging `https://privacy-api.staging.liveramp.com`.
  Staging credentials are not self-serve — ask your LiveRamp representative.

## Steps

1. **Create the request.** `Create PrivacyRequests` — `POST /v1/requests`. Supported subject
   identifiers include mobile advertising IDs (MAIDs), added 2026-03-03.
2. **Read the response.** You get back a `request_uuid`. If `is_duplicate` is `true`, LiveRamp
   recognized this as a repeat and returned the **original** `request_uuid` rather than opening a
   second request. That is success, not an error.
3. **Track it.** `Get PrivacyRequests` — `GET /v1/requests`.

## Rules an agent must not break

- **This endpoint IS safe to retry**, and it is the only one that is. The deduplication is on the
  request's natural key, not on a client-supplied `Idempotency-Key` header — there is no such
  header. Do not generalize this behavior to the Activation or Clean Room APIs; they have no
  deduplication at all.
- **Retry only on 500, 502, 503, 504.** Use exponential backoff with jitter: 1s, 2s, 4s, maximum
  3–5 attempts.
- **Never retry 400, 401, 403 or 422.** 400 means fix the request format, 401 means check the
  token, 403 means verify organization permissions, 422 means fix validation errors. Retrying
  these wastes quota and changes nothing.
- **Privacy requests are irreversible in effect.** A deletion request is a real-world consequence
  for a real person. Treat `Create PrivacyRequests` as human-in-the-loop unless the calling system
  is itself the authenticated data-subject intake surface.

## Cross-references

- `conventions/liveramp-conventions.yml` (idempotency)
- `errors/liveramp-error-codes.yml` (retry policy)
- `sandbox/liveramp-sandbox.yml` (staging environment)
