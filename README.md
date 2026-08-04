# LiveRamp (liveramp)

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

LiveRamp is a data connectivity platform that enables enterprises to safely connect, control, and activate first-party customer data across the digital ecosystem. Their developer platform exposes a suite of REST APIs for identity resolution, data activation, clean-room collaboration, marketplace data access, and privacy-first authenticated traffic.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/liveramp/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/liveramp/refs/heads/main/apis.yml)

## Scope

- **Type:** Index
- **Position:** Consuming
- **Access:** 3rd-Party

## Tags

- Data Connectivity
- Identity Resolution
- Activation
- Clean Room
- Privacy
- AdTech

## Timestamps

- **Created:** 2026-03-16
- **Modified:** 2026-05-19

## APIs

### LiveRamp Activation API

Programmatic activation of first-party and marketplace data across destination partners and connected platforms in the LiveRamp network.

- **Human URL:** [https://developers.liveramp.com/activation-api](https://developers.liveramp.com/activation-api)

#### Tags

- Activation
- AdTech
- Marketing

#### Properties

- [Documentation](https://developers.liveramp.com/activation-api)
- [Postman Collection](collections/liveramp.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/liveramp.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### LiveRamp Authenticated Traffic Solution (ATS) API

Privacy-first, PII-based authentication API enabling programmatic addressability without third-party cookies via RampID envelopes.

- **Human URL:** [https://developers.liveramp.com/authenticatedtraffic-api](https://developers.liveramp.com/authenticatedtraffic-api)

#### Tags

- Identity
- Privacy
- Authentication

#### Properties

- [Documentation](https://developers.liveramp.com/authenticatedtraffic-api)
- [Postman Collection](collections/liveramp.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/liveramp.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### LiveRamp Clean Room API

API for setting up and managing clean rooms, data sources, and collaborative analytics queries between data partners.

- **Human URL:** [https://developers.liveramp.com/clean-room-api](https://developers.liveramp.com/clean-room-api)

#### Tags

- Clean Room
- Data Collaboration
- Privacy

#### Properties

- [Documentation](https://developers.liveramp.com/clean-room-api)
- [Postman Collection](collections/liveramp.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/liveramp.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### LiveRamp Data Marketplace Buyer API

API enabling platforms to host third-party segments from the LiveRamp Data Marketplace and access detailed segment metadata.

- **Human URL:** [https://developers.liveramp.com/datamarketplace-buyer-api](https://developers.liveramp.com/datamarketplace-buyer-api)

#### Tags

- Data Marketplace
- Segments
- AdTech

#### Properties

- [Documentation](https://developers.liveramp.com/datamarketplace-buyer-api)
- [Postman Collection](collections/liveramp.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/liveramp.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### LiveRamp AbiliTec API

Identity resolution API that resolves offline PII data into stable AbiliTec links for enterprise customer-database unification.

- **Human URL:** [https://developers.liveramp.com/abilitec-api](https://developers.liveramp.com/abilitec-api)

#### Tags

- Identity
- Resolution
- PII

#### Properties

- [Documentation](https://developers.liveramp.com/abilitec-api)
- [Postman Collection](collections/liveramp.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/liveramp.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### LiveRamp RampID API

API for matching data to the LiveRamp Identity Graph, including envelope decryption and translation between pseudonymous identifiers.

- **Human URL:** [https://developers.liveramp.com/rampid-api](https://developers.liveramp.com/rampid-api)

#### Tags

- Identity
- RampID
- Pseudonymous

#### Properties

- [Documentation](https://developers.liveramp.com/rampid-api)
- [Postman Collection](collections/liveramp.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/liveramp.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### LiveRamp Safe Haven Job Management API

Automates Python, PySpark, and BigQuery jobs running in LiveRamp's Safe Haven Analytics Environment.

- **Human URL:** [https://developers.liveramp.com/ae-job-management-api](https://developers.liveramp.com/ae-job-management-api)

#### Tags

- Analytics
- Automation
- Jobs

#### Properties

- [Documentation](https://developers.liveramp.com/ae-job-management-api)
- [Postman Collection](collections/liveramp.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/liveramp.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### LiveRamp Privacy API

Automates data subject requests including opt-outs, deletions, and consent updates across the LiveRamp ecosystem.

- **Human URL:** [https://developers.liveramp.com/privacy-api](https://developers.liveramp.com/privacy-api)

#### Tags

- Privacy
- Consent
- Compliance

#### Properties

- [Documentation](https://developers.liveramp.com/privacy-api)
- [Postman Collection](collections/liveramp.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/liveramp.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

### LiveRamp Sidecar

Service enabling SSPs to decrypt RampID identity envelopes into DSP-specific identifiers for programmatic activation.

- **Human URL:** [https://sidecar.readme.io/](https://sidecar.readme.io/)

#### Tags

- SSP
- Programmatic
- Identity

#### Properties

- [Documentation](https://sidecar.readme.io/)
- [Postman Collection](collections/liveramp.postman_collection.json) — [Postman Collection 2.1](https://schema.getpostman.com/json/collection/v2.1.0/collection.json)
- [Open Collection](collections/liveramp.opencollection.json) — [Open Collection 1.0](https://schema.opencollection.com/opencollection/v1.0.0.json)

## Common Properties

- [LinkedIn](https://www.linkedin.com/company/liveramp)
- [Website](https://liveramp.com)
- [Portal](https://developers.liveramp.com/)
- [Documentation](https://docs.liveramp.com/)
- [Support Portal](https://support.liveramp.com/)
- [Blog](https://liveramp.com/blog/)
- [GitHub Organization](https://github.com/LiveRamp)
- [M C P Server](https://github.com/LiveRamp/logscale-mcp)
- [L L Ms Txt](https://developers.liveramp.com/llms.txt)

## Maintainers

**FN:** API Evangelist
**Email:** info@apievangelist.com
