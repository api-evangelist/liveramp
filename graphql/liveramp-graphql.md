# LiveRamp GraphQL — NOT A REAL SURFACE

> **Provenance correction, 2026-08-13.** LiveRamp publishes **no GraphQL endpoint** for any of its
> APIs. The `liveramp-schema.graphql` file in this directory is **not a harvested schema** — it is
> a conceptual model that an earlier pass wrote by hand from the REST documentation. It describes
> types, queries and mutations LiveRamp has never shipped.
>
> It is retained only so the record of what was written is not lost, and the `type: GraphQL`
> pointer has been **removed from `apis.yml`** so the catalog no longer credits LiveRamp with a
> GraphQL API it does not have. Do not treat `liveramp-schema.graphql` as a contract, do not
> derive artifacts from it, and do not publish it as LiveRamp's.

**Endpoint:** none. Probed: no `/graphql` surface is documented on `developers.liveramp.com`, and
LiveRamp's own `/.well-known/api-catalog` linkset names ten REST API surfaces and zero GraphQL
ones.

**What LiveRamp actually publishes as machine-readable contracts:**

| API | Contract | Base |
| --- | --- | --- |
| Activation API | OpenAPI 3.0.1, 26 operations | `https://api.liveramp.com/activation` |
| Clean Room API | OpenAPI 3.0.0, 151 operations | `https://api.habu.com/v1/` |
| Privacy API | OpenAPI 3.0.1, 2 operations | `https://privacy-api.liveramp.com` |

See `openapi/`, and `mcp/liveramp-tool-crosswalk.yml` for how the REST surface compares to
LiveRamp's MCP surface.

**One GraphQL caveat worth recording:** LiveRamp's `logscale-mcp` server speaks GraphQL — but to
*CrowdStrike LogScale*, a third-party product. That is not a LiveRamp GraphQL API.

- Documentation: https://developers.liveramp.com/
- API catalog: https://developers.liveramp.com/.well-known/api-catalog
