# Superseded scaffold specifications

These files were **not published by LiveRamp**. They were written by an earlier API Evangelist
pass that hand-authored an OpenAPI outline for the Activation API from the documentation, then
split it by tag. Their paths are broadly right, but their `operationId`s, response shapes and
component schemas were invented — LiveRamp's real Activation API uses operationIds of the form
`Get v2/Destinations` and `Create v2/DistributionManager::SegmentConfigs`, not `listDestinations`
or `addSegmentConfiguration`.

On **2026-08-13** the enrichment pass found LiveRamp's real, first-party specifications and
harvested them verbatim:

| API | Source URL | Result |
| --- | --- | --- |
| Activation API | `https://storage.googleapis.com/lr-tech-docs-resources/Files/connect/activation/api/activation-api-v2.openapi.yaml` | OpenAPI 3.0.1, 26 ops, 48 schemas |
| Clean Room API | `https://storage.googleapis.com/lr-tech-docs-resources/Files/clean-room/api/liveramp-clean-room-api-specification.yml` | OpenAPI 3.0.0, 151 ops, 294 schemas |
| Privacy API | `https://storage.googleapis.com/lr-tech-docs-resources/Files/privacy/api/liveramp-privacy-api-specification.yaml` | OpenAPI 3.0.1, 2 ops, 6 schemas |

All three are linked from LiveRamp's own developer portal (`developers.liveramp.com`) and served
from LiveRamp's own documentation bucket (`lr-tech-docs-resources`). The scaffolds are retained
here only as a record; **nothing should be derived from them and no `apis.yml` pointer references
them.** They are excluded from scoring, refinement and every downstream artifact.
