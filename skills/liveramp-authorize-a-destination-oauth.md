---
name: Authorize a LiveRamp destination over OAuth
description: Drive the OAuth handshake that lets a customer authorize LiveRamp to write into a destination platform, and confirm the resulting connection is usable.
api: openapi/liveramp-activation-api-openapi.yml
base_url: https://api.liveramp.com/activation
operations:
  - Create v2/OauthConnectionAttempt
  - Get v2/OauthConnectionAttempt
  - Get v2/OauthConnections
  - Get v2/OauthConnection
  - Get v2/IntegrationConnection
  - Modify v2/IntegrationConnection
generated: '2026-08-13'
method: generated
source: openapi/liveramp-activation-api-openapi.yml, https://developers.liveramp.com/activation-api/reference/oauth-configuration
---

# Authorize a LiveRamp destination over OAuth

Some destination platforms require the customer to authorize LiveRamp directly. That is a second,
separate OAuth flow from the one you use to call LiveRamp — do not confuse them.

- **Your** auth to LiveRamp: service-account password grant at
  `https://serviceaccounts.liveramp.com/authn/v1/oauth2/token`.
- **The customer's** auth to the destination: the operations in this skill.

## Steps

1. **Start the attempt.** `Create v2/OauthConnectionAttempt` for the integration you want the
   customer to authorize. The response carries the handle you poll on.
2. **Send the customer through the destination's consent screen.** This is a browser step. An
   agent cannot complete it headlessly and should not try.
3. **Poll the attempt.** `Get v2/OauthConnectionAttempt` returns where the flow stands. Poll with
   backoff, not in a tight loop — there are no rate-limit headers to tell you when to slow down.
4. **Confirm the connection exists.** `Get v2/OauthConnections` lists authorizations held for the
   organization; `Get v2/OauthConnection` reads one.
5. **Verify the integration connection flipped.** `Get v2/IntegrationConnection` and check
   `oauthStatus` is now `Authorized`. The three documented values are `NotApplicable`,
   `Authorized`, `Unauthorized`. Use `Modify v2/IntegrationConnection` if the connection needs
   updating afterwards.

## Rules an agent must not break

- **This is a human-in-the-loop flow.** Step 2 requires the customer. Never fabricate a
  redirect completion.
- **`NotApplicable` is a success state**, not a failure — many integrations do not use OAuth at
  all. Do not start an attempt for those.
- **Retries are not safe.** No idempotency key exists; a repeated
  `Create v2/OauthConnectionAttempt` starts a new attempt. Poll the existing one instead.
- **403 is ambiguous.** It can mean your LiveRamp token expired (fetch a new one) or that the
  organization lacks permission. Check token age first.

## Cross-references

- `authentication/liveramp-authentication.yml`
- `scopes/liveramp-scopes.yml`
- `errors/liveramp-error-codes.yml`
