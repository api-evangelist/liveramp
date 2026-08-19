---
name: Stand up a LiveRamp clean room and run a question
description: Create a clean room, bring a partner and data in, configure a question, run it, and get the results out — the core LiveRamp Clean Room (formerly Habu) collaboration loop.
api: openapi/liveramp-clean-room-api-openapi.yml
base_url: https://api.habu.com/v1/
operations:
  - getHealth
  - createCleanroom
  - getAllCleanrooms
  - getCleanroomById
  - addCleanroomPartner
  - getAllCleanroomPartners
  - createDataConnection
  - getAllDataConnections
  - configureCleanroomDataset
  - getCleanroomDatasets
  - createQuestion
  - addCleanroomQuestion
  - configureCleanroomQuestionDatasets
  - configureCleanRoomQuestionPermissions
  - createCleanroomQuestionRun
  - getCleanroomQuestionRunById
  - getCleanroomQuestionRunData
  - getCleanroomQuestionRunOutputFile
  - createDataExportJobs
  - getDataExportJobRuns
generated: '2026-08-13'
method: generated
source: openapi/liveramp-clean-room-api-openapi.yml
---

# Stand up a LiveRamp clean room and run a question

The Clean Room API is the former Habu platform — it lives on `https://api.habu.com/v1/` and its
own specification names the contact as "LiveRamp (previously Habu)". It is by far the largest
LiveRamp API: 151 operations, 294 schemas.

## Before you start

- Auth is **OAuth 2.0 client credentials** against `https://api.habu.com/v1/oauth/token`. This is
  a *different* token service from the rest of the LiveRamp portfolio. The declared scopes map is
  empty — request no scopes.
- `getHealth` (`GET /health`) is the availability probe. Call it first if you are unsure the
  environment is reachable.

## Steps

1. **Create the room.** `createCleanroom`. `getCleanroomTypes` tells you what kinds exist;
   `getAllCleanrooms` / `getCleanroomById` read them back.
2. **Bring the partner in.** `addCleanroomPartner`, then `getAllCleanroomPartners` to confirm.
   Invitations are their own surface — `listPartnerInvitationsForInviter` to see pending ones,
   `cancelPartnerInvitationById` to withdraw one.
3. **Connect data.** `createDataConnection` (browse what is available with `getAllDataSources`
   and `getAllDataSourceParameters` first). If a connection job fails, `retryDataConnectionJob`
   rather than creating a duplicate connection.
4. **Configure the dataset into the room.** `configureCleanroomDataset`, then
   `getCleanroomDatasets`. `updateCleanroomDatasetPartnerAssignment` controls which partner owns
   which dataset.
5. **Author the question.** `createQuestion` defines it;  `addCleanroomQuestion` attaches it to a
   specific clean room. `configureCleanroomQuestionDatasets` binds the datasets it may read, and
   `configureCleanRoomQuestionPermissions` decides who may run it. **Do not skip the permissions
   call** — a clean room's whole point is that a question can only see what it was permitted to
   see.
6. **Run it.** `createCleanroomQuestionRun`. For recurring analysis use
   `createCleanroomQuestionRunSchedule` instead of polling-and-recreating.
7. **Wait and read.** `getCleanroomQuestionRunById` for status,
   `getCleanroomQuestionRunDataCount` for size before you pull,
   `getCleanroomQuestionRunData` for the rows, `getCleanroomQuestionRunOutputFile` for a file.
   `getCleanroomQuestionRunAudit` gives you the audit trail and
   `getCleanroomQuestionRunExplainPlan` explains what the engine did.
8. **Export.** `createDataExportJobs` moves results out; `getDataExportJobRuns` tracks them.
   Destinations are provisioned per room with `provisionCleanroomDestinations`.

## Rules an agent must not break

- **Every create is non-idempotent.** There is no idempotency key anywhere in this API. A retried
  `createCleanroom` or `createDataExportJobs` makes a second one. Always list-then-create.
- **Count before you pull.** `getCleanroomQuestionRunDataCount` exists so you do not stream an
  unbounded result set into a context window.
- **409 and 412 are real here.** Two operations return 409 Conflict and one returns 412
  Precondition Failed — treat them as "your view is stale", re-read, and retry deliberately.
- **Permissions and result shares are separate.** `configureCleanRoomQuestionPermissions` governs
  who may run; `upsertCleanRoomQuestionResultShares` governs who may see results. Setting one
  does not set the other.
- **Billing is in the API.** `getBillableConfig` / `upsertBillableConfig` change what a room
  costs. Treat these as high-consequence writes requiring a human.

## Cross-references

- `authentication/liveramp-authentication.yml`
- `data-model/liveramp-data-model.yml`
- `agentic-access/liveramp-agentic-access.yml`
