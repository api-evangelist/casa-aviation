# Civil Aviation Safety Authority (CASA)

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
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

The Civil Aviation Safety Authority (CASA) is Australia's independent statutory aviation safety regulator, established under the Civil Aviation Act 1988. It maintains the Australian Civil Aircraft Register (VH- marks), issues Airworthiness Directives, licenses flight crew and maintenance organisations, certifies air operators, and regulates drone and RPAS operations. CASA sits entirely OUTSIDE the travel distribution chain — it is a safety regulator, not a distributor, so it has no GDS, NDC, channel-manager or OTA position, and airline fare distribution, full-content agreements and consumer disclosure are not CASA functions. Its API posture is split and honest: two genuinely open, no-key, documented bulk data products (the full Airworthiness Directives listing as JSON/CSV and the complete civil aircraft register as a daily CSV, both served from services.casa.gov.au), and one approval-gated partner API — the CASA RPAS Digital Platform at data.casa.rpasplatform.net — whose endpoints are named in public PDFs but require a service account, a signed four-year agreement, a CASA onboarding check-out and a paid Airservices Australia airspace data licence. There is no self-serve developer portal, no OpenAPI, and new RPAS Platform onboarding is currently paused pending Airservices' Flight Information Management System.

**Areas:** Travel · Australia · Aviation · Airports · Government · Regulator · Aviation Safety · Open Data · Drones

## Civil Aviation Safety Authority (CASA) on APIs.io

Everything profiled for Civil Aviation Safety Authority (CASA) is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/casa-aviation/](https://apis.io/providers/casa-aviation/)** — or go straight to one of the APIs or properties below.

### APIs (3)

- [CASA Airworthiness Directives Data Files](https://apis.io/apis/casa-aviation/casa-airworthiness-directives-data/) — Open, unauthenticated bulk data files covering every current Australian Airworthiness Directive (AD). combinedadweb.json lists all current ADs with aircraft…
- [Australian Civil Aircraft Register Data Files](https://apis.io/apis/casa-aviation/casa-aircraft-register-data/) — The complete Australian Civil Aircraft Register published as a daily comma-delimited data file (acrftreg.csv, approximately 7.6MB) and a zip compressed…
- [CASA RPAS Digital Platform API](https://apis.io/apis/casa-aviation/casa-rpas-digital-platform/) — A partner-only API that supplies CASA advisories, notifications and geospatial map data to drone safety applications, and processes Automated Airspace…

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [casa-aviation-mcp.yml](https://apis.io/servers/casa-aviation/casa-aviation-mcp-yml/)

#### JSON Schema (3)

The data models the API reads and writes.

- [CASA Airworthiness Directive listing row (adweb.csv) and series row (folder.csv)](https://apis.io/schemas/casa-aviation/casa-aviation-ad-listing-row.schema/)
- [Australian Civil Aircraft Register row (acrftreg.csv)](https://apis.io/schemas/casa-aviation/casa-aviation-aircraft-register-row.schema/)
- [CASA Airworthiness Directive record (combinedadweb.json)](https://apis.io/schemas/casa-aviation/casa-aviation-airworthiness-directive.schema/)

#### Vocabulary (1)

The provider's domain terms, defined.

- [Casa Aviation Vocabulary](https://apis.io/vocabularies/casa-aviation/casa-aviation-vocabulary/)

#### Examples (2)

Example requests and responses.

- [Casa Aviation Aircraft Register Examples](https://apis.io/examples/casa-aviation/casa-aviation-aircraft-register-examples/)
- [Casa Aviation Airworthiness Directives Examples](https://apis.io/examples/casa-aviation/casa-aviation-airworthiness-directives-examples/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Casa Aviation Authentication](https://apis.io/security/casa-aviation/casa-aviation-authentication/)
- [Casa Aviation Domain Security](https://apis.io/security/casa-aviation/casa-aviation-domain-security/)
- [Casa Aviation Vulnerability Disclosure](https://apis.io/security/casa-aviation/casa-aviation-vulnerability-disclosure/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://www.casa.gov.au/)
- [Documentation](https://www.casa.gov.au/aircraft/aircraft-registration/data-files-registered-aircraft)
- [Getting started](https://www.casa.gov.au/aircraft/aircraft-registration/data-files-registered-aircraft/downloading-and-using-our-data-files)
- [Support](https://www.casa.gov.au/about-us/contact-us)
- [Blog](https://www.casa.gov.au/about-us/news-media-releases-and-speeches)
- [Security](https://www.casa.gov.au/about-us/reporting-and-accountability/external-security-vulnerability-disclosure-program)
- [Terms of service](https://www.casa.gov.au/sites/default/files/2021-09/rpas-platform-terms-conditions.pdf)
- [Privacy policy](https://www.casa.gov.au/about-us/about-website/privacy-statement)
- [Status](https://my.casa.gov.au/outage/)

## API Evangelist rating

**Kin Score 24.9** — emerging · rubric 0.24.0 · scored 2026-10-17

| Facet | Score |
|---|---|
| Discoverability | 71.4 |
| Contract quality | 9.9 |
| Contract governance | 8.3 |
| Operational transparency | 21.1 |
| Developer ergonomics | 37.5 |
| Access clarity | 10.5 |

**Agent readiness 7.6** — agent-aware

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | — |
| Agentic Access | — |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | documented (partial credit) |
| OpenAPI Examples | documented (partial credit) |
| Rate Limit Signal | — |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | — |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |

**Regulatory alignment 26.5** — Government & Public Sector

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/casa-aviation/](https://apis.io/providers/casa-aviation/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Civil Aviation Safety Authority (CASA): the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/casa-aviation/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
